---
layout: topic
title:  "Implementation design"
abstract: "This is put just at an higher level than Java doc and shred light on design choices."
---

You can find a table of content at the bottom.

## Readings

To build up this new implementation, I read these books: « Clojure for
the brave and true », « Introduction to Automata Theory », « Languages,
and Computations », « Living Clojure »

Reading « Introduction to Automata Theory, Languages, and Computations »
from H<small>OPPCROFT</small>, M<small>OTWANI</small> and
U<small>LLMAN</small> may seem just academic duty but I surely will
benefit from all this theory so I must keep on! ~

## About regular expressions

These following regular expressions can be very helpful for building a
formal grammar:

{% highlight Clojure %}
(re-seq #"\p{InIdeographic_Description_Characters}" "aA1¬→⿱七")
; => ("⿱")
(re-seq #"\p{L}" "aA1¬→⿱.𫝕𬹁𫥇")
; => ("a" "A" "𫝕")
{% endhighlight %}

As can be seen, `\p{L}` doesn't fully support ideographs. But it may
suffice to enter full range of unicode blocks to solve this problem.
However, reguler expression only dealswith text so a ranges have to be
dealt with accordingly (see char-pattern namespace).

{% highlight Clojure %}
(def negative-grammar
  (insta/parser
   (let [kernel "&(U\\+|CDP\\-)[0-9a-zA-Z]+;"]
     (str "<S> = (Letter | Else)*"
          "Letter = " (print-str (re-pattern (str "^(?!" kernel "$).")))
          "Else = " (print-str (re-pattern (str #"" kernel "")))))))
{% endhighlight %}

This is an suggestion to retrieve strings that match *not* a pattern.

## Parser levels

The role of a parser is to take raw data and to output something
intelligible by a software. It thus have several levels. For each level
we should check the file processing to catch and remove errors.

-   Level 0 accesses physical data, that's to say the filesystem. This
    level only takes a location as single parameter. It gives a way to
    access each data row.
-   Level 1 presents raw data. It take as single parameter a description
    of the source format. This description is used to populate the
    output map. It splits a row into a map which will be later parsed.
    This map may have keywords like :ids, :codepoint, :letter. Here,
    :letter means letter of the alphabet. The description taken as
    parameter can thereby map each keyword to a column index. If there
    are several <small>IDS</small> variants, :ids will be mapped to a
    vector. If there is just one string then :ids will map to it.
-   Level 2 parses the <small>IDS</small>. Thus is uses the officially
    specified <small>IDS</small> grammar.
-   Level 3 no longer belongs to the parser only but can be included
    into the lexer: we know have manipulable data so we want to
    manipulate them to construct a graph. From this level and above, we
    should deal with versions and prepare the data structure for
    queries.

Then, as the graph has now been constructed, we can query it. This is
something else but it would still need a grammar to form a
domain-specific language. It sure will be very interesting to design
such a grammar. It reminds me somethnig like <small>XML</small> queries.
Maybe I could get inspired by grep as in an article I read.

## Grammar types

I use this context-free-grammar-based [parser
builder](github.com/Engelberg/instaparse) to define grammar in a
theoretic way.

At least three kinds of context-free grammars will be used in this
project:

-   The first one (the most simple) is for level 1 to parse strings
    which contain variants to formal <small>IDS</small>.
-   The second one (the most show-off: «hey buddy, I've defined my own
    grammar for the whole Chinese language!») is used in level 2 to
    parse <small>IDS</small>.
-   The last one (the most interesting) will appear in the query engine
    to define its language.
-   Finally, we can add another grammar, at an higher level than
    previous ones. Such high-order grammar will be real Chinese grammar,
    for example used <small>NLP</small>.

## Overcoming Java flaws

The JVM comes with a big flaw: character are encoded in 16 bits. This
means only the BMP can be directly addressed and semalessly used. To
overcome this painful limitation, we provide several functions to escape
Chinese characters. It's pretty straightforward but one have to keep in
mind we must be able to use explicit characters like 𠆢 (which doesn't
belong to the BMP), escaped explicit characters (𠆢 becomes &U+201A2;)
and escaped CDP characters (like &CDP-8C42;).

Basically, it will change the way letters are defined in the grammar
definitions and all functions will natively assume they have to deal
with espaced characters. Functions with side-effect will allow us to get
back to the « real Chinese » world and the few remaining limitation will
be the font to display glyphs.

## About purity

I believe I should try to keep functions perfectly pure. However, some
data are constants across the whole project and are not meant to change
once they're defined, as for Unicode block range definitions. I'm still
puzzle about how I should properly handle this and currently use ad-hoc
policy but I should get it cleaner.

Maybe it would be a good practice to write ony pure closures. Thus once
we need it, we set closures we want then we seamlessly use them. It
would avoid parameter inflation and it's likely to keep the code more
understandable but will add some more (let) form.

## Domain-driven architecture

Emacs is fun to use because it's a beautiful piece of software but I'm
not very well used yet to Emacs thus I don't know yet how to click on a
symbol to jump to its definition, to refactor properly the name of a
symbol or how to have a correct autocompletion feature. This push me to
strengthen the structure of my code to help my development process and
not to waste too much time on implementing the same wheel again and
again across the same files.

Here is the namespace I foresee to be useful perchance, based on
existing code:

### 華文 core

First of all, `core` is empty as I have nothing to put in yet. I could
yet add code to use existing code and parse expressions but I consider
my current work as widely unfinished so this would be pointless.

Core could contains the data itself, manipulate it, normalize it and
make link with the graph-oriented database. I could use this:
<https://github.com/kawabata/ids-edit> and the organisation to see how
it looks into the set.

### Worker namespaces

The current three namespaces `manipulation.{char,struct,regeces}` are to
be respectively renamed and put under a single `manipulation` namespace:
`char`, `struct` and `regeces`. They should host only pure, simple
functions.

### Range regular expressions pattern

`regeces` allows to seamlessly deal with range of integers and overcome
regular expression all-char-string policy. It exposes following public
functions:

-   `dec-to-hex` and `hex-to-dec` respectively convert a number into a
    string-stored hexadecimal representation and vice-versa.
-   `pow` is the mathematical power. This should be packed in some
    algebraic-specific namespace but I currently to few similar
    functions to put in.
-   `range-pattern-from-hex` is the prominent function of this
    namespace. It takes two strings representing hex-formatted numbers
    and returns a pattern which matches all numbers in the range
    (including the borders). It may be renamed `range.to-pattern` as a
    more direct formulation.

`pow`, `dec-to-hex` and `hex-to-dec` can be made private if they are
solely used in this namespace.

### Character manipulation

`char` is about characters manipulation. It defines both vars and
functions. The most prominent var is `definitions`, talked about below.
I'm very bothered by how to handle properly with these vars: they are
perfectly static and immutable so are they used in an idiomatic way;
however where should I put them? they're likely to be used throughought
the namespaces. As a result, I will move all vars into propers
sub-namespaces of some `consts` ones. This will result in more purity so
I gullibly believe it can't hurt.

-   `token-to-codepoint` expects a string containing a single token.
    Whatever explicit or escaped the token will be given, this function
    returns the codepoint. Beware it will return `U+201A2` for example
    and not `&U+201A2;`.
-   `escape-token` expects a string containing a single token, already
    escaped or still explicit, and returns its escaped counterpart. It
    doesn't accept codepoint, only a token.
-   `select-regeces` is to be given some parameters but actually does a
    simple thing: it returns a filtered set of regular expressions. This
    functions takes three arguments only for it's pure.
-   `aggregate-regeces` is a bastard unpure, underoptimised functions
    which do great job however. We should thank her and turn it into a
    more noble form. As the name suggest, it unify regular expressions
    into a single one whose solution space is the union of the
    aforementionned regeces.
-   `select-escape-token` only escape the token it's given if it matches
    any of the rules defined. It means you can apply it with a (map)
    form to a vector of tokens to escape characters which matching only
    some specific rules and let other untouched.
-   `deref-codepoint` takes a codepoint and outputs a token. This token
    will be in explicit form whenever possible, or will be escaped.
-   `deref-escaped` takes an escaped token and returns its explicit form
    whenever possible. I should make it a bit more symmetric and change
    it to let it accept any form of tokens.
-   `print-rules` has been given a misleading name as it does output
    nothing. The name is made in the same fashion of `print-str`. As
    suggested, it takes parameters and construct a string which
    represents the induced rules. This string can be processed by formal
    grammar.
-   `definitions` is built on the top of this namespace. It may
    unconsistent to keep it in this namespace about characters because
    it defines radical definitions for grammars. However, where to put
    it is a subtle question.
-   `block-ranges` defines Unicode block ranges.

This functions are a vivid mess we could clean by summing it up into the
following function set:

-   `char.token.escape` and `char.token.deref`. `char.token.escape`
    accepts 1 argument (the token to escape) or 2 to have add a
    condition. If two arguments, you will give it the token to be
    escaped and the test it must pass. This test can be a regular
    expression or a function which will take only one parameter and
    return false or nil if the token doesn't fulfill it.
-   `definitions` and `block-ranges` to be moved to `consts` namespace.
-   `block-ranges` is to be renamed `unicode-blocks`.
-   `select-regeces` and `aggregate-regeces` may be moved to `regeces`
    to increase consistency.
-   `print-rules` will be moved to `consts` as a private function.
-   `deref-codepoint` has no sense but should be something like `deref-codepoint`.
-   We add new function `codepoint` which take a parameter to say the direction: from codepoint or to codepoint?

### <small>IDS</small> and trees

`struct` uses the two aforementionned namespaces, hence `char` and
`range`, to offer functions about manipulate structures (IDS or tree).

-   `deref-tree` takes a tree (well, actually it's a list containing one
    vector composed of nested vectors) and turns tokens to explicit form
    by applying `deref-escaped` when possible.
-   `escape-tree-set` takes a tree of tokens of any forms and returns a
    set of its tokens. As for a set, order is lost. I could perhaps
    change it to return a vector which would preserve order as it may be
    easier to build back the <small>IDS</small> from the latter.
    Actually this function doesn't not escape any character so its name
    is misleading. It just flatten a tree to an set.
-   `tokens-from-string` splits a string into tokens. However this
    function has regular expressions as supplemental arguments which
    tell it what is a token or what isn't.
-   `tree-to-ids` takes a tree and flatten it into an
    <small>IDS</small>.
-   `escape-ids-set` is given an <small>IDS</small> and drops a set of
    its elements (both structure and Chinese characters).
-   `ids-token-set` is fed of an <small>IDS</small> and gives back a set
    of its tokens.
-   `escaped-lexer` turns an <small>IDS</small> into a tree of
    exclusively escaped tokens. However this function is not pure at all
    because it relies on a grammar made of aforementionned
    `definitions`.
-   `ids-to-tree` behaves in a rather similar way but returns a tree of
    explicit tokens whenever it's possible. However it should be better
    to merge `escaped-lexer` and `ids-to-tree` to a same function. Here
    three implementations are possible:
    -   Either this function takes a new parameter which tells it which
        token form it should return;
    -   Either this function does it job then crawl the original
        <small>IDS</small> and check each tree token has the same
        original form;
    -   A more elegant design would remember side-effect are to be
        prohibited from functions, then we should only return escaped
        form because those functions are said to mostly deal with this
        form.

As we can see, features of this namespace can be classified on a
three-dimension basis:

-   Does it takes a tree or an <small>IDS</small> an input?
-   Does it output an <small>IDS</small>, a tree or a set?
-   Does we know anything about the output form?

So it would be more explicit to have the following set of functions
(prefixed by the namespace):

-   `struct.deref` and `struct.escape` would accept both string or
    collection (including vectors, set and nested collections) and would
    be built upon private functions. Well, actually we don't care about
    this, this is just for side-effect functions.
-   `struct.process-to` is a powerful function. Well, Keep It Simple
    Stupid philosophy would disagree with such a function but I believe
    it can make the code easy to understand. This function would wrap
    translation functions such as `{ids,tree}-to{tree,ids,set}`. This
    function itself can take several arguments such as a grammar or
    character ranges but returns a well-fit closure which accepts two
    parameters: 1) a keyword which refers to the destination data
    structure and 2) the structure to operate on. For example, if we
    call `turn-into` the resulting closure, we can have
    `(turn-into :set original-collection)`.

### Immutable data

The namespace `consts` has been defined whilst I was writing the text above.
It's to host definitions which are not to be changed on a regular pace
across the program. It may be poorly designed but currently it's still
an improvement because it helps purity functions. It's currently made of
the following:

-   `definitions` is a string to be appended at the end of formal
    grammars. It contains rules.
-   `print-rules` is private function used to produce string out of
    regular expressions. This production will later be added to
    `definitions`.
-   `block-ranges` is to be renamed `unicode-blocks`.

### Side-effect functions and interaction with the real world

Pure functions should have no side-effect, hence display nothing. I
prefer to have some side-effect to make some useful program ^\_^ so in
the namespace `side-effect`, function are still pure *except* they display stuff. I
could also need to set some vars as in imperative paradigm to keep track
of the user choices. Actually this is not automatically a turn to the
Evil side! Indeed, user choices has said static and immutable whilst a
program is running.

-   `struct.deref` and `struct.escape` would accept both string or
    collection (including vectors, set and nested collections) and would
    be built upon private functions. They will ensure data are escaped
    as soon as possible before to be processed. They ill accordingly be
    renamed into `side-effect.deref` or `side-effect.escape`.

Couldn't gephi-toolkit be used in conjunction with js graph?
<http://maurizzzio.github.io/greuler/>. Actually gephi-oolkit can be
used for the algorithms it's shipped with while greuler would be a nice
front-end. Unfortunately Jenkins can't run the JVM… but Clojure can be
compiled to JavaScript :-) what a strong language ~~

### About `consts` and `side-effect`

Those two namespaces might be contested as other designs may get rid of
them. I'm truely open to anything new and merely want to produce the
best first Clojure project I can. If you think I've missed something
special, just tell me. However, those two namespaces contain few stuff
(by the time being) then from my viewpoint it makes it likely to be in
accordance with functionnal paradigm.

### Parsers

`parser` hosts parsers which could be made for several data sources. I
currently have only one, entitled `kawabata` after the maintainer of the
repository I got ids listing in. Actually I should hail Kawabata-san
somewhere and rename this parser Chise to make it more general.

At least all parsers should expose the following three functions:
`level-[0-2]`. Each of these functions returns a closure which
implements formerly described behaviours (cf. § Parser levels). I don't
know to use inheritance mechanism in Clojure but it may be nice to try
:-)

#### Chise parser

`parser.chise` is a child namespace of `parser`. Apart from the three
levels, it contains nothing worth of interest, except perhaps
assoc-one-by-one which should be moved to some helper namespace.

### Lexer

As we are not dead, stabilised project ready to be used yet but still
vivid, playful code, lexer explicitly binds its `level-[0-2]` functions
to chise's. Lexer levels eventually act like defined in § Parser levels.
Besides them, you also find several functions.

-   `harden` function is used to crawl throughout the database and check
    whether all data can be processed.
-   `export-graph` reduce a specified data structure into a character
    string to be exported in a graph processing tool. This should be
    moved to `side-effect`.

## Resulting architecture

This paragraph presents current feature sharing amongst namespaces. Space names are in __bold__ font, functions in regular shape and immutable datas are in italics.

* __華文__
	* __core__
		* -main
	* __manipulation__
		* __char__
			* token
				* codepoint
				* some missing :/
		* __struct__
			* deref
			* escape
			* process-to
		* __regeces__
			* dec-to-hex
			* hex-to-dec
			* pow
			* to-pattern
			* select
			* aggregate
	* __consts__
		* *definitions*
		* *unicode-blocks*
		* *print-rules*
		* *code-escape*
		* *prefix-u*
		* *prefix-cdp*
		* *prefix*
		* *code-body*
		* *code-end-escape*
		* *re-codepoint*
	* __side-effect__
		* deref
		* escape
		* export-graph
	* __parsers__
		* __chise__
			* level-0
			* level-1
			* level-2
	* __lexer__
		* harden

## Polymorphism and other stuff I must know

I will replace test on type by the use of multimethod.

To flatten a structure, I will use flatten partition-by is a powerful
tool for some need.

When this project will be advanced enough, I will try to define some macro.

## Table of content

* TOC
{:toc}
