---
title: "華文: an efficient way to learn Chinese"
layout: topic
index: true
collection: topics
changefreq: daily
abstract_html: "<p>Chinese language is not like most of Western languages: a sinogram like 貴 can be meaningful by its own whereas Western <i>z</i> means nothing by itself. Chinese is a very different thus very interesting language. What's the most efficient way to learn characters?</p><p>The rational way may be to learn components before compounds. Given that, the most efficient way may be to order Chinese character by frequency. We initially focus on a single sinogram sructure and then broaden the scope to sinogram composition directed network. We further foresee how to crawl it and retrieve data from it.</p>"
---
A table of content can be found at the bottom of this page.

## What's the most efficient way to learn Chinese?

Chinese language is not like most of Western languages: a Chinese character like 貴 can be meaningful by its own whereas Western _z_ means nothing by itself. Chinese is a very different thus very interesting language.

Most of Chinese handbooks are built in a Western fashion: daily-life conversation samples bring new vocabulary and syntax examples. This fashion doesn't take advantage of intrinsic Chinese language structure, which makes easier to discover 貴 when knowing yet 中, 一 and 貝. 貴 stands for expensive or honourable while 貝 refers to shell or money. This semantic link lets it easy to remember both of them. The rational way to learn Chinese may be to learn components before compounds. Given that, the most efficient way may be to order Chinese character by frequency.

## Summary

If reading bores you, watch to [__some pictures__](https://www.github.com/{{ site.links.github | append: "/chinese-huawen" | append: "/tree/master/gephi" }}) of what I got some times ago ☺

We begin with an introduction to [__sinogram structure__]({{ "../sinogram-structure/" }}) in which we compare Western and Chinese languages. How do they form new words? Chinese etymology is reachable in most case by just giving a look to the word. This etymology can be described with description sequence. However, some times it's more difficult because a character has a different shape: this is the sinogram variants problem. Finally, we imagine what could be a good Chinese learning order and why it matters.

Once the sinogram structure is described, we discuss the structure of the [__sinogram set__]({{ "../sinogram-set-structure" }}). How can you compose them? We can put sinograms together and use the composition relation to build several graph structures. We comment them and explain how we move from one to another to get an higher abstraction. We further define the sinogram frequency in two ways, geographically and graph-theoretically. We also sketch some ways to draw such graphs.

Previous parts define the environment of this project of theoretical surrounding. While I cas reading these, some questions or ideas came to my mind: « what if we could…? » and some of these possible [__features__]({{ "../features" }}) have kept. Some ideas directly come from the recension and may be interesting to implement because of technical points or to get a deeper comprehension of what we're talking about. Some others may have been not explored yet.

However, it also comes with tangible [__implementations__]({{ "../implementation-design" }}). The latters not only address programming problems but also grammar definitions.

## Recension and data

This project has been initiated with a [_*bibliographic research*_]({{ "../bibliographic-recension" }}) in order to draw a state of the art. Interesting articles detail some field but leave some other still to be explored.

Data sources are essential in that topic and any result heavily depends of them.

 * Unihan from the Unicode consortium;
 * Chise;
 * Kawabata;
 * and few others.

## About the name

{{ site.description }} The first character 華 of the project name means sinity; 文 stands for language. The whole phrase 華文 means _Chinese language_ and is read ㄏㄨㄚˊ ㄨㄣˊ or huáwén.

## Handling technic

The [GitHub repository](https://www.github.com/{{ site.links.github | append: "/chinese-huawen" }}) has a Get started section.

## Table of content

* TOC
{:toc}
