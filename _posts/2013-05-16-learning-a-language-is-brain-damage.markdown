---
layout: post
title: "Learning a language is brain damage"
published: true
---
I've been learning Clojure. Its a joy to use, but the shape and flow of Lisp forms takes some getting used to. Or put a another way, my brain needs to be loaded up with common constructs and patterns of usage before I can even read code without scrunching up my eyebrows.

Like learning a natural language, you have to learn the elementary constructions until there is no significant cognitive load.

I can literally feel the stress of not understanding something.  As I've learned in Yoga you want to maintain the right level of effort and learning.  Don't try 100%, you will only burn out faster. The brain doesn't learn well when its overloaded, nor when you don't challenge it enough. If you can't feel some cognitive stress then you need to dive in and challenge yourself more.

Last week this involved thinking:

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

You'll need to know if-let assoc get reduce.

Which means roughly:

reduce the array "text" using the function counter and initial value empty dict {}

{% highlight pseudocode %}
if-let means let c = maybe something
   and do this it is something
   and if it ain't then do this
{% endhighlight %}

Then I learn some tricks:

{% highlight clojure %}
;; simpler version
;; note get using a default value like python
(reduce #(assoc %1 %2 (inc (get %1 %2 0))) {} text)
{% endhighlight %}

Then I see somebody else solving it this way:

{% highlight clojure %}
;; merge maps using +
;; fn [val-in-result val-in-latter]
(apply merge-with + (map (fn [c] {c 1}) text))
;; this can work for streams too
{% endhighlight %}

This is a very clojuresque way of doing it.  For this you need to know about using apply and merge-with.  As he notes (it was a comment on a blog post and I can't find it now) you can use it with streams too for doing a running word count.

The next stage is knowing the core library enough that in the real world you would just use that:

{% highlight cloujure %}
;; clojure/core function
(frequencies text)
{% endhighlight %}

You don't want to jump too quickly into tangled lisp forms that seem like puzzles.  They only seem like puzzles.  Remember: at one time you probably thought a for loop looked odd.
