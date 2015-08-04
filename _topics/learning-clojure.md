---
title: "Learning Clo<i>j</i>ure"
layout: topic
index: true
changefreq: daily
abstract_html: "<p>The print of my path from vain thoughts through darkness to Clo<i>j</i>ure.</p>"
---

## Learning Clo<i>j</i>ure

The more I learn about Clo<i>j</i>ure, the more I feel I never knew what « being a developer » truly means before. Functionnal paradigm is so very powerful! Clo<i>j</i>ure is beautiful. It demands a very fresh new mindset I've never been taught before. I believe all computer students should start to code within the functional frame. Then, if they prefer, they could downgrade their mind to model-driven, actor-, object- or even imperative-oriented programming.

* TOC
{:toc}

### <small>GNU</small> Emacs key bindings

Emacs is a wonderful tool but one who is willing to get help from it must first accept using a wiser, more powerful… and older-that-them tool. Here is a short cheat sheet to help me get emacs not disturb me too much. I'll let her unleash her magic when I'll be wiser!

* Buffers and frames
	* `C-x 1` Delete all other windows, leaving only the current window in the
	frame. This doesn’t close your buffers, and it won’t cause you to lose
	any work.
	* `C-x 2` Split frame above and below.
	* `C-x 3` Split frame side by side.
	* `C-x 0` Delete current window.
	* `C-x b` Open a buffer.
	* `C-x C-f` Create a buffer for a file.
	* `C-x C-e` Send the expression immediately preceding point to the <small>REPL</small>, which then evaluates the expression.
	* `C-u C-x C-e` Print the result of the evaluation after point.
	* `C-c M-n` Set the namespace to the namespace listed at the top of the current buffered file.
* Clo<i>j</i>ure-mode
	* `C-c C-k` Kompile the `*.clj` to the <small>REPL</small>. Sounds German because it was created by the Nazi during <small>WWII</small>[^1].
	* `M-x cider*` connect to an exisiting <small>REPL</small>, create a new one, interrupt, quit…
	* `C →` or `C ←` Change how a pair of parens spans over the data.
	* `M ↓` or `M ↑` Lead to disaster
* Cider
	* `C-enter` Close parentheses and evaluate
* Region and expression
	* `C-x C-e` Evaluate the afore region.
	* Evaluate the selected snippet.
	* `C-w` Kill a region.
        * `C-y` Yank a region.
	* `C-x C-k` ?
	* Browse over yank ring.
	* Yank a region.

### Gists

What would it look like in Java?

{% highlight Clojure %}
(defn clean
	[text]
	(reduce (fn [string string-fn] (string-fn string))
		text
		[s/trim #(s/replace % #"lol" "LOL")]))
{% endhighlight %}

First, in Java 8 we can mimmic functionnal programming and iterate through an array of functional interface implementations. Why not. But how creepy this sounds compared to Clo<i>j</i>ure style: « iterate through a list of functions »!

### Links to read

* [http://en.wikipedia.org/wiki/Tail_call](http://en.wikipedia.org/wiki/Tail_call)
* [http://hypirion.com/musings/understanding-persistent-vector-pt-1](http://hypirion.com/musings/understanding-persistent-vector-pt-1)

### Personnal pack

I'd like to change `clojure-pack` a bit so it could display $$∧$$ (and), $$∨$$ (or), $$∃$$ (Polish notation exists symbol), $$¬$$ (Polish notation not symbol), $$∘$$ (function composition).

### Exercices

Some exercices lay in a [dedicated repository](https://www.github.com/{{ site.links.github | append: "/clojure-for-a-newbie" }}).

---
[^1]: This is bad joke: I acknowledge German people must be distinguished from Nazi ideology.

