---
title: "華文: an efficient way to learn Chinese"
layout: page
collection: topics
changefreq: daily
abstract_html: "<p>Chinese language is not like most of Western languages: a sinogram like 貴 can be meaningful by its own whereas Western <i>z</i> means nothing by itself. Chinese is a very different thus very interesting language. What's the most efficient way to learn characters?</p><p>The rational way may be to learn components before compounds. Given that, the most efficient way may be to order Chinese character by frequency. We initially focus on a single sinogram sructure and then broaden the scope to sinogram composition directed network. We further foresee how to crawl it and retrieve data from it.</p>"
---

That page doesn't contain programmatical details about that project – see the [git repository](https://www.github.com/{{ site.links.github | append: "/chinese-huawen" }}) if you're willing to give them a glance. If reading bores you, watch to [some pictures](https://www.github.com/{{ site.links.github | append: "/chinese-huawen" | append: "/tree/master/gephi" }}) of what I've currently got ☺

> The first character 華 of the project name means sinity; 文 stands for language. The whole phrase 華文 means _Chinese language_ and is read ㄏㄨㄚˊ ㄨㄣˊ or huáwén.

* TOC
{:toc}

## What's the most efficient way to learn Chinese?

Chinese language is not like most of Western languages: a Chinese character like 貴 can be meaningful by its own whereas Western _z_ means nothing by itself. Chinese is a very different thus very interesting language.

Most of Chinese handbooks are built in a Western fashion: daily-life conversation samples bring new vocabulary and syntax examples. This fashion doesn't take advantage of intrinsic Chinese language structure, which makes easier to discover 貴 when knowing yet 中, 一 and 貝. 貴 stands for expensive or honourable while 貝 refers to shell or money. This semantic link lets it easy to remember both of them. The rational way to learn Chinese may be to learn components before compounds. Given that, the most efficient way may be to order Chinese character by frequency.

That page extends the previous example and widen its scope step by step. We initially focus on a single sinogram sructure and then broaden the scope to sinogram composition directed network. We further foresee how to crawl it and retrieve data from it.

## Sinogram structure

We compare Western and Chinese languages. How do they form new words? Chinese etymology is reachable in most case by just giving a look to the word. This etymology can be described with description sequence. However, some times it's more difficult because a character has a different shape: this is the sinogram variants problem. Finally, we imagine what could be a good Chinese learning order and why it matters.

### Etymology

An English word is made with letters, thanks captain Obvious! As seen previously, letters like _e_, _b_ do mean nothing (in main case) by their own. You need to put letters together to get meaning: _be_. You can combine old words from antique languages to make a new one whose meaning can be guessed by its etymology _kilo_ and _metre_ give you kilometre. Sometimes the components are changed: _altogether_ comes from _all_ and an old English noun _tōgædere_, sometimes they are not: _aforesaid_ come from _afore_ and _said_.

Chinese is build the same way with a tiny difference: where Western characters (letters) don't mean anything, Eastern characters (sinogram) are yet [semes](https://en.wikipedia.org/wiki/Seme_%28semantics%29). To make it clear, sinograms are at the same level of Western [etymons](http://en.wiktionary.org/wiki/etymon). Western letters can be compared to Eastern strokes. Thus _a_, _aa_ and _aaa_ can't be understood whilst 木, 林 and 森 mean tree, grove of trees and forest. Chinese etymology is very strong!

### Description sequence

The structure of a sinogram gives a lot of information about its etymology. Like English, most of sinograms don't visually change a lot when they're used as etymons (or components): 中, 一 and 貝 automatically gives 貴 which is described by the following [Ideographic Description Sequence (<small>IDS</small>)](https://en.wikipedia.org/wiki/Chinese_character_description_languages#Ideographic_Description_Sequences): ⿳中一貝. The first character, ⿳, is an [Ideographic Description Character (<small>IDC</small>)](http://www.unicode.org/versions/Unicode6.0.0/ch12.pdf). Those characters are used to described sinogram structure. There are twelve ways to compose sinograms so there are accordingly twelve characters: ⿰, ⿱, ⿲, ⿳, ⿴, ⿵, ⿶, ⿷, ⿸, ⿹, ⿺ and ⿻. Such an <small>IDC</small> can be seen as an operator whose arity can be 2 or 3.

Let us see another example. The sinogram 灣 can be described by the following equivalent sequences: 

 * 灣 (yes it's a sequence – yet minimal – for the sake of consistency);
 * ⿰氵彎 (normalized decomposition, there are the fewest characters possible):
 * ⿰氵⿱⿲⿱幺小言⿱幺小弓 (unfold decomposition to radical).

Extended <small>IDS</small> format has also been introduced to build a [structural query system](https://github.com/piotr2b/chinese-huawen/blob/master/bibliography/A%20Structural%20Query%20System%20for%20Han%20Characters.pdf) for sinograms.

However, Unicode hasn't been the first to struggle to encode sinograms. Researchers from Academia Sinica have published an [explanation to handle unencoded sinograms](http://cscl.iis.sinica.edu.tw/cscl/Publication/ICDAT04-WebICS.pdf) by composing them. Their composition system is rather interesting but lacks free and available decomposition data sources. Moreover, I can't figure out how they did encode symbols for their equivalent <small>IDC</small> so I can sadly even not type them.

Those decompositions don't go to stroke scale. For instance, the unfold decomposition of 灣 doen't break 小 down. Such "ending" sinograms are called radicals and are used to sort sinograms à la Western lexicographic order. A de facto standard is the [214 Kangxi radical set](https://en.wikipedia.org/wiki/Kangxi_radical). Other decompositions (such like [Wenlin's Character Description Language](http://www.wenlin.com/cdl/)) go straight to strokes. We'll keep to Unicode <small>IDS</small>.

### Sinogram variants

Besides that smooth way to compose Chinese characters, some change quite a lot. 部 is visually made of 咅 and ⻏ but the latter sinogram ⻏ is a variant of 邑. To make things more awkward, ⻏ refers to 邑 when put on the right side of the compound sinogram but refers to 阜 on its left. Different versions of a same abstract character are called variants. Variants also depends on the exogen factors just like English language sometimes differs depending on speaker culture or citizenship. I've chosen in previous examples to talk about _kilometre_ but American English spells it _kilometer_. In the same process, sinogram glyphs can be slightly different for Japanese, Korean or Chinese languages. it's even the mess in Chinese language itself where can be found simplified and traditionnal ways to write one sinogram.

There is no one-to-one link with variants, even not one-to-many. So variation patterns can be rather complex and involve many-to-many links. Variants are properly defined in a [report by the Unicode consortium](http://www.unicode.org/reports/tr38/#N10211).

### Learning order

We could early guess at this point that it may be interesting to learn etymons before compound sinograms to make the latter both easier to understand and remember. This process can be compared with Spanish. You can learn it only and no other languages else but it's so much easier to learn it when you already know Latin! Moreover, you need to know Latin to understand deeply that language. Anyway, would you learn both Latin and Spanish before going to Spain in vacations? Sure not, because it implies a bigger workload. This is different from Chinese because the Chinese language is more than three-thousand-year old thus uses its own old words as etymons and doesn't need older previous languages – actually Chinese is the main first Asian written language. To put it in a nutshell, learning order counts for Chinese far more than for Western languages.

## Sinogram set structure

We can put sinograms together and use the composition relation to build several graph structures, comment them and explain how we move from one to another to get an higher abstraction. We discuss the structure of the sinogram set. We further define the sinogram frequency in two ways, geographically and graph-theoretically. We also sketch some ways to draw such graphs.

### Math-free summary

We use the composition relation to build a composition network and we rise an open question about the structure of the sinogram set. We further distinguish between two definitions for sinogram frequency. Finally, the more frequent is a sinogram, the closer it is to the centre of the network.

### Definition of the composition relation

Let's define the set $$\mathbb{S}$$ of existing sinograms. This is a finite but still growing set. It's a subset of the infinite thus bigger universe set $$\mathbb{U}$$ of all possible sinograms.

We've seen that sinograms can be broken down in smaller ones, called components. Those components enclose etymology and convey meaning. Composition relation $$\mathcal{R}$$ is a partial order relation on $$\mathbb{S}$$ whith these main properties:

 * Reflexive: $$x$$ is a component of itself. This is interesting to say a single sinogram can be a valid <small>IDS</small>. Moreover <small>IDC</small> has arities from 2 to 3 so if $$x$$ is not a component of itself we can't represent a radical <small>IDS</small>. This is why we choose to have not a strict partial order relation (when it's irreflexive) ;
 * Antisymmetric: $$x$$ is a component of $$y$$ and $$y$$ a component of $$x$$ if and only if $$x = y$$ (it's possible because it's reflexive); 
 * Transitivity: $$x$$ is a component of $$y$$ and $$y$$ a component of $$z$$ if and only if $$x$$ is a component of $$z$$. If $$x$$ is a component of $$z$$ with no third distinct sinogram $$y$$ between them, we say $$x$$ is a nearest component of $$z$$. Else we call $$x$$ a far component of $$z$$.

We can also find minor properties:

 * Serial: for all $$x$$ we can find one component or more (at least: itself because it's reflexive);
 * Set-like: sinograms have a finite number of stroke so the class of its components is a set;
 * Non-euclidean: because it's antisymmetric.

This relation defines extrema.
An element $$x$$ is maximal if and only if there is no element $$y$$ different from $$x$$ such that $$x$$ is a component of $$y$$.
Similarly, An element $$x$$ is minimal if and only if there is no element $$y$$ different from $$x$$ such that $$y$$ is a component of $$x$$. It's also a radical.
The greatest element is a sinogram $$y$$ such as every sinogram $$x$$ is a component of $$y$$. The greatest component might not exist.

We use this fresh relation to attach two sets to each sinogram $$s \in \mathbb{S}$$. The first set $$\mathbb{T}_s$$ contains all sinograms $$t \in \mathbb{S}$$ such like $$t \mathcal{R} s$$ while the second set $$\mathbb{F}_s$$ contains all sinograms $$t \in \mathbb{S}$$ such like $$s \mathcal{R} t$$. Because $$\mathcal{R}$$ is antisymmetric, the intersection of two sets of a given sinogram contains only the sinogram itself. A sinogram $$s \in \mathbb{S}$$ has no other components than itself if and only if $$\mathbb{T}_s = \mathbb{F}_s = \left\{ s \right\}$$. $$\mathbb{T}_v$$ is called the component set of $$v$$ and $$\mathbb{F}_v$$ its etymon set.

### Constructing graphs to reach a structure

This part is aiming at acting like a natural bridge from what has been told afore to smotthly lead to a sinogram structure. We define several graph structures, comment them and explain why we move to another. Incidentally, we become a little bit more abstract. On the very beginning we define a basic edgeless graph with one vertex for each existing sinogram. Then, we describe several ways to add arcs to link vertices and finally choose one. We further perform an operation to merge some vertices together. On that new graph, vertices stand no more for a sinogram but rather more for an etymological class of sinograms.

As first step, we consider a graph $$G = \left(V, E\right)$$ whose vertex set $$V$$ is defined such like there is a bijection between $$V$$ and the sinogram set $$\mathbb{S}$$. That bijection allows us to speak about sinogram or vertex as it's the same object. Given a sinogram $$s \in \mathbb{S}$$ and its associated vertex $$v \in V$$, we write $$a \leftrightarrow v$$ to express that relation. The edge set of $$G$$ is currently empty. If we would draw $$G$$, it would merely show lonely dots.

The most basic to populate $$E_G$$ and to link those dots would be to add arcs according to <small>IDS</small>. That means you would draw arcs from a sinogram to its nearest components. In doing so you would get a parsing graph. This is interesting but we can go further. A parsing graph link each sinogram to its components. Etymons are more interesting than components. For a given sinogram couldn't we basically consider the final leaves of its parsing tree? Actually yes we could but transitional sinograms would be skipped. Those latters are etymons too and we want'em all. As we need to go farther than parsing tree, let's build another graph.

As second step, for two vertices $$v, w \in E$$ and two sinograms $$a, b \in \mathbb{S}$$ such like $$v \leftrightarrow a$$ and $$w \leftrightarrow b$$, we draw an arc (that's to say an oriented edge) from $$a$$ to $$b$$ if and only if the two following conditions are satisfied:

* $$a$$ is a component of $$b$$ which means $$a \mathcal{R} b$$;
* there exist no distinct sinograms $$x \in \mathbb{S}$$ such like $$ a \mathcal{R} x$$ and $$x \mathcal{R} b $$.

If $$a = x = b$$, we have $$a \mathcal{R} b$$, $$ a \mathcal{R} c$$ and $$c \mathcal{R} b $$ so it doesn't match then there are no self-loops. Given three distinct sinograms $$a, b, c \in \mathbb{S}$$ such like $$ a \mathcal{R} b$$ and $$b \mathcal{R} c$$ and three vertices $$u$$, $$v$$ and $$w$$ such like $$a \leftrightarrow u$$, $$b \leftrightarrow v$$ and $$c \leftrightarrow w$$ there are an arc from $$u$$ to $$v$$ and another arc from $$v$$ to $$w$$ then $$w$$ is reachable from both $$u$$ and $$v$$ whilst $$v$$ is reachable from $$u$$.

$$G$$ is currently the [transitive reduction](https://en.wikipedia.org/wiki/Transitive_reduction) of the aforementionned parsing graph. It doesn't match perfectly. We draw for instance such an intuitive graph on the left and its transitive reduction on the right. They are equivalent whilst talking about composition and the transitive reduction ensures there is zero or one single path from a sinogram to another. Arcs are top-to-down oriented.

{% highlight HTML %}
   a   b    a   b   The right graph is the transitive
    \ /|     \ /    reduction of the left one; they
     c |      c     have the same reachability.
     |/       |     
     d        d     Arcs are ↓.
{% endhighlight %}

To each vertex $$v \in V$$ we associate two subgraphs $$T_v$$ and $$F_v$$ defined as follows: $$F_v$$ is the subgraph of all vertices reachable *from* $$v$$ and $$T_v$$ of all vertices which can lead *to* $$v$$. We give another equivalent definition of $$F_v = V_{\mathbb{F}_v}$$ and $$T_v = V_{\mathbb{T}_v}$$. We also define $$\mathbb{T}_\mathbb{S} = \left\{ T_x, x \in \mathbb{S} \right\}$$ and $$\mathbb{F}_\mathbb{S} = \left\{ F_x, x \in \mathbb{S} \right\}$$. Note that $$F_v$$ is a tree but $$T_v$$ would be a « reversed » tree (arcs are swapped). However, $$T_v$$ can't be seen as the tree of the <small>IDS</small> of $$v$$ because of $$G$$ is a transitive reduction: it's a etymologic tree which contains all possible etymon of $$v$$. We may get interested in [Hasse diagram](https://en.wikipedia.org/wiki/Hasse_diagram). As usual, the size of a tree (or a reversed tree) is defined as the number of vertices it contains including the root and its length as the length of the longest enclosed path.

A vertex out-degree can be up 3 because of <small>IDC</small> arity. Built that way, this graph is a [multitree](https://en.wikipedia.org/wiki/Multitree) which means this is a directed acyclic graph in which the set of nodes reachable from any node form a tree.


{% highlight HTML %}
 x       A multitree. Arcs are left-to-right oriented.
  \      
   z     x and y are minimal vertices.
  /      z is a maximal vertex. It's also the greatest.
 y
{% endhighlight %}

$$G$$ is build with the partial order relation $$\mathcal{R}$$ so it's inherited its maxima. Let's call the vertices associated to the maximal sinograms the roots of the multitree and those associated to minimal sinograms the leaves of the multitree.

**Below haven't been upgraded yet to $$H$$. Make it clearer**

As third step we can remark it's possible for two sinograms $$a, b \in \mathbb{S}$$ to share the same etymon tree: $$T_a = T_b$$. To avoid such a duplication, we build a new graph $$H$$ upon $$G$$ by merging two vertices $$u, v \in E_G$$ when $$T_a = T_v$$:

* There is an surjection $$f : \left\{
  \begin{array}{l l}
    V_G \rightarrow V_H\\
    u \mapsto f(i)
  \end{array} \right.$$ such like $$\forall u, v \in V_G, f(u) = f(v)$$ if and only if $$T_u = T_v$$.
* A vertex 

A vertex $$\mathbb{S} \ni a \leftrightarrow v \in V_H$$ from the resulting graph represents the etymology class of all sinograms within $$\mathbb{S}$$ you can get from $$T_a$$.

Be careful: directed tree are usually defined such like the root can reach leaves. Sinogram trees are reversed. I choose to keep going with reversed trees because it makes the composition relation easier to be defined. Moreover, The formal definition of a forest is a multitree with no intertwinned trees. Then it's formally wrong to call such a multitree a forest but it's funnier to perform sylvan path finding ☺

### Structure of some sets

By construction, the sets $$\mathbb{F}_\mathbb{S}$$ and $$\mathbb{T}_\mathbb{S}$$ are subsets of the set of all subsets of $$\mathbb{S}$$. This latter set is called the [power set](https://en.wikipedia.org/wiki/Power_set) and noted $$2^\mathbb{S}$$. We know that $$\left( 2^\mathbb{S}, \cup, \cap, \complement \right)$$ [is a finite Boole algebra](https://en.wikipedia.org/wiki/Algebra_of_sets) then we can build an isomorphism to other Boole algebras. What can we say about $$\mathbb{F}_\mathbb{S}$$ and $$\mathbb{T}_\mathbb{S}$$? This is a thrilling question which can be extended to $$\mathbb{U}$$, knowing non-finite Boole algebra are not isomorphic. If $$\mathbb{F}_\mathbb{S}$$ and $$\mathbb{T}_\mathbb{S}$$ would be some kind of algebra, it would be nice to name it Chinese algebra!

We hereby restrain the scope to finite set $$\mathbb{S}$$ so we get a finite graph and all is finite. This matter for the definition of cartesian product $$\mathbb{T}_a \times \mathbb{T}_b$$ which could be defined as the set of all sinograms which can be composed from each component of $$a$$ and $$b$$. So it would belong to $$\mathbb{U}$$ and not to $$\mathbb{S}$$. Scaling up that sketch to $$\mathbb{U}$$ might get additionnal precision to be added, such like a choice between the transitive reduction and the minimal equivalent graph.

We precise the following sets from component and compound trees. Let's have two sinograms $$a$$ and $$b$$ from $$\mathbb{S}$$.

 * $$ \mathbb{F}_a \times \mathbb{F}_b $$ can be equal to $$ \mathbb{F}_a \cup \mathbb{F}_b$$ because of the structure of $$\left( \mathbb{S}, \mathcal{R} \right)$$ but we can also choose to widen it in $$\mathbb{U}$$. It's a difficult choice to define the right thing;
 * $$ \mathbb{T}_a \times \mathbb{T}_b $$ can be defined as the set of all sinograms which can be composed from each component of $$a$$ and $$b$$. Methinks it's the more natural definition.

We can order those sets (let's check about $$\mathbb{T}$$ and $$\Delta$$):

$$ \mathbb{T}_a \cap \mathbb{T}_b \subset \mathbb{T}_a \cup \mathbb{T}_b \subset \mathbb{T}_a \times \mathbb{T}_b $$

$$ \mathbb{T}_a \setminus \mathbb{T}_b \subset \mathbb{T}_a \Delta \mathbb{T}_b \subset \mathbb{T}_a \times \mathbb{T}_b $$

$$ \mathbb{F}_a \cup \mathbb{F}_b = \mathbb{F}_a \times \mathbb{F}_b \subset \mathbb{T}_a \times \mathbb{T}_b $$

$$ \mathbb{F}_a \cap \mathbb{F}_b \subset \mathbb{F}_a \cup \mathbb{F}_b $$

$$ \mathbb{F}_a \setminus \mathbb{F}_b \subset \mathbb{F}_a \Delta \mathbb{F}_b \subset \mathbb{F}_a \cup \mathbb{F}_b $$


### Sinogram frequence

Well… finally what's the most efficient way to learn Chinese? Have we stepped forward or is all this theoretic discussion useless? Let's have a look on such a forest. Arcs are from the top to the bottom, thus arc $$af$$ is $$a \rightarrow f$$.

{% highlight HTML %}
  a    b    c    d
  |   /|\   |        A denser forest. Arcs are from the top to the bottom.
   \ / | \  e                        +–––––––––––––––––––––––––––––––––––+
    f  |  \ |               Sinogram | a | b | c | d | e | f | g | h | i |
    \  /   \|                        +–––+–––+–––+–––+–––+–––+–––+–––+–––+
     `g     h              Frequency | 4 | 5 | 4 | 1 | 3 | 3 | 2 | 2 | 1 |
      \    /                         +–––+–––+–––+–––+–––+–––+–––+–––+–––+
       \  /      Component tree size | 1 | 1 | 1 | 1 | 2 | 3 | 4 | 4 | 8 |
        `i                           +–––––––––––––––––––––––––––––––––––+
{% endhighlight %}

Now it's become easier to define the frequence of a sinogram $$\mathbb{S} \ni x \leftrightarrow a \in G$$ as the cardinality of $$F_a$$. Moreover, let's have a look on the underlying non directed graph of the forest in previous illustration. Such graph can be obtained by replacing every arcs (that's to say directed edges) by (non directed) edges.

According to the [usual definition](https://en.wikipedia.org/wiki/Graph_center) of [closeness centrality](https://en.wikipedia.org/wiki/Centrality#Closeness_centrality), the center of this underlying graph is the set of vertices of minimum eccentricity, thus here $$\left\{b, f, h, i\right\}$$. Even if $$f$$, $$h$$ and $$i$$ don't have a big frequency, $$b$$ hereby belongs to the centre and has the biggest frequency. It's clear now that components have a higher frequency than compound so the first assumption may be hereby explained: sorting sinograms by frequency leads to sort out components before compounds.

We define $$f: \mathbb{S} \rightarrow \mathbb{R}^*_+$$ the function which maps a sinogram $$x$$ to its frequency $$f(x)$$. Let's pick up two sinograms $$a$$, $$b$$ from $$\mathbb{S}$$. We have a range of triangle inequalities to be completed.

$$\forall c \in T_a \cup T_b, f\left(c\right) \geq f(u \in F_a) + f(v \in F_b)$$

$$\forall c \in T_a \Delta T_b, ?$$

$$\forall c \in F_a \cup F_b, f\left(c\right) \leq f(u \in T_a) + f(b \in T_b)$$

The following triangle inequalities must be proved right or wrong:

$$\forall c \in T_a \setminus T_b, f\left(c\right) \leq \mathit{abs}(f(a) - f(b))$$

$$\forall c \in T_a \Delta T_b, ?$$

$$\forall c \in F_a \setminus F_b, f\left(c\right) \geq \mathit{abs}(f(u \in F_a) - f(v \in F_b))$$

We may also intuit the higher is a sinogram frequency, the closer its vertex is to the centre so we would just need to find an centrality mesure which is appropriate to directed graph. The [hierarchical closeness](https://en.wikipedia.org/wiki/Hierarchical_closeness) structural centrality measure is an extension from the previous definition. I haven't implemented that measure yet but according to its definition, it may suit our needs.

Actually, let's don't get stuck into technical consideration. Back to real life, frequency doesn't mean hierarchical closeness but merely: how often do I use that word in my speech? Existing datasources provide such statistics. To put it in a nutshell, learning sinograms by frequency means a trade-off between those centrality and speech frequency definitions is mandatory. One a hand, some sinograms are used only as components and never alone; even is they're quite close to the centre, we don't need to learn them because we would never use them. One the other hand, some words are used very often (like figures and numerals) but may be far from the centre.

### Drawing the forest

Displaying the messy forest made with thousands of sinograms demands to be performed automatically. Designing an algorithm which can fit is both a very difficult and complex part. Maximal vertices may be clustered to show the forest structure so it may involve [geographical](https://en.wikipedia.org/wiki/R-tree) algorithm. We could also try to layout it with [Force-directed](https://en.wikipedia.org/wiki/Force-directed_graph_drawing) algorithms. The essential points of a such a drawing are to know what we want to be shown and to understand we can't use it to discover better the forest structure: this is up to our imagination.

__The following is still a draft__

## Bibliographic recension

This project has been initiated with a bibliographic recension in order to draw a state of the art. Interesting article detail some field but leave some other still to be explorer.

### State of the art

I've found most of these articles on their respective authors' websites. However, if I wouldn't be allowed to publicly expose some of them, just send an email about that.

## Implementations

This part comes when theoretic frame has been weel-defined. Some ideas directly come from the recension and may be interested to implement because of technical points or to get a deeper comprehension of what we're talking about. Some others may have been not explored yet.

* Compare Chinese frequency and [that diagram](http://tigger.uic.edu/~ejv/img/thelwallfigure1.jpg). Which viewpoint can we get a similar phenomenom from? Can we give a bounding function?
* It'd be nice to unify variants. Not all but at least the Z axix (like 阝). It's easier. ANd get tir of simplified characters, it's easier.
* How to store ideogram graphs? Graph databases are quite inviting. Such a database may be able to deal with character variants, thanks to the Unicode Consortium  [character-glyph model](https://github.com/piotr2b/chinese-huawen/blob/master/refs/New%20Perspectives%20in%20Sinographic%20Language%20Processing%20through%20the%20Use%20of%20Character%20Structure.pdf) or any other;
* How to query character set? [Query language](https://github.com/piotr2b/chinese-huawen/blob/master/refs/A%20Structural%20Query%20System%20for%20Han%20Characters.pdf) sketch has been drawn to mimic `grep`;
* Signal processing may be useful to break down a character in all possible ways. Either it'd use <small>IDS</small> (so-called [Unicode way](https://en.wikipedia.org/wiki/Chinese_character_description_languages#Ideographic_Description_Sequences)) either it'd choose [Wenlin's <small>CDL</small> way](https://en.wikipedia.org/wiki/Chinese_character_description_languages#CDL). Assuming Unicode way has been chosen, could we break down a character only by  analysing its glyph or would we need to use Wenlin's stroke-end way then to browse for fetched patterns in an already-kown-character database?
* I was first aiming at learning characters better and more easily: given a characters set, what's a best order to learn all of them? This sounds like a sylvan  graph traversal for which we would hop from tree to tree in a forest ^^ Well, actually not: a forest is a disjoint tree union and trees hereby are intertwined. The aforementionned order may be related to [most semantic subcharacter paths](https://github.com/piotr2b/chinese-huawen/blob/master/refs/New%20Perspectives%20in%20Sinographic%20Language%20Processing%20through%20the%20Use%20of%20Character%20Structure.pdf);
* Student could thus build a optimal learning strategy. To sort out by frequency is not [maximal](https://github.com/piotr2b/chinese-huawen/blob/master/refs/Efficient%20learning%20strategy%20of%20Chinese%20characters%20based%20on%20network%20approach.pdf));
* Ideograms can be seen as a set which we could give a [basis](https://en.wikipedia.org/wiki/Basis_%28linear_algebra%29) to. A basis is a free, spanning orthogonal family. It's a radical list. Some attempt have been performed by Ancient lettered Chinese to give radical lists. Can we find criteria to evaluate such list relevance? According to those criteria, can we find the best basis?
* Once we've found such a criteria, we can use it to find the best base we could use to generate characters. We can enhance <small>IDS</small> by adding them some cues about glyph construction and thus we can build a new way for computers to handle Asian scripts. So fonts would be defined as a set of clues. This is similar to Wenlin's Institute way, but something more intersting cause embedded in computer font rendering softwares. So finally they could deduce glyphs of previouly unkown characters. 214 Kangxi radicals is a de facto standard. So it can be improved.
* Moreover character are compound most of the time. What's the relation between the number *n* of existing characters we can make from *x* characters?
* Several tools can compose new ideograms from existing components. I don't feel enough a valuable typesetter to be useful in any way in that field. Methinks the more than 80,000 ideograms included in unicode make that issue less critical.



-----

## New implementation design

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

Then, as the graph has now been constructed, we can query it. This is something else but it would still need a grammar to form a domain-specific language. It sure will be very interesting to design such a grammar. It reminds me somethnig like XML queries. Maybe I could get inspired by grep as in an article I read.

### Grammar types

At least three kinds of context-free grammars will be used in this project:
 * The first one (the most simple) is for level 1 to parse strings which contain variants to formal <small>IDS</small>. 
 * The second one (the most show-off: «hey buddy, I've defined a grammar for Chinese!») is used in level 2 to parse <small>IDS</small>.
 * The last one (the most interesting) will appear in the query engine to define its language.

Reading « Introduction to Automata Theory, Languages, and Computations » from Hoppcroft, Motwani and Ullman may seem just academic duty but I surely will benefit from all this theory so I must keep on! ~
