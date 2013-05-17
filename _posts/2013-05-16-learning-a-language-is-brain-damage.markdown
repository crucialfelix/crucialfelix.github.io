---
layout: post
title: "Learning a language is like brain damage"
published: true
---

As of late I've been learning Clojure. Its a joy to use, the brevity and feeling of encapsulating power is splendid, but the shape and flow of Lisp forms takes some getting used to.  "Reading Lisp forms" is a practice that needs to be practiced.

So first my brain needs to be loaded up with all these common constructs and patterns of usage.  Alien things that need to be consumed till they are taken for granted.  In a way this is brain damage - your habit mind knows one pathway, and you are asking it to behave in an alien fashion.

Asking yourself to change is always a form of self-abnegation.  You are often telling yourself that you are wrong, that you don't get it, that "you" are somehow deficient. This is a fallacy based on self-identifying with your knowledge and your habits. You are not your habits. You are not your memories. You are not your fucking Khakis etc.  All these things are mutable &mdash; unlike Clojure data structures.

Of course its not actually brain damage.  In fact learning (natural) languages has been shown to increase the size of the hippocamus, increase synapse connections leading to a "bigger brain" (will I need to purchase a new casing soon?)

The stress of writing new pathways just feels like brain damange.  I can even feel the physical sensation as my brain squirms around trying to put (+ 2 2) together.  Possibly its also the challenge to your self esteem.  "You" don't know this, "you" suck.

I've found that in periods in my life where I had a very quiet non-invasive ego that I learned much faster. I felt more intelligent and I solved problems easier.  Being hung up on the personal cartoon character is like having a rogue process.  You need to shut it down or quiet it down, and then the system runs much smoother.  Being self-judgemental is useless.

Keep the level of challenge high, keep out of overload.  Don't gorge on information (I do that a lot), keep calm, keep in the REPL, keep writing, screwing up, scraping your knee; keep encountering things you don't know and working them until they feel familiar.

A few weeks ago when I first started out, this involved thinking in order to read it:

{% highlight clojure %}
;; count the number of occurences of each letter
(def text "aabbckckekfijsleijflijseflijfzzaa")

;; my first version
(defn counter [map val]
  (println val map)
  (if-let [c (get map val)]
    (assoc map val (inc c))
    (assoc map val 1)))

(reduce counter {} text)
;; =>  {a 2,b 2, c 2, e 3, f 4, i 4, j 4, k 3, l 3, s 2, z 1}
{% endhighlight %}

Now it looks self-explanatory to me.

Which means roughly:

reduce the array "text" using the function counter and initial value empty dict {}

You'll need to know basics like [if-let](http://clojuredocs.org/clojure_core/clojure.core/if-let) [assoc](http://clojuredocs.org/clojure_core/clojure.core/assoc) [get](http://clojuredocs.org/clojure_core/clojure.core/get) [reduce](http://clojuredocs.org/clojure_core/clojure.core/reduce).

{% highlight pseudocode %}
if-let means let c = maybe something
   and do this it is something
   and if it ain't then do this
{% endhighlight %}

Then I learn some tricks:

{% highlight clojure %}
;; simpler version
;; note the use of get with a default value like python
(reduce #(assoc %1 %2 (inc (get %1 %2 0))) {} text)
{% endhighlight %}

Then I see somebody else solving it this way:

{% highlight clojure %}
;; merge maps using +
;; fn [val-in-result val-in-latter]
(apply merge-with + (map (fn [c] {c 1}) text))
;; this can work for streams too
{% endhighlight %}

This is a very clojuresque way of doing it.  For this you need to know about using apply and merge-with.

The next stage is knowing the core library enough that in the real world you would just use that:

{% highlight cloujure %}
;; clojure/core function
(frequencies text)
{% endhighlight %}

These examples are from [this post](http://twoguysarguing.wordpress.com/2010/07/26/7-rules-for-writing-clojure-programs/).  Note that he got all embarassed when others pointed out better ways of doing it.  But the post was useful, the learning process was useful and the discussion was very useful.

Shame is a rogue process.  Relax and consume the alien.
