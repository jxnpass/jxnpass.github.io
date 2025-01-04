---
title: Managing a Volleyball Tourney as a Coder
description: I was challenged to manage a volleyball tourney with 29 teams, placed in 6 pools to play in an upper and a lower bracket. This post highlights how a stats nerd did this all using Google Sheets, Google Forms, and a little R coding.   
layout: post

github:
    is_project_page: true
    repository_name: TourneyManager
    repository_url: https://github.com/jxnpass/TourneyManager

date: 2025-1-2 17:50:00
---

## Table of Contents
- [Overview](#overview)
- [How It Works](#how-it-works)
- [How To Use It For Yourself](#how-to-use-it-for-yourself)
- [Highlights and Credits](#highlights-and-credits)

<p align="center">
<img style="width: 80%" src="/assets/TourneyManager/groupphoto.png" alt="tourneyphoto">
</p>

## Overview
One thing I love to do with my friends in Arizona is play volleyball. Over the years, the pickup volleyball scene in AZ has grown so popular that sometimes hundreds of people now come to play with us. My friends and I decided to host frequent tourneys during holiday breaks to foster greater competitive, offering prize money to winning teams.

For our 2025 New Year's Day tourney, I was tasked to create game schedules, collect scores, and seed teams into an upper and lower bracket. 

## How It Works
The main management system is hosted on this [Google Sheets file](https://docs.google.com/spreadsheets/d/1eCC9_43aua6a_YkqlNo_lh17zN3fFBxsDAmNnN1jnK0/edit?gid=1469598526#gid=1469598526) (this link leads to a copy of what I made with generic team names). Schedules, scores, and seeds are stored on various tabs on here. 

### Entering Team Information
The start of the program begins with the [Teams List](https://docs.google.com/spreadsheets/d/1eCC9_43aua6a_YkqlNo_lh17zN3fFBxsDAmNnN1jnK0/edit?gid=96325893#gid=96325893). All one needs to do is enter in the the name of the team under the first column, and the assigned pool in the second. Enter the number of rounds for each team to play in at the fourth column slot, highlighted yellow. The max number this manager can handle is eight, but an expert Excel coder can duplicate the sheet and reconfigure it if desired.

<video align="center" width="640" height="360" controls>
  <source src="/assets/TourneyManager/teamslist.mov" type="video/mp4">
  Your browser does not support the video tag.
</video>

This step, though simple, is essential for every other part of the spreadsheet. This list is used both to create the pool schedule AND score the round robin match results. 

### Creating the Round Robin
This next part utilizes the R scripts found in the [TourneyManager Repository](https://github.com/jxnpass/TourneyManager). The script create_round_robin.R takes in the sheets link, looks for the "Teams List" tab, and then creates a round robin schedule. Nice features of this script include the ability to incorporate bye rounds for pools with odd-numbered sizes, as well as print out the schedule back directly onto the sheet. If desired, you can change the stack argument at the top of the script to customize how many sheets to write.

When you supply the link (and change the stack argument), all that is needed is to run the script. When running, Google Sheets will ask for authentication. After following the steps, it should run the rest of the code. 

The sheets created are not too readable for audiences, so it transfers information to the [Master Schedule tab](https://docs.google.com/spreadsheets/d/1eCC9_43aua6a_YkqlNo_lh17zN3fFBxsDAmNnN1jnK0/edit?gid=1477006579#gid=1477006579). This sheet is for customizing the schedule to be displayed to the tourney participants. It takes in the information based on the pool name you enter into the yellow cell at the top, and then concatenates the team names into the match for that round and pool. The court column is a helper function for display only, and will not work logically for all scenarios (including matches with byes). Match number indicates the match unique to each pool, and the pool column indicates which pool that match takes place in (which is pulled from the ID column). The ID column and the round number columns are then used to pull the information from the generated schedule and concatenate the team names, showing the game for that round and match. 

My personal method when using the Master Schedule tab is to copy schedule onto another sheet and paste (using "Values Only") onto another. Then I customize it for personal needs, removing court numbers with bye matchups. You can also remove the match number and ID column as they are unnecessary. 

### Reporting Round Robin Results
As you can see, the tourney is set up where teams are placed in one of many pools. These pools are usually separated by skill level, and games are played to determine who is ranked higher/lower than their opponents. After a match, both teams submit their results in a [Google Form link](https://docs.google.com/forms/d/1WFWo_PO638oHvYKf0lf6X_orLddXfKGRRlKc0IMpPd8/edit). All they need to do is enter their team name, which round they played in, and the match result (which is three different questions).

### Assigning Seeds
As scores get reported, the Google Form data is transferred live to the spreadsheet in the [Responses tab](https://docs.google.com/spreadsheets/d/1eCC9_43aua6a_YkqlNo_lh17zN3fFBxsDAmNnN1jnK0/edit?gid=818500033#gid=818500033). This immediately transfers results to the different pool sheets, (e.g. [Pool A Scores](https://docs.google.com/spreadsheets/d/1eCC9_43aua6a_YkqlNo_lh17zN3fFBxsDAmNnN1jnK0/edit?gid=890974284#gid=890974284)), and dynamically updates each teams' standing in their own pool. Their pool standing is calculated based on their pool score, which is a sum of their wins multiplied by 20 and the points scored minus conceded. If teams win games by a large margin, then they are ranked higher. If they lose their games by a lot of points, then they are ranked lower. Nothing is needed to set up the Pool Score tabs: only if you use different names other than A, B, C, and D do you need to make adjustments (to do so, duplicate one of the tabs, change the top left yellow cell to the name desired. If you see team names go into the first column, that is good sign you set it up right. Change the sheet name to "Pool {name} Scores" when you are done to update the [Seed Calculations tab](https://docs.google.com/spreadsheets/d/1eCC9_43aua6a_YkqlNo_lh17zN3fFBxsDAmNnN1jnK0/edit?gid=673908820#gid=673908820)). 

Based on their pool score and standing, they are either promoted (for lower division pools) or demoted (from upper division pools). The teams sent to each bracket are then seeded based on their individual pool scores, now classified as the Power Ranking. Additionally, a placement feature is included for changes needed to teams sent to the upper or lower bracket. A single value above each pool (highlighted yellow) alters the teams that get promoted/demoted. To see the seed placement in action, you can view the [Seed Calculations tab](https://docs.google.com/spreadsheets/d/1eCC9_43aua6a_YkqlNo_lh17zN3fFBxsDAmNnN1jnK0/edit?gid=673908820#gid=673908820).

### Bracket Creation
When pool play is finished and teams are seeded, the [Upper and Lower Bracket Tabs](https://docs.google.com/spreadsheets/d/1eCC9_43aua6a_YkqlNo_lh17zN3fFBxsDAmNnN1jnK0/edit?gid=884757995#gid=884757995) positions the team names into their slots respective to the seed. When tournament matches finish, you can enter in the scored points for each team. The team name with more points gets placed automatically to the next round. A completed match is highlighted orange to green, and a ready match is highlighted red to orange. A major limitation of this bracket is it is restricted to a 16-man tourney: these brackets are built under a Google Sheets extension called ["Tournament Extension"](https://workspace.google.com/u/0/marketplace/app/tournament_extensions/684126244332), which can adjust the number of entries for a tourney. While the add-on isn't required for this sheet anymore due to my personal adjustments, it is useful for building your own tourney (for example, you can increase the number of slots, incorporate dates for matches, etc.). 

## How To Use It For Yourself
First of all, I would not claim this tool is fool proof since it was made to meet my needs in the moment (so its more "seasoned Excel user" proof). If it breaks anywhere, just use the undo button or re-copy it. 

1. Navigate to the [Google Drive Folder](https://drive.google.com/drive/folders/1psT-Cm-eqDbe9LxJ1c76snN0MBDgRRDh)
2. Duplicate the Tourney Manager Spreadsheet file onto your personal Google Drive. The Google Forms file "Pool Play Submissions" will also be duplicated and linked to the "Responses" tab of your duplicated sheets file. 
3. Follow the instructions in the "How To Use" tab for personal customization. 
4. For additional customization, such as adding a fifth pool or a third bracket, first ponder whether you really want to go through that kind of work. If you do, you can email me at [jxnpass@gmail.com](mailto:jxnpass@gmail.com) for guidance. However, if you are familiar with how Google Sheets and Excel work, I recommend taking the time to understand. If you do, you can figure it out.   

## Highlights and Credits
- [Bill Venables](https://github.com/BillVenables): author of the [round robin code in R](https://rdrr.io/github/BillVenables/WWRCourse/man/round_robin.html). 
- [YoRai Geffen](https://workspace.google.com/u/0/marketplace/app/tournament_extensions/684126244332): author of the tourney extensions add-on.
- [Kyler Curry](https://www.instagram.com/kyler.curry24/) and [Josh Hilton](https://www.instagram.com/7josh7hilton7/): framework for the seed calculations
- [Shawn McGarvin](https://www.facebook.com/people/Shawn-McGarvin/pfbid02bD55jMaMpmzGitaLG2SaGNKbY24DS9Are3Yi3VduwRShkXabCawULmT8a9ajM8VDl/) and [John Burton](https://www.instagram.com/bob_the_clarinet/): they are the hosts for the volleyball tournaments
- [Volleyball Homies](https://www.instagram.com/vb_homies/): budding Instagram account
- [Matthew Palmer](https://www.instagram.com/matthewpa1mer/): video and photography (check out his [drone shot video!](https://www.instagram.com/reel/DEWAMutyrEd/?utm_source=ig_web_copy_link&igsh=MzRlODBiNWFlZA==))
