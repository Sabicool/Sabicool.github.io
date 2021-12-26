+++
title = "Academic Orgmode Workflow"
date = 2021-12-25
lastmod = 2021-12-27T04:36:49+08:00
categories = ["notetaking"]
draft = false
tags = ["Emacs", "Research", "Workflow"]
+++

## Background {#background}

One of my goals for next year (apart from writing more blog posts) is to also read more academic material and journal articles. In an effort to streamline the process of finding new articles[^fn:1], reading, notetaking and forming new ideas, I'm making an effort to write this blog in order to consolidate the process for me (while hopefully providing some value to you, the reader). This blog post will likely remain a work in progress and change with time. On another note, while my configuration is not yet public, I'm using what's recommended in the packages' respective readme pages.

I preface this entry to also make the point that much of this workflow depends on Emacs. While I explain my workflow in such a way that it can be understood by someone not using Emacs (and perhaps even implemented in something easier to use like OneNote or Notion), I would like to point out that setting up Emacs on your machine and customising it is not covered.


## Reference Management {#reference-management}

For reference management I use Zotero. Its my preferred because of the way it is able to integrate with the rest of my workflow using better-bibtex[^fn:2]. This addon allows me to have a single file in which all of my bibliography entries can be stored and indexed.

The other benefit is the ability to clip websites easily using an extension or by sharing it to the zotero app on iPad or zoo for zotero app on Android. I previously was a fan of Mendeleey, until they removed support for their iPad app and brought in a paid model. Endnote is recommended by my university and I've used it a bit, but not enough for me to bother switching.

For the purpose of this blog post I shall be looking at [this article on clinical equipoise in research](https://www.bmj.com/content/359/bmj.j5787). Capturing it requires me to click on the addon to add it to my zotero library.

{{< figure src="/ox-hugo/bmj.png" >}}

This captures it into my .bib file as below with all the correct formatting. Importantly, it requires almost zero edits afterwards to make sure the metadata is correct. Furthermore, it also downloads the pdf (useful later).

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

For notetaking, I take notes on Emacs org-mode[^fn:3] and so the packages I use for notetaking I use include:

Org-ref
: referencing and managing my bibliography in Emacs

Org-noter
: note taking on PDFs

Org-roam
: making connections between different notes and ideas

In essence the note taking process is 3 fold. Step 1 is taking direct notes from the PDF itself and often directly quoting the text with the main aim being to write the main details from the text. Step 2 is to write your own notes and interpretation on these notes as you see fit. In particular for this article it would be relevant to discuss say previous experiences or what to keep in mind for the future (i.e. what you have learnt or can reflect on, now having read the article). Finally, step 3, for this example, I would write a brief few points on what I've learnt from the topic in my summary notes on clinical equipoise. This summary note would therefore not only form a cohesive document containing opinions and studies from multiple journal articles but would also contain potentially my own thoughts and reflections as well. Most importantly I can make cool node graphs to show the hierachial and linking nature of the notes.


### Step 1: Direct Notes from the Journal Article {#step-1-direct-notes-from-the-journal-article}

I would run the command `ivy-bibtex` which pulls up a list of my bibliography entries for me to select and choose from. I can pull up the PDF and to take notes on it I run the command `org-noter`.

{{< figure src="/ox-hugo/ivybibtex.png" >}}

I can then run the command `org-noter-insert-precise-note` to add notes and populate the org notes buffer as I please. Generally I try and constrain this document to just the information that is in the document[^fn:4]. In essence its just to record whatever new information you have found in this document.

{{< figure src="/ox-hugo/orgnoter.png" >}}

{{< figure src="/ox-hugo/orgnoter2.png" >}}


### Step 2: Reflective Notes {#step-2-reflective-notes}

As stated earlier, this is a place for me to reflect on what I've learnt from reading this article. Linking to other points/topics if necessary.

{{< figure src="/ox-hugo/reflectivenotes.png" >}}


### Step 3: Incorporation into the Topic Notes {#step-3-incorporation-into-the-topic-notes}

I often write for the purpose of writing just literature notes. So these topic notes often just end up being prose summaries of the topic with multiple references and so forth. This note will likely be something you reference and restructure every now and then as you read and understand more about the topic.

{{< figure src="/ox-hugo/topicnotes.png" >}}


### Step 4: Cool Graphs {#step-4-cool-graphs}

Running `org-roam-ui-mode` will produce nice graphs of all my notes and allow me to filter out notes based on different parameters. Most importantly you can make nice graphs like this and even 3D graphs. I recommend taking a look at their [github page for more information](https://github.com/org-roam/org-roam-ui).

{{< figure src="/ox-hugo/graph.png" >}}

As you can imagine, I was under the conception that a graph of my notes and how they link to each other would provide some grand new novel ideas. I am yet to prove this correct and so the graphs for me provide no purpose other than looking nice.


## Improvements {#improvements}

I am looking to using the package org-transclusion in the future. This package makes roam like portals between documents where editing information in one document changes it elsewhere as well.


## Conclusion {#conclusion}

Feel free to make use of whatever you can from this for your personal benefit. I would like to again point out that this workflow is perhaps not Emacs specific (maybe apart from the graphs part), and so could potentially be implemented in something more user friendly such as Notion, OneNote or even Google Docs for that matter.


## Useful Links and References: {#useful-links-and-references}

-   [An Orgmode Note Workflow by Rohit Goswami](https://rgoswami.me/posts/org-note-workflow/#fn:4)
-   [Academic Doom-Emacs Config by Sunny Hasija](https://github.com/sunnyhasija/Academic-Doom-Emacs-Config)

[^fn:1]: Though I don't have a concrete way of doing this other than RSS feeds, subscriptions and search engines.
[^fn:2]: Or even with word processors using an addon.
[^fn:3]: I hope to write about why I use Emacs org-mode in the future
[^fn:4]: However selecting what information is relevant is entirely dependent on your purpose for reading that article (which you must decide before reading it). In my case, I figured learning about clinical equipoise would be relevant when designing my own study in the future.
