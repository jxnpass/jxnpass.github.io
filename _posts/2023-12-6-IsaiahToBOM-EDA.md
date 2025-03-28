---
title: Exploring Isaiah's Legacy in the Book of Mormon - EDA and Dashboard
description: The words of the biblical prophet Isaiah influenced over 35% of the Book of Mormon! This post utilizes generated data and illustrates the impact of Isaiah on the Book of Mormon using cross references, textual similarities, and Bible language. 
layout: post

github:
    is_project_page: true
    repository_name: Isaiah-to-BOM
    repository_url: https://github.com/jxnpass/Isaiah-to-BoM

tags: [Dashboards, Data Science, Python]
date: 2023-12-6 17:50:00
---

## Table of Contents

- [Synopsis](#synopsis)
- [EDA](#eda)
    - [Isaiah and Popular Chapters](#isaiah-and-popular-chapters)
    - [Isaiah in the Book of Mormon](#isaiah-in-the-book-of-mormon)
    - [Biblical Language](#biblical-language)
    - [Textual Differences](#textual-differences)
    - [Cross Reference Networks](#cross-reference-networks)
    - [Dashboard](#dashboard)
- [Conclusion](#conclusion)
- [Acknowledgements](#acknowledgements-and-ethical-considerations)

## Synopsis

For a full description of my project motivation and synopsis, review the first section in [*Exploring Isaiah's Legacy in the Book of Mormon - Data Collection*](https://jxnpass.github.io/2023/12/05/IsaiahToBOM-DC.html#synopsis).

There are four areas whereby we can scope our exploration between Isaiah and the Book of Mormon:
1. Where in Isaiah does the Book of Mormon most refer to?
2. Where in the Book of Mormon is Isaiah heavily referenced?
3. How much is biblical language utilized in Isaiah and the Book of Mormon?
4. Where do textual differences occur between Duhm's Classifications and the Book of Mormon?

## EDA

The data I scraped and generated includes a few variables that need some definitions before we dive into the EDA. 

Duhms Category: [Bernhard Duhm](https://en.wikipedia.org/wiki/Book_of_Isaiah) uses varying structures and models to break up and explain the chronological and thematic differences in Isaiah. In this project, we used the threefold structure to identify them:
- **Proto-Isaiah** lists chapters 1-39 (742-687 BCE). It encompasses the stories and words of Isaiah in 8th-century BCE, where he narrates certain events like his call to prophethood, the Syro-Ephramite war, and the rise of the rightoeus king Hezekiah.
- **Deutero-Isaiah** lists chapters 40-55 (597-538 BCE). This is believed to originate from the work of an anonymous 6th-century acolyte of Isaiah, written during the time of the Babylonian exile. 
- **Trito-Isaiah** lists chapters 56-66 (after 538 BCE). This was mainly composed after the Exile and the Jews' return to Jerusalem.

Similarity Score and Reference Type: I used `nltk` and `textdistance` in Python to calculate text similarities between the determined references. The similarity scores calculated ranged from 0 to 1, 1 being word-for-word alike. I categorized it based on the score as follows:
- Direct Quote = .75 to 1
- Shared Language = .25 to .75
- Similar Theme = 0 to .25

More info about the similarity score calculations and data creation can be found on [*Exploring Isaiah's Legacy in the Book of Mormon - Data Collection*](https://jxnpass.github.io/2023/12/05/IsaiahToBOM-DC.html).

### Isaiah and Popular Chapters

A viable method to chart cross references throughout Isaiah is by utilizing a bar chart. The following graph counts the number of times a verse from the chapter is used in the Book of Mormon, whether that be a verse that directly quotes, shares language, or has a similar theme to Isaiah.  

<p align="center">
    <img src="/assets/Isaiah-to-BOM/graphics/ref_count_ISH.png" alt="image" width="250%" height="auto">
</p>

Note: I created a [streamlit dashboard](https://isaiah-to-bom.streamlit.app/) that makes viewing reference barcharts easier to read and interactive. 

Ultimately, we see that Isaiah 2-14 and 48-55 are heavily quoted, but Isaiannic language and themes are pulled from throughout the text. It is important to note, however, that based on the [linguistic data](http://www.creationismonline.com/Mormons/KJV_Order.pdf) I scraped, a reference does not mean that the Book of Mormon author meant to directly pull doctrine or words from Isaiah, rather, modern-day scholars found a thematic or language connection between them. 

A summarized version applies the Duhms categories to illustrate where cross referencing occurs. 

![Duhms-References](/assets/Isaiah-to-BOM/graphics/ref_count_DUHMS.png)

We see that a lot of quoting from Isaiah comes from chapters 1 through 39 (Proto), and a few from 40 through 55 (Deutero). Surprisngly, we find no direct quotations from Trito-Isaiah. But, we do detect regular connections between language and themes from all three sections. 

### Isaiah in the Book of Mormon

We can also chart how the Book of Mormon references Isaiah. The following graph facets bar charts by author and then provides a **proportion** of how much of the specified chapter references Isaiah. 

<p align="center">
    <img src="/assets/Isaiah-to-BOM/graphics/ref_count_BOM.png" alt="image" width="250%" height="auto">
</p>

Note: I created a [streamlit dashboard](https://isaiah-to-bom.streamlit.app/) that makes viewing reference barcharts easier to read and interactive. 

We find that the chapters that consistently quote Isaiah are 1 Nephi 20-21, 2 Nephi 6-8, 12-24, and Mosiah 14-15, and 3 Nephi 20-22. Alma and Helaman pull regular themes and language, but abstain from using direct quotations. 

A writer has a key indicator for when he intends to quote Isaiah directly. 1 Nephi 19:24 declares to an audience to "hear ye the words of the prophet," before 1 Nephi 20-21 is issued (which are direct pulls from Isaiah 48-49). In 2 Nephi 25:5, Nephi claims that his "soul delighteth in the words of Isaiah," after exhaustively quoting Isaiah 2-14. In 3 Nephi 23:1, the Ressurected Christ states his approval for the author, and giving "a commandment" to "search... diligently; for great are the words of Isaiah," wherein 3 Nephi 22 quotes all of Isaiah 54. Hence, we know that plenty of the "direct quotes" are intentional. 

Mosiah 14-15 tell a different story. In his argument against Noah's wicked priests, Abinadi pulls Isaiah 53 for Mosiah 14, starting with the phrase "did not the prophet Isaiah say." After his recitation, he then references another verse, particularly Isaiah 52:7, multiple times, but each with a different twist.  

Ultimately, there are many prophets who find Isaiah's words very useful in teaching about Jesus Christ, the House of Israel, the Abrahmic Covenant, and other biblical themes. Throughout the Book of Mormon, prophets utilize differing styles in teaching; Isaiah's teachings likely impacted the prophets comprehension of gospel topics differently, and thus fostered their enthusiam to reference his words. 

### Biblical Language

The [LDS Bible Dictionary](https://www.churchofjesuschrist.org/study/scriptures/bd?lang=eng) is a useful resource for comprehending certain characters, themes, events, or locations within biblical times. More often are common terms used in both Isaiah and the Book of Mormon to mention doctrine, with words like "Lord" or "God" as the top two most used words. Other terms mentioning locations (or peoples) like Zion, heaven, Israel followed. Certain biblical figures and places like Jerusalem, Moses, and even Isaiah were mentioned occasionally, but paled in comparison when mentioning Lord and God in text. 

Because of how extensive the LDS Bible Dictionary is, finding some word within a verse that matches isn't too significant. What matters mainly is how much Isaiah uses common biblical themes and terms and if it matches with the Book of Mormon quotations. 

The figure below shows what proportion of verses within a chapter has a biblical term used. 

![Duhms-BibleDictionary](/assets/Isaiah-to-BOM/graphics/bd_DUHMS.png)

Proto and Trito-Isaiah seem to use biblical terminology more-so than Duetero-Isaiah. My opinion for this finding is that Deutero-Isaiah presents what is called the [Servant Songs](https://www.britannica.com/topic/biblical-literature/Isaiah). While the language clearly points to Jesus Christ, the decree is extensively metaphorical, and biblical context involving location, characters, or themes are less prevalent.

![Duhms-BOM-BibleDictionary](/assets/Isaiah-to-BOM/graphics/bd_comp.png)

This violinplot takes in data from Isaiah's cross references and pairs it to where its mentioned in the Book of Mormon. A symmetrical violin-shape would indicate that the chapters in Isaiah use the same proportion of biblical terminology as the chapter in the Book of Mormon. In this case, every reference be it directly or thematically related seems to pair up regarding biblical terminology, except for Deutero-Isaiah. This likely occurs for one of two reasons. Book of Mormon authors when quoting Deutero-Isaiah may liken or relate the words to Jesus Christ and other important biblical themes, in which the LDS Bible Dictionary recognizes biblical terminology within the Book of Mormon verses, and less so from Isaiah's symbolism. In addition, modern scholarship could have recognized where Book of Mormon authors depict Christ as a "servant" that suffers, and references these themes to Deutero-Isaiah. 

### Textual Differences

Recall that the Book of Mormon narrative begins in 600 BCE, when Lehi's family left Jerusalem. This brings up an interesting concern: how could Book of Mormon civilizations have the entire account of Isaiah in the brass plates if the latter half of the Book of Isaiah wasn't written until after 597 BCE? This means that only Proto-Isaiah could have been written before then. Deutero-Isaiah, however, is often quoted, as we'll see later.

Certain theories provide solutions to justify this chronological discrepancy. The most convincing inference about the Isaiah problem is arguing for the sole authorship of the book of Isaiah. Meaning, Isaiah wrote Proto, Deutero, and Trito-Isaiah during his lifetime, and the latter two sections were written as lengthy prophecies. This viewpoint would require, however, that the writing is linguistically similar across the three sections. 

Performing the linguistic analyses of the textual differences between the three sections are beyond the scope of this project, as this post aims to illustrate how Isaiah is referenced in the Book of Mormon in general. However, we can look at a glance how  words are unique between sections generally. 

Since we've seen so many bar charts, I figured I'd switch it up and use some wordclouds! Using Python's `WordCloud` package, I displayed text occurances as seen here. Bigger words mean that they are found more often in the scriptures than smaller words. 

![ISH-WordCloud](/assets/Isaiah-to-BOM/graphics/wordcloud_DUHMS.png)

At first glance, Proto, Deutero, and Trito-Isaiah seem to procure the same words, such as "Lord", "God", "unto", "will", etc. However, there are a few differences to note. Proto-Isaiah has an astonishing representation of the word "day". This refers to how Isaiah makes prophesies:
- "In the last days..." (Isaiah 2:1)
- "For the day of the Lord..." (Isaiah 2:11)
- "In that day..." (Isaiah 3:18)
And sometimes to refer to events in history:
- "from the day that Ephraim departed from Judah" (Isaiah 7:17)
- "as in the day of Midian" (Isaiah 9:4)

One could argue that this evidence that the book of Isaiah is written by multiple authors, as 'day' is not used in other sections. However, each section of the book of Isaiah was to serve a different purpose. Chapters 1-39 might have had the intention to prophesy of specfic events in Jewish history, Christ's life, and the latter days. 

Duetero-Isaiah has a prevalence of the word "Israel" in its section. Israel is mentioned so thoroughly in this section, because at this time Israel was taken over by Babylon and in bondage. The author of this section (whether it is Isaiah or not) directed his message to where the voice of the Lord was magnified to speak to "Israel" the "servant" (Isaiah 41:8), identifying himself as the "Holy One of Israel" (Isaiah 43:14) or "King of Israel" (Isaiah 44:6). In a way, the message of Duetero-Isaiah is to remind them of their identity and to declare God's obligation to be with His covenant people.

### Cross Reference Networks

I used Python's ```pyvis.network``` and ```networkx``` to generate the following network graphics. 

[By Chapter](/assets/Isaiah-to-BOM/network-visuals/by_chapter.html)

* Width of the edge (lines) signify number of shared verses between chapters
* Colored edges show which connections hold direct quotes. Blue edges are direct quotes from Proto-Isaiah, red edges are direct quotes from Deutero and Trito-Isaiah. Gray edges connect chapters with shared language or similar themes

[By Verse](/assets/Isaiah-to-BOM/network-visuals/by_verse.html)

* <u>Loading the verse network takes about 20 seconds</u>
* Black edges connect direct quotes
* Dark gray edges connect verses with shared language
* Light gray edges connect verses with similar themes
* You'll notice that Isaiah 7:14 is colored gold. I gave it attention because this verse is actually matched 55 times, but the network could not handle that many connections. I limited the network to only show those that had a similarity score greater than 0

### Dashboard

This streamlit dashboard makes it easy to look at cross reference data between book authors, chapters, and even analyze individual scriptures. 

[Streamlit](https://isaiah-to-bom.streamlit.app/)

## Conclusion

In conclusion, our exploration on the associations between the Book of Mormon and Isaiah has unearthed fascinating insights that shed light on the intricate tapestry of these scriptures. This comprehensive analysis of scriptural cross references, linguistic patterns, and visualizations can provide a nuanced understanding of how Book of Mormon prophets engaged with Isaiah's profound teachings. As we grapple with the chronological discrepancy, considering theories such as sole-authorship, we recognize the complexity is inherent in reconciling historical timelines. The heavy reliance on specific chapters and verses, as revealed through cross-reference networks and linguistic analyses, attests to the profound influence of Isaiah on the teachings found in the Book of Mormon. The network visualizations, particularly the color-coded and widened edges, became invaluable graphics to unravel the interwoven nature between scriptural references, offering a dynamic perspective on the relationships between chapters and verses. The created Streamlit Dashboard can further enhance the accessibility of scriptural findings, with the intention of inviting readers to delve deeper into the data analytically and interactively. 

Future research could dive deeper into textual differences between the Duhm's Classifications and the biblical terminology within the texts, as I only scratched the surface of these questions. In addition, other projects could determine scholarly methods to dictate which verses are considered direct quotes and which do not, as I mainly utilized math and statistics to determine these categories. I ultimately encourage all to invest in future exploration of the rich intersection of the scriptures, and I urge both seasoned scholars and dilettante readers to continue discovering textual complexities and contributing to the ongoing discussion about the connections between the Book of Mormon and Isaiah. 

## Acknowledgements and Ethical Considerations

All data used was made publicly available. The inspiration for this project came from the [OpenBible.info](http://www.openbible.info/labs/cross-references/) and [Medium](https://medium.com/swlh/analyzing-references-in-bibles-verses-using-complex-networks-with-pandas-and-gephi-8a4edc52e7ab). Part of the data was downloaded from the [LDS Documentation Project](https://scriptures.nephi.org/), a research organization providing public domain data files on LDS scriptures. Rest of the raw data was scraped from [Linguistics Study in the Book of Mormon](http://www.creationismonline.com/Mormons/Mormons.html) and [The Church of Jesus Christ of Latter-day Saints](https://www.churchofjesuschrist.org/). I am grateful for these sources and their openness to provide available data for me to complete this project. 