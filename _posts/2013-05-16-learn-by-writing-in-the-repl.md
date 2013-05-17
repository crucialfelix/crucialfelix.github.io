---
layout: post
title: Learn by writing in the REPL
categories: clojure
published: true
---

Writing code is a much more effective way to learn than just reading it. I tend to gorge myself on information and reading.  Then I go to write or start a project and I realize I don't know some basic syntax form.

1 hour in the REPL is worth (some made up number) reading blogs.

In the last years I've been doing a lot of Python, JavaScript and some SuperCollider.  Clojure is a Lisp, and it uses a lot of functional programming idioms. Merely reading code examples doesn't really get them into the brain enough.

Common and good advice: when you are reading tutorials or example problems, start that REPL up and jack in.  Try not to copy and paste, but read and retype and think about what you are typing.

Notice things like "the arguments are supplied as a vector" or "its a :keyword not a #'sharpquote or a string"

Starting a REPL in Emacs is option-x nrepl-jack-in:

![nrepl-jack-in](/images/nrepl-jack-in.png)

This opens a terminal style call-and-response REPL, but once you have the REPL started then you can also execute forms directly off any .clj source code file.

Tip: `C-x <-`  (control x, then backwards arrow key) will return you to the previous page you were editing.  Because nrepl-jack-in just forwarded you to the call-and-response REPL.  Pretty essential basic Emacs navigation skill.

Type your code out, place the cursor anywhere inside the ( ) form and control-option-x (aka `M-C-x`):

![nrepl-execute](/images/nrepl-execute.png)

It flashes soothing deep violet and posts the results in the status area.

Writing unit tests is another great way to learn. You pose your problem, set up your test and fiddle about with your solution. The teacher grades you in milliseconds.  This is using the [Expectations](https://github.com/jaycfields/expectations) library and Emacs expectations-mode:

{% highlight clojure %}
(defn testme [x y]
  (+ y x))
{% endhighlight %}

Failing tests are shown highlighted on the page in firetruck red, so you know which ones you still have to fix.

![expectations-fail](/images/expectations-fail.png)

You can also run lein auto-expect which will re-run the tests whenever you save the source file.  Continuous testing is a true joy.

![expectations-console-failure](/images/expectations-console-failure.png)

## Emacs

Just a few starter notes about the setup I've started with.

After years of refusing to learn anything more about VIM other than :q! I did the unthinkable and switched to VIM.  I got pretty good at it too. Now ... I've switched to Emacs.  I still hit control-c a lot.  They are both great environments in different ways.  Using both at the same time is like soy sauce in milk.

On OS X [configure your option key](http://stackoverflow.com/questions/162896/emacs-on-mac-os-x-leopard-key-bindings) in Terminal/iTerm so that it sends Meta and then M-x means typing option-x.  C-M-x is then control-option-x

I had been using [http://vim.spf13.com/](VIM-SPF13) as a starter pack for VIM.

I'm now using the Emacs starter pack from:

[Emacs Live](https://github.com/overtone/emacs-live)

This is from the Overtone folks, so there are some music related things in there like supercollider syntax modes which you might not want, but it will get you all configured for general Clojure development.

This gives the colorschemes, paredit, clojure mode, and the latest trendy auto completes and whatnot.

These things are great to start with. You will run into annoyances. You will have unexplainable behavior.  I'm still not sure who is flashing that pink thing at me right now or how to toggle it.

![pink thing](/images/pink-thing.png)

But its often right, so I put up with the flashing.  Gradually I will take more command of my Emacs environment.

## Light Table

Light Table is another great way to learn Clojure. Its still in its early alpha days and has some bugs, but you could download it and start up a Clojure insta-REPL and be productive in minutes.  Development is moving along quickly and will support plugins and I would hope a lot of innovative ways to change what an IDE can do.

The killer feature for the learning phase is that you can see the results of your functions as you type and fiddle.  This virtually eliminates the code -> test -> debug cycle. Its now one single activity, not a cycle.  So experimentation results in a higher density of A-ha moments per session, and that's what learning is all about.

![lightable](/images/lighttable.png)

[Light Table](http://www.chris-granger.com/lighttable/)

But for real work its near impossible to beat a well set up Emacs environment.
