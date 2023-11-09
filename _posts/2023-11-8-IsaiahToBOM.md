---
title: Exploring Isaiah's Legacy in the Book of Mormon
description: The words of the biblical prophet Isaiah are referenced in the Book of Mormon over 700 times! My project explores the connections in terminology, themes, and historical contexts. 
layout: post

github:
    is_project_page: true
    repository_name: Isaiah-to-BOM
    repository_url: https://github.com/jxnpass/Isaiah-to-BoM

date: 2023-11-8 17:50:00
---

## Table of Contents

- [Introduction](#introduction)
- [Data Collection](#data-collection)
- [Data Processing](#data-processing)
- [Acknowledgements](#acknowledgements)

## Introduction

The Holy Bible is one of the most revered and consistently read texts in the entire world. The complexities of biblical histories, from religious themes and worship, languages, and to major societal events, fascinate scholars today. However, what is commonly overlooked is the connections between the Bible and the Book of Mormon. In the beginning of the Book of Mormon, the record opens with a family commanded by God to leave their home in Jerusalem, escape the incoming Babylonian Exile, and start a new civilization in the modern-day Americas. One of the belongings of this family was a record written on brass plates, in which the biblical prophets and narratives from the five books of Moses and the records of the Jews up and to the prophet Jeremiah. One of the most commonly referenced prophets made by Book of Mormon characters is Isaiah, in which his words, themes, and doctrines are mentioned 780 times (according to LDS scholars).

The words of Isaiah are some the most revered (and confusing) that Book of Mormon writers regularly recite. However, modern scholars have stated that the authorship of the book of Isaiah is not solely written by the prophet: arguments have circulated stating that Isaiah's disciples had written the second half of the book, and Isaiah himself had no contribution. This claim is valid since the second half of the book was written after the Babylonian Exile from 597 to 538 BCE, over a hundred years after Isaiah had passed on. The Book of Mormon family left Jerusalem in 600 BCE. This leads to the following question: how could Book of Mormon civilizations have the entire account of Isaiah in the brass plates if the latter half of the Book of Isaiah wasn't written after 538 BCE? 

Multiple scholarly interpretations have debated these concerns. One assertion is that the book of Isaiah was written wholly by the prophet himself, and disciples later edited it to be in its current format. Others speculate the possibility of divine intervention as the writings of Isaiah and the Book of Mormon went through translations. 

The aim of this post is not directed to discuss this concern in great detail, but to illuminate the breadth of Isaiah's writing using visualization and statistics, accounting for these common scholarly perspectives. We will also look into cross reference levels of similarities, subdivisions of Isaiah using [Bernhard Duhm's classifications](https://en.wikipedia.org/wiki/Book_of_Isaiah), presence of biblical terms, and summaries of word, verse, and chapters between authors. This project intends to promote a detailed understanding of the scriptures by visualizing complexities that are otherwise incomprehensible. 

## Data Collection

Finding the right cross reference data was difficult, so I had to pull information from uncanny sources. Data was downloaded and scraped from three locations:
1. [creationismonline.com](http://www.creationismonline.com/Mormons/Mormons.html)
2. [LDS Documentation Project lds-scriptures.xlsx](https://github.com/mormon-documentation-project/lds-scriptures/blob/master/lds-scriptures.xlsx)
3. [Church of Jesus Christ of Latter-day Saints Bible Dictionary](https://www.churchofjesuschrist.org/study/scriptures/bd?lang=eng)

The first location is a static html file that links viewers to numerous pdf files, articles, and websites highlighting differing attributes of LDS doctrine and policy. I was only interested in gathering the data from the [KJV_order.pdf](http://www.creationismonline.com/Mormons/KJV_Order.pdf), which contains the cross references of all bible verses to all Book of Mormon verses, normally listed as footnotes in the Latter-day Saint version of the KJV Bible. Since this was a pdf file listed on the main site, I wanted to extract the website links using webscraping and download the pdf of interest in Python:

### Dataset One: Scraping PDF links

``` py

# Import libraries
import pandas as pd
import requests
from bs4 import BeautifulSoup
import pdfplumber
import re

# for link in links:
#  print(link.get('href'))
# I want http://www.creationismonline.com/Mormons/KJV_Order.pdf and to download it for pdf scraping, so I will access it as so:

local_file_path = "../DirtyData/cross_reference.pdf"
cr_link =  requests.get(links[9].get('href'))
with open(local_file_path, "wb") as pdf_file:
        pdf_file.write(cr_link.content)

```

My newly downloaded pdf file was then extracted using ```pdfplumber```. I filtered the lines to extract only those that had "Isaiah" in the row and appended it to vector ```cr```.

``` py

cr = []

with pdfplumber.open(local_file_path) as pdf:
    for page in pdf.pages:
        pdf_text = page.extract_text()
        lines = pdf_text.split('\n')

        for line in lines:
            if "Isaiah" in line:
                cr.append(line)

```

Now instead of a vector of strings, I want to write a dataframe that has two columns: one for the Isaiah chapter, and one for the Book of Mormon chapter. However, this extracted the entire line of text instead of the two columns. I will need to initialize a new dataframe and write two new for loops that 1: limits the data into two columns and 2: cleans the string objects.

``` py

# setting up dataframes

cr2 = pd.DataFrame()
cr2['Isaiah_chapter'] = []
cr2['BoM_chapter'] = []

# 1: turning four column table into two columns
for row in cr:
    parts = row.split()
    if "Isaiah" in parts[0]:
        new_row = {'Isaiah_chapter': parts[0], 'BoM_chapter': parts[1]}
        cr2.loc[len(cr2)] = new_row
    if "Isaiah" in parts[2]:
        new_row = {'Isaiah_chapter': parts[2], 'BoM_chapter': parts[3]}
        cr2.loc[len(cr2)] = new_row

# 2: cleaning string values (separates numbers from name)

cr2['Isaiah_chapter'] = cr2['Isaiah_chapter'].str.replace(r'(\d+)', r' \1', 1)

nrs = []
for row in cr2['BoM_chapter']:
    if "Nephi" in row:
        nr = re.sub(r'(\d)Nephi', r'\1 Nephi', row)
        nr = re.sub(r'(\d+)', r' \1', nr, 2)
        nr = re.sub(' ', '', nr, 1)
        nrs.append(nr)
    else:
        nr = re.sub(r'(\d+)', r' \1', row, 1)
        nrs.append(nr)

cr2['BoM_chapter'] = nrs

```

Then I export my simple cross reference data to a csv file using ```cr2.to_csv(file_path)```.

### Dataset Two: Downloading Spreadsheet Data from the LDS Documentation Project

Thanks to the [LDS Documentation Project](https://scriptures.nephi.org/) for their [Mormon Documentation Repository](https://github.com/mormon-documentation-project/lds-scriptures) for making life very easy and providing an extensive list of the book title, chapter number, verse number, and verse text for every single LDS scripture, This allowed the pairing of sciptural text between Isaiah and the Book of Mormon to be a very robust process. More on this process in [Data Processing](#data-processing)

### Dataset Three: Scraping Bible Dictionary Terms from [churchofjesuschrist.org](churchofjesuschrist.org)



## Data Processing



## Acknowledgements

The inspiration for this project came from the [OpenBible.info](http://www.openbible.info/labs/cross-references/) and [Medium](https://medium.com/swlh/analyzing-references-in-bibles-verses-using-complex-networks-with-pandas-and-gephi-8a4edc52e7ab). Data was downloaded from the [LDS Documentation Project](https://scriptures.nephi.org/), a research organization providing public domain data files on LDS scriptures. 
