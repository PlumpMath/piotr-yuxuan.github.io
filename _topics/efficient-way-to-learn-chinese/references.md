---
layout: topic
title:  "Solving Clojure cross-file references within the REPL (in Cider on Emacs)"
abstract: "Cross-files references in Clojure"
---

I've come to be lead by domain-driven design to change the architecture of an existing code to put altogether in the same namespace functions which lay in the same semantic field. However, now I'm stuck because of the kind of cross-file references examplified by the three following files `file[A-C]`.

How do veteran clojurists deal with this kind of reference issue? furthermore, what's most common way to define namespace: should they naturally be domain-driven?

I'm using Emacs with Cider but I believe this problem is quite common and doesn't depend on which software you create your code with.

File A:

{% highlight Clojure %}
(ns root.fileA
  (:use clojure.test)
  (:require [root.fileB :refer [funcB1]])
  (:require [root.fileC :refer [funcC1 funcC2]]))
  
  (declare funcA1)
{% endhighlight %}

File B:

{% highlight Clojure %}
(ns root.fileB
  (:use clojure.test)
  (:require [root.fileA :refer [funcA1]])
  (:require [root.fileC :refer [funcC1 funcC3]]))
  
  (declare funcB1 funcB2)
{% endhighlight %}

File C:

{% highlight Clojure %}
(ns root.fileC
  (:use clojure.test)
  (:require [root.fileA :refer [funcA1]])
  (:require [root.fileB :refer [funcB1 funcB2]]))
  
  (declare funcC1 funcC2 funcC3)
{% endhighlight %}

