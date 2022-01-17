+++
title = "Academic Orgmode Workflow"
author = ["Sabiqul Hoque"]
date = 2021-12-25
lastmod = 2022-01-17T17:48:12+08:00
categories = ["Notetaking"]
draft = false
tags = ["Emacs", "Research", "Workflow"]
+++

## Background {#background}

One of my goals for next year (apart from writing more blog posts) is to also read more academic material and journal articles. In an effort to streamline the process of finding new articles[^fn:1], reading, notetaking and forming new ideas, I'm making an effort to write this blog in order to consolidate the process for me (while hopefully providing some value to you, the reader). This blog post will likely remain a work in progress and change with time. On another note, while my configuration is not yet public, I'm using what's recommended in the packages' respective read-me pages.

I preface this entry to also make the point that much of this workflow depends on Emacs. While I explain my workflow in such a way that it can be understood by someone not using Emacs (and perhaps even implemented in something easier to use like Obsidian, OneNote or Notion[^fn:2]), I would like to point out that setting up Emacs on your machine and customising it is not covered.


## Reference Management {#reference-management}

For reference management I use Zotero. Its my preferred because of the way it is able to integrate with the rest of my workflow using better-bibtex[^fn:3]. This add-on allows me to have a single file in which all of my bibliography entries can be stored and indexed.

The other benefit is the ability to clip websites easily using an extension or by sharing it to the Zotero app on iPad or zoo for Zotero app on Android. I previously was a fan of Mendeley, until they removed support for their iPad app and brought in a paid model. Endnote is recommended by my university and I've used it a bit, but not enough for me to bother switching.

For the purpose of this blog post I shall be looking at <see;&heyConceptClinicalEquipoise2017;for examples>. Capturing it requires me to click on the add-on to add it to my Zotero library.

<a id="org4fbaa69"></a>

{{< figure src="/ox-hugo/bmj.png" caption="Figure 1: Save to Zotero add-on available for firefox and chrome makes it possible to easily add references from the browser to Zotero while capturing relevent metadata" >}}

This captures it into my .bib file as below with all the correct formatting. Importantly, it requires almost zero edits afterwards to make sure the metadata is correct. Furthermore, it also downloads the PDF (useful later).

```nil
@article{heyConceptClinicalEquipoise2017,
  title = {Is the Concept of Clinical Equipoise Still Relevant to Research?},
  author = {Hey, Spencer Phillips and London, Alex John and Weijer, Charles and Rid, Annette and Miller, Franklin},
  date = {2017-12-28},
  journaltitle = {BMJ},
  shortjournal = {BMJ},
  volume = {359},
  eprint = {29284666},
  eprinttype = {pmid},
  pages = {j5787},
  publisher = {{British Medical Journal Publishing Group}},
  issn = {0959-8138, 1756-1833},
  doi = {10.1136/bmj.j5787},
  url = {https://www.bmj.com/content/359/bmj.j5787},
  urldate = {2021-12-20},
  abstract = {{$<$}p{$>$}\textbf{Spencer Hey}, \textbf{Alex John London}, and \textbf{Charles Weijer} argue that there is no better framework for justifying patient participation in research. But \textbf{Annette Rid} and \textbf{Franklin Miller} say that it is a mistake to require clinical research ethics to align with the norms of clinical practice{$<$}/p{$>$}},
  langid = {english},
  file = {/home/sabiqul/Zotero/storage/FUW9DW8T/Hey et al. - 2017 - Is the concept of clinical equipoise still relevan.pdf;/home/sabiqul/Zotero/storage/4JQTHAZS/bmj.html}
}
```


## Notetaking {#notetaking}

For notetaking, I take notes on Emacs org-mode[^fn:4] and so the packages I use for notetaking I use include:

Org-ref
: referencing and managing my bibliography in Emacs

Org-noter
: note taking on PDFs

Org-roam
: making connections between different notes and ideas

In essence the note taking process is 3 fold. Step 1 is taking direct notes from the PDF itself and often directly quoting the text with the main aim being to write the main details from the text. Step 2 is to write your own notes and interpretation on these notes as you see fit. In particular for this article it would be relevant to discuss say previous experiences or what to keep in mind for the future (i.e. what you have learnt or can reflect on, now having read the article). Finally, step 3, for this example, I would write a brief few points on what I've learnt from the topic in my summary notes on clinical equipoise. This summary note would therefore not only form a cohesive document containing opinions and studies from multiple journal articles but would also contain potentially my own thoughts and reflections as well. Most importantly I can make cool node graphs to show the hierachial and linking nature of the notes.


### Step 1: Direct Notes from the Journal Article {#step-1-direct-notes-from-the-journal-article}

I would run the command `ivy-bibtex` which pulls up a list of my bibliography entries for me to select and choose from. I can pull up the PDF and to take notes on it I run the command `org-noter`.

{{< figure src="/ox-hugo/ivybibtex.png" caption="Figure 2: Calling ivy-bibtex opens a searchable window of all references. The snowflake icon shows whether a PDF is available to take notes on. Other fields can be shown if desired." >}}

I can then run the command `org-noter-insert-precise-note` to add notes and populate the org notes buffer as I please. Generally I try and constrain this document to just the information that is in the document[^fn:5]. In essence its just to record whatever new information you have found in this document.

{{< figure src="/ox-hugo/orgnoter.png" caption="Figure 3: Re-colourised PDF on the left (for easier reading) and notes on the right." >}}

{{< figure src="/ox-hugo/orgnoter2.png" caption="Figure 4: Completed direct notes using mainly quotes. Org-noter makes it possible to link each heading to a specific point in the PDF making the PDF sync to what's unfolded on the right side." >}}


### Step 2: Reflective Notes {#step-2-reflective-notes}

As stated earlier, this is a place for me to reflect on what I've learnt from reading this article. Linking to other points/topics if necessary.

{{< figure src="/ox-hugo/reflectivenotes.png" caption="Figure 5: Reflective notes open on the left with direct notes open in the middle. On the far right side is the backlinks buffer which shows what other documents I've referenced the reflective notes in." >}}


### Step 3: Incorporation into the Topic Notes {#step-3-incorporation-into-the-topic-notes}

I often write for the purpose of writing just literature notes. So these topic notes often just end up being prose summaries of the topic with multiple references and so forth. This note will likely be something you reference and restructure every now and then as you read and understand more about the topic.

{{< figure src="/ox-hugo/topicnotes.png" caption="Figure 6: The notes on the topic where I cite different sources. You can have a read of these notes, but they're just for display purposes. Not near finished at all." >}}


### Step 4: Cool Graphs {#step-4-cool-graphs}

Running `org-roam-ui-mode` will produce nice graphs of all my notes and allow me to filter out notes based on different parameters. Most importantly you can make nice graphs like this and even 3D graphs. I recommend taking a look at their [github page for more information](https://github.com/org-roam/org-roam-ui).

{{< figure src="/ox-hugo/graph.png" caption="Figure 7: A small part of the complete graph of all my notes showing only those relevant to clinical equipoise" >}}

As you can imagine, I was under the conception that a graph of my notes and how they link to each other would provide some grand new novel ideas. I am yet to prove this correct and so the graphs for me provide no purpose other than looking nice.


## Improvements {#improvements}

I am looking to using the package org-transclusion in the future. This package makes roam like portals between documents where editing information in one document changes it elsewhere as well.


## Conclusion {#conclusion}

Feel free to make use of whatever you can from this for your personal benefit. I would like to again point out that this workflow is perhaps not Emacs specific (maybe apart from the graphs part), and so could potentially be implemented in something more user friendly such as Notion, OneNote or even Google Docs for that matter.


## Useful Links and References: {#useful-links-and-references}

-   [An Orgmode Note Workflow by Rohit Goswami](https://rgoswami.me/posts/org-note-workflow/#fn:4)
-   [Academic Doom-Emacs Config by Sunny Hasija](https://github.com/sunnyhasija/Academic-Doom-Emacs-Config)

[^fn:1]: Though I don't have a concrete way of doing this other than RSS feeds, subscriptions and search engines.
[^fn:2]: From my personal experience I believe it is easiest to replicate this workflow using Obsidian. Its also far more user friendly and perhaps has more entry level features than what Emacs provides
[^fn:3]: Or even with word processors using an add-on.
[^fn:4]: I hope to write about why I use Emacs org-mode in the future
[^fn:5]: However selecting what information is relevant is entirely dependent on your purpose for reading that article (which you must decide before reading it). In my case, I figured learning about clinical equipoise would be relevant when designing my own study in the future.
