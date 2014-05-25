---
layout: post
title: "Confluence Learning Notes"
date: 2013-03-23 21:00
comments: true
categories: Productivity
---

Days ago I was asked to help building a knowledge sharing wiki for our team. Yes, I'm interested in different kinds of wiki. And most of my previous wiki experiences were coming from my own wiki which is based on open-sourced [DokuWiki](https://www.dokuwiki.org/dokuwiki). It's a good chance to learn the best enterprise wiki software -- [Confluence](http://www.atlassian.com/software/confluence/overview/team-collaboration-software).

<!--more-->

The [syntax of Confluence](https://confluence.atlassian.com/display/DOC/Confluence+Documentation+Home) is totally different from [DokuWiki](https://www.dokuwiki.org/wiki:syntax) or [Markdown](http://daringfireball.net/projects/markdown/syntax) or [Org mode](http://orgmode.org/), which is the most annoyed issue during learning. Except this, everything is almost perfect in Confluence. Especially, various of macros are quite inspiring to create beautiful pages.

Here I just want to show you how to insert a Table of Contents on the upper right corner, and create a multi-tab page.

**NOTE**: Below instructions are based on Confluence 3.5 (may not be compatible with the latest Confluence).

## TOC on upper right corner

1. First section this page;
2. Split this section into two columns;
3. Contents are placed in the left(first) column;
4. TOC is displayed in the right(second) column within a panel.
5.  Title/colore of the panel could be formatted by yourself.

<pre><code>
{section}
{column}
{numberedheadings}

body of contents

{numberedheadings}
{column}
{column:width=30%}
{panel:title=Contents| borderColor=#ccc| titleBGColor=#FFAF00| bgColor=#FFFFCE}
{toc}
{panel}
{column}
{section}
</code></pre>

## Multi-tab page

The following macros are required when designing multi-tab page:

* composition-setup
* card
* deck

<pre><code>
{composition-setup}
deck.startHidder=true
deck.tab.inactive.border = 1px #ccc solid
deck.tab.inactive.background = #ccc
deck.tab.active.border = 1px #ccc solid
deck.tab.active.background = #FFFFFF
deck.card.border = #FFFFFF
deck.width = 100%
deck.tab.spacer = 5px
{composition-setup}

{deck:id=FAQsCard}

{card:label=General Questions}

card 1 content

{card}

{card:label=Case & PR Questions}

card 2 content

{card}

{card:label=Other Questions}

card 3 content

{card}

{deck}
</code></pre>
