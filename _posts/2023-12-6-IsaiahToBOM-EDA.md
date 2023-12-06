---
title: Exploring Isaiah's Legacy in the Book of Mormon - Exploratory Data Analysis and Dashboard
description: The words of the biblical prophet Isaiah are referenced in the Book of Mormon over 700 times! My project explores the connections in terminology, themes, and historical contexts. 
layout: post

github:
    is_project_page: true
    repository_name: Isaiah-to-BOM
    repository_url: https://github.com/jxnpass/Isaiah-to-BoM

date: 2023-12-5 17:50:00
---

## Table of Contents

- [Introduction](#introduction)
- [Static Graphics](#static-graphics)
- [Networks](#cross-reference-networks)
- [Dashboard](#dashboard)
- [Acknowledgements](#acknowledgements-and-ethical-considerations)

## Introduction

The Holy Bible is one of the most revered and consistently read texts in the entire world. The complexities of biblical histories, from religious themes and worship, languages, and to major societal events, fascinate scholars today. However, what is commonly overlooked is the connections between the Bible and the Book of Mormon. In the narrative beginning of the Book of Mormon, the record opens with a family commanded by God to leave their home in Jerusalem, escape the impending doom of the Babylonian Exile, and start a new civilization in the modern-day Americas. One of the belongings of this family was a record written on brass plates, which contains the biblical prophets and narratives from the five books of Moses and the words of the Old Testament prophets up to Jeremiah. One of the most commonly referenced prophets made by Book of Mormon characters is Isaiah, in which his words, themes, and doctrines are referenced 780 times (cite ref).

The prophet Isaiah is heavily revered for Book of Mormon peoples, and their writers and preachers regularly recite from the 66 chapters we have today. However, modern scholars have stated that the authorship of the book of Isaiah is not solely written by the prophet: numerous arguments cirulated stating that Isaiah's disciples had written chapters 40-66, and Isaiah himself had only contributed chapters 1-39. This claim has validity since the second half is written after the Babylonian Exile (597 to 538 BCE), which was over a hundred years after Isaiah had passed on. The Book of Mormon family left Jerusalem in 600 BCE. This leads to the following question: how could Book of Mormon civilizations have the entire account of Isaiah in the brass plates if the latter half of the Book of Isaiah wasn't written after 538 BCE? 

Multiple scholarly interpretations have debated these concerns. One assertion is that the book of Isaiah was written wholly by the prophet himself, and disciples later edited it to be in its current format. Others speculate the possibility of divine intervention as the writings of Isaiah and the Book of Mormon went through translations. 

The aim of this post is not directed to discuss this concern in great detail, but to illuminate the breadth of Isaiah's writing using visualization and statistics, accounting for these common scholarly perspectives. We will also look into cross reference levels of similarities, subdivisions of Isaiah using [Bernhard Duhm's classifications](https://en.wikipedia.org/wiki/Book_of_Isaiah), presence of biblical terms, and summaries of words, verses, and chapters between authors. This project intends to promote a detailed understanding of the scriptures by visualizing complexities that are otherwise incomprehensible.  

## Static Graphics

<!-- WordClouds   -->

![ISH-WordCloud](/assets/Isaiah-to-BOM/graphics/wordcloud_DUHMS.png)

<p align="center">
    <img src="/assets/Isaiah-to-BOM/graphics/wordcloud_BOM.png" alt="image" width="40%" height="auto">
</p>

<!-- ![BOM-WordCloud](/assets/Isaiah-to-BOM/graphics/wordcloud_BOM.png) -->

<!-- Isaiah Summary  -->

![Isaiah-References](/assets/Isaiah-to-BOM/graphics/ref_count_ISH.png)

![Duhms-References](/assets/Isaiah-to-BOM/graphics/ref_count_DUHMS.png)

![Duhms-BibleDictionary](/assets/Isaiah-to-BOM/graphics/bd_DUHMS.png)

<!-- Book of Mormon Summary  -->

![BoM-References](/assets/Isaiah-to-BOM/graphics/ref_count_BOM.png)
![BoM-BibleDictionary](/assets/Isaiah-to-BOM/graphics/bd_BOM.png)

<!-- Comparison -->

![BoM-ISH-BibleDictionary](/assets/Isaiah-to-BOM/graphics/bd_comp.png)


## Cross Reference Networks

[By Chapter](/assets/Isaiah-to-BOM/network-visuals/by_chapter.html)

[By Verse](/assets/Isaiah-to-BOM/network-visuals/by_verse.html)

## Dashboard

[Streamlit](https://isaiah-to-bom.streamlit.app/)

## Acknowledgements and Ethical Considerations

All data used was made publicly available. The inspiration for this project came from the [OpenBible.info](http://www.openbible.info/labs/cross-references/) and [Medium](https://medium.com/swlh/analyzing-references-in-bibles-verses-using-complex-networks-with-pandas-and-gephi-8a4edc52e7ab). Part of the data was downloaded from the [LDS Documentation Project](https://scriptures.nephi.org/), a research organization providing public domain data files on LDS scriptures. Rest of the raw data was scraped from [Linguistics Study in the Book of Mormon](http://www.creationismonline.com/Mormons/Mormons.html) and [The Church of Jesus Christ of Latter-day Saints](https://www.churchofjesuschrist.org/).