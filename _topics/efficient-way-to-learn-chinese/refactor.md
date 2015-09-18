---
layout: topic
title:  "How to refactor with Emacs as well as in a newer IDE"
abstract: "This is put just at an higher level than Java doc and shred light on design choices."
---

If you have been using Emacs for a long time, it's pretty likely you've faced refactoring projects with more than a couple of functions spread over two or three files. I come from IntelliJ and I've used to be pretty stuned by their refactoring tool. It makes almost code a vivid set of biological cells you can manipulate to construct the body you want.

However, as a newbie, I don't know yet how to achieve (at least) basic refactoring with Emacs:

* How to change the name of a symbol thorough the whole code base?
* How to move symbols over files and get references automatically updated?

I'm working out Clojure on Emacs with Cider. After a first code shot I've been willing to give it a proper shape… and that's terrible it's like I have to care every single detail by hand. It would finally take me the same amount of time to write that first shot than to arrange it. Sure you can tell me I should have thought more before start writing, but I changed my mind a lot and now I need to repack things – basically I'm doing Agile development ~
