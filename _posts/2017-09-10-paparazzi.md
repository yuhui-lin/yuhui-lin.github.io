---
layout: post
title: >
        Analyzing IMDb Top Celebrities Collaborative Relationship
author: "Yuhui Lin"
date: "Sep 10, 2017"
categories: blog
tag: 
    - IMDb Database
    - data analysis
    - d3.js
    - typescript
comments: true
root: "../"
---

{% assign lvl = page.url | append:'X' | split:'/' | size %}
{% capture relative %}{% for i in (3..lvl) %}../{% endfor %}{% endcapture %}

<style>
svg {
  display: block;
  //margin: 0 auto; 
  margin-left: -120px;
}
</style>
<link href="{{ relative }}misc/IMDb_celebrities/d3.ts/styles.css" rel="stylesheet" />

# Overview
As an international student in Canada, I found I am only familiar with a few number of TV show/movie stars. As a result, I decided to write a post concerning the relationship between tv/movie celebrities. Instead of focusing on the rumors or hearsay on gossip magzines, this post is more about working relationships and career achievements.

I get the top 200 celebrities from [IMDb Most Popular Females/Males](http://www.imdb.com/search/name?gender=male,female) on Aug 2017. This ranking is based on IMDb STARmeter which does not mean the acting skills of the stars but the level of public interest in the person. The working relationships are extracted from [IMDb Datasets](http://www.imdb.com/interfaces) located in the AWS S3 bucket.

All source code has been uploaded to [this github repository](https://github.com/yuhui-lin/IMDb_celebrities).

# Strongly connected celebrities

Working relationship can be easily demonstrated by graphs. In this post, I use D3.js and Typescript to draw interactively [Force-Directed Graph](https://bl.ocks.org/mbostock/4062045). D3.js is a really cool visualization tool which can be hosted in github.io with Jekyll Blog. while learning Javascript, I found Typescript is rather interesting. It provides not only plenty of object-oriented syntactic sugars, but also static analysis which helps me learn D3.js faster.

In the following graph, I tried to find strongly connected celebrities' groups by applying a classic community detection algorithm - [Louvain Method](https://perso.uclouvain.be/vincent.blondel/research/louvain.html). This algorithm divides the top celebrities into groups such that each set of person is densely connected internally and sparsely connected between groups.

**TV stars'relationship network:**
<svg id='tv' width="1000" height="700"></svg>
*(You can click-and-drag the nodes around. The name of celebrities should emerge when hovering over the circles. Different groups are distinguished by different color. The radius of circles stand for their number of connections.)*

For TV show stars, there are a few densely connected groups:

**Game of Throne**:

- Emilia Clarke
- Nikolaj Coster-Waldau
- Peter Dinklage
- Lena Headey
- Kit Harington
- Aidan Gillen
- Rose Leslie
- Sophie Turner
- Natalie Dormer

**Vikings**:

- Katheryn Winnick
- Travis Fimmel

**Riverdale**:

- Cole Sprouse
- Mädchen Amick

**Big Little Lies**:

- Shailene Woodley
- Reese Witherspoon
- Shailene Woodley

**Guardians of the Galaxy**:

- Chris Pratt
- Zoe Saldana

**Movie stars'relationship network:**
<svg id='movie' width="1000" height="700"></svg>

For movie stars, they are more likely to collaborate with varous of people.

# Centers Among Stars

In this section, I am going to compare the "degree" of top celebrities.



# Reference

- inspired by [别开枪，我不是狗仔——数据剖析明星关系](https://zhuanlan.zhihu.com/p/27369379)

<script src="{{ relative }}misc/IMDb_celebrities/d3.ts/bundle.js"></script>
<script>
  bundle.draw('movie', 'movie', "{{ relative }}misc/IMDb_celebrities/output/graph_200.json");
  bundle.draw('tv', 'tvEps', "{{ relative }}misc/IMDb_celebrities/output/graph_200.json");
  <!-- bundle.draw('all', 'all', "{{ relative }}misc/IMDb_celebrities/output/graph_200.json"); -->
</script>

{% include disqus.html %}