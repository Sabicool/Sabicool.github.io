+++
title = "2022 Study Plan Part 1"
author = ["Sabiqul Hoque"]
date = 2022-01-16
lastmod = 2022-01-17T19:14:48+08:00
categories = ["Productivity"]
draft = false
tags = ["Study", "Workflow", "Template"]
+++

This will be a series of blog posts about my planned study methodology for the coming semester of 2022. That being said, it'll likely change throughout the semester.

TLDR: [Here is a link](https://sabsblogstudy.notion.site/) to my notion setup listing the LOs and PBLs, making it easy to see my progress in each PBL, how well I know each LO and when I last studied a particular topic.


## Background {#background}

I realised after writing this blog post that I should give some background to the terms and structure of my university course. Each week we are given a PBL on some broad topic (e.g. gastrooesphageal reflux disease). Within this PBL are specific learning objectives (LOs) which relate to the broader PBL topic but are more specific (e.g. embryology of the oesaphagus).


## The Idea {#the-idea}

Last year I figured just learning the topics in a broad and comprehensive manner would be best. While that did work, there were a few topics that I definitely felt as though I could have covered more. In essence, what I figured was that I gave an equal amount of attention to all topics instead of catering it to my strengths and weaknesses.

What I'd like to do this year is actually have a list of all the LOs and PBLs, when I last reviwed them and how comfortable I am with the topic, so that when I do decide to sit down and do some revision, I can look through this table and easily decide. While I've traditionally done this in google sheets[^fn:1], I figured I might try do it in [notion](https://www.notion.so/) this time round. The reason for this change is mainly aesthetic purposes but also functional purposes. A list of all the LOs with all the PBLs lends itself to being better suited for a database where each row is its own item as opposed to a spreadsheet, making notion the better choice.

I have also set something up like this in notion before. The only problem with that it had far too many features to make it useful. It combined a master todo list, areas and goals list with my notes on lectures, LOs and entire PBLs. It became too large to work through and too cumbersome very quickly.

<a id="orgd8b2cb2"></a>

{{< figure src="/ox-hugo/oldstudynotion.png" caption="Figure 1: This was the old setup for reference. From the left to the right the columns are: unit, name, whether flashcards were created, completion status of the relevant tasks, strength regarding that topic, how many days ago it was reviewed and the next task for that topic. There were too many features for this method to be sustainable." >}}

The setup will involve two databases, one with a list of all the LOs and one with a list of all the PBLs.

<div class="ox-hugo-table sane-table">
<div></div>
<div class="table-caption">
  <span class="table-number">Table 1</span>:
  Table with verbatim CSS
</div>

| LO                        | PBL         | Strength | Last Reviewed |
|---------------------------|-------------|----------|---------------|
| Embryology of the foregut | PBL 1: GERD | 3        | 05-01-2022    |
| ...                       | ...         | ...      | ...           |

</div>

The other would be a list of PBLs

| PBL     | Block            | Last Reviewed | Progress  |
|---------|------------------|---------------|-----------|
| 1: GERD | Gastrointestinal | `formula`     | `formula` |
| ...     | ...              | ...           | ...       |

Here the formulas would show the date of the most recently reviewed LO and the average strength of the PBL based on the individual strength of each LO in particular.


## The Setup {#the-setup}

I've made the basic layout of the notion setup public and its available at [https://sabsblogstudy.notion.site/](https://sabsblogstudy.notion.site/) for you to duplicate.

<a id="orgc14dfef"></a>

{{< figure src="/ox-hugo/LOs.png" caption="Figure 2: The LOs database. From left to right the columns are strength (i.e. how well I know the topic), followed by the PBL column which shows the broader topic it is connected to, followed by the name of the LO in question, when I last studied it and finally when I plan to study it again." >}}

Sincec each row of the LO database is a page, notes can be added to each LO if I so wish. At this moment before the semester has started they are all empty but it is a proof of concept for now.

<a id="orgb4e83f2"></a>

{{< figure src="/ox-hugo/PBLs.png" caption="Figure 3: The PBLs database. From left to right the columns are the PBL in question, what block it is part of, the list of LOs, the earliest date of the LOs studied and the progress in completing that PBL (based on how many LOs are at their full strength)" >}}


## Formulas {#formulas}

The user inputs a strength for the LO using the coloured circle dropdown menu (see Figure 1, column 1). This is converted to a number from 0 to 1 using the following formula:

```nil
if(prop("Strength") == "🔴", .2, if(prop("Strength") == "🟠", .4, if(prop("Strength") == "🟡", .6, if(prop("Strength") == "🟢", .8, if(prop("Strength") == "🟣", 1, 0)))))
```

<div class="src-block-caption">
  <span class="src-block-number">Code Snippet 1</span>:
  Sorry about it being 1 line, its not my fauly notion formulas don't allow multi-line input
</div>

From here, the PBL database uses a rollup configured to evaluate the sum of the formula above. The maximum strength of the PBL is calculated using a rollup that just counts the number of LOs there are (since each LO can have a maximum of 1 for its strength).

The progress bar is generated using the following formula:

```nil
if(not empty(prop("Complete Value")) and not empty(prop("Maximum Strength")), slice("——————————", 0, floor(10 * prop("Complete Value") / prop("Maximum Strength"))) + "●" + slice("——————————", 0, 10 - floor(10 * prop("Complete Value") / prop("Maximum Strength"))) + " " + format(floor(100 * prop("Complete Value") / prop("Maximum Strength"))) + "%", "")
```

[^fn:1]: To see my year 2 semester 1 google sheets [see here](https://docs.google.com/spreadsheets/d/e/2PACX-1vQa8zHZeeOMM3oRqqtUe1okm5rckCrstfYty510t5Dd%5FKFvItEvVnYallPG1oSiACOCGzguSzVpu9UX/pubhtml#)
