---
title: Renaming database columns in production
date: 2021-10-17
draft: false
description: Gracefully pulling the rug out from under a live server.
---
Let's say you want to rename a database field on table `blog_post` from `created` to `created_at`. Everyone keeps thinking `created`is a `BOOLEAN` (and then asking you what the point of that is) and you just want it to be nice and consistent.

You can't just write a data migration, renaming the database field and changing usages in the codes base and then simply deploy that to production.

While your new release is rolling out you will have two versions of the application running at the same time: the current version (using `created`) and the next version (which uses `created_at`). 

**When the data migration runs, the currently running app will throw database errors even on select as the column with that name no longer exist.**

The correct approach is to implement and deploy this in a release:
1. Add new column `created_at` 
2. Copy the old column data to the new column:
  ```sql
  UPDATE blog_post SET created_at = created;
  ```
3. Change all usages in codebase to the new field name

After you deploy this (assuming you always run migrations during a deploy) you will have two columns. The app will only read and write to `created_at`

In the next release you can drop column `created`.

Now it is still possible that in the seconds just after the migration was executed, the old still running version managed to process one more insert which only sets `created`. If you are on a high traffic site then it's guaranteed to be a problem.

In this particular case, `created_at` would probably have a default of `NOW()`, but what if we are migrating from `org` -> `company`?

You could put some temporary glue code in to use `company` or `org` when reading the model:

```python
company = blog_post.company or blog_post.org
```

Remove that in the subsequent release.

You might think that you could install a temporary trigger to keep it updated:

```sql
create or replace function trigger_on_blog_post()
returns trigger language plpgsql as $$
begin
	new.created_at := new.created;
	return new;
end
$$;

create trigger trigger_on_blog_post
before insert or update on blog_post
-- for each row execute procedure trigger_on_example();
```

The problem here is that once the new app goes live then it's copying the wrong direction! By this point you probably want to report back to your team that we should just live with the bad name.

If you have a lot of fields to rename, if you have tables to rename, or if you have many types to fix then you should plan to migrate the data to a new schema using something like [dbt](https://www.getdbt.com/) and make the switch with a breif scheduled maintenance. This is going to be far faster and less error prone then trying to fix every single problem sequentially.



