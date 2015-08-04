---
layout: topic
title:  "Implementation design"
abstract: "This is put just at an higher level than Java doc and shred light on design choices."
---

Couldn't gephi-toolkit be used in conjunction with js graph? [http://maurizzzio.github.io/greuler/](http://maurizzzio.github.io/greuler/)
Actually gephi-oolkit can be used for the algorithms it's shipped with while greuler would be a nice front-end. Unfortunately Jenkins can't run the JVM… but Clojure can be compiled to JavaScript :-) what a strong language ~~

So we could make something like this as an namespace-based architecture:

 * Input tool
  * Scanner (fits each and every input type and use lazy sequences. It's at the very frontground)
  * Lexer (from a raw row to sinograms IDS representation through a scanner)
  * Parser ()
 * Core (Contains the data itself, manipulate it, normalize it and make link with the graph-oriented database)
 * Export the whole database or excerpt of it in reduced or expended form (to js graph, gephi, txt, xml, image… can rely on gephi-toolkit)
  * One tool per export goal.

I could use this: [https://github.com/kawabata/ids-edit](https://github.com/kawabata/ids-edit) and the organisation to see how it looks into the set.

### Resulting structure

{% highlight HTML %}
.
├── COPYING
├── LICENSE
├── project.clj
└── src
    └── 華文
        ├── core.clj
        ├── export
        │   └── export.clj
        └── lexer
            ├── lexer.clj
            ├── parser
            │   └── strategies
            │       ├── chise
            │       │   └── strategy.clj
            │       └── kawabata
            │           └── strategy.clj
            ├── parser.clj
            └── scanner.clj
{% endhighlight %}

### Enlightened thoughts

Stored data will be of the reduced form:

 * Either the key is a radical, so the extent value length is 1;
 * Either it's n-fold then the extend value length is n and we know IDC can not be more than threefold thus 1 ≤ n ≤ 3.

What about the key? Chinese character set doesn't span over the whole IDS universe.

I've found a context-free-grammar-based parser builder on GitHub (github.com/Engelberg/instaparse) then now my main goal is to define a gramar for Chinese language ;-)

I want labelled syntax tree isn't it? just like resultant tree but with labels where it's possible.

### Readings

To build up this new implementation, I read these books: « Clojure for the brave and true », « Introduction to Automata Theory », « Languages, and Computations », « Living Clojure »

### About regular expressions

These following regular expressions can be very helpful for building a formal grammar:

{% highlight Clojure %}
(re-seq #"\p{InIdeographic_Description_Characters}" "aA1¬→⿱七")
; => ("⿱")
(re-seq #"\p{L}" "aA1¬→⿱.𫝕𬹁𫥇")
; => ("a" "A" "𫝕")
{% endhighlight %}

As can be seen, \p{L} doesn't fully support ideographs. But it may suffice to enter full range of unicode blocks to solve this problem.

### Parser levels

The role of a parser is to take raw data and to output some intelligible by a software. It thus have several levels:

 * Level 0 accesses physical data, that's to say the filesystem. This level only takes a location as single parameter. It gives a way to access each data row.
 * Level 1 presents raw data. It take as single parameter a description of the source format. This description is used to populate the output map. It splits a row into a map which will be later parsed. This map may have keywords like :ids, :codepoint, :letter. Here, :letter means letter of the alphabet. The description taken as parameter can thereby map each keyword to a column index. If there are several <small>IDS</small> variants, :ids will be mapped to a vector. If there is just one string then :ids will map to it.
 * Level 2 parses the <small>IDS</small>. Thus is uses the official <small>IDS</small> grammar.
 * Level 3 no longer belongs to the parser only but can be included into the lexer: we know have manipulable data so we want to manipulate them to construct a graph. From this level and above, we should deal with versions and prepare the data structure for queries.

Then, as the graph has now been constructed, we can query it. This is something else but it would still need a grammar to form a domain-specific language. It sure will be very interesting to design such a grammar. It reminds me somethnig like <small>XML</small> queries. Maybe I could get inspired by grep as in an article I read.

### Grammar types

At least three kinds of context-free grammars will be used in this project:

 * The first one (the most simple) is for level 1 to parse strings which contain variants to formal <small>IDS</small>. 
 * The second one (the most show-off: «hey buddy, I've defined my own grammar for the whole Chinese language!») is used in level 2 to parse <small>IDS</small>.
 * The last one (the most interesting) will appear in the query engine to define its language.
 * Finally, we can add another grammar, at an higher level than previous ones. Such high-order grammar will be real Chinese grammar, for example used <small>NLP</small>.

Reading « Introduction to Automata Theory, Languages, and Computations » from H<small>OPPCROFT</small>, M<small>OTWANI</small> and U<small>LLMAN</small> may seem just academic duty but I surely will benefit from all this theory so I must keep on! ~
