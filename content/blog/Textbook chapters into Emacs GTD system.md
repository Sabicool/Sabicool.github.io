+++
title = "Adding textbook chapters to GTD system in Emacs"
author = ["Sabiqul Hoque"]
date = 2023-09-23
lastmod = 2023-09-24T00:19:17+08:00
categories = ["Productivity"]
draft = false
tags = ["Emacs", "Workflow"]
+++

This is a small blog post on my use-case for a small function.

I often find myself extracting the chapter names from a PDF opened inside of [org-noter](https://github.com/weirdNox/org-noter) using the function `org-noter-create-skeleton` or `org-noter-pdftools-create-skeleton`. I then tend to mark which chapters and sections need to be read by setting a todo state to them (such as READ).

The following function pulls all marked headings with the specific TODO keyword in question into a new buffer and calls `org-gtd-clarify-item` from the [org-gtd](https://github.com/Trevoke/org-gtd.el) package.

```emacs-lisp
(defun my/get-org-headings-with-todo (todo-keyword project-title)
  "Get all Org mode headings with a specific TODO keyword and insert them into a org-gtd-clarify-buffer."
  (interactive "sTODO keyword: \nsProject title: ")
  (let* ((headings-buffer (generate-new-buffer "*New Project*"))
         (org-headings (save-excursion
                         (goto-char (point-min))
                         (cl-loop while (re-search-forward (format "^\*+\\s-+\\(%s\\)\\s-+" todo-keyword) nil t)
                                  collect (org-get-heading t t t t)))))
    (with-current-buffer headings-buffer
      (org-mode)
      ;(insert "* Test Headings\n")
      (insert (concat "* " project-title "\n"))
      (dolist (heading org-headings)
        (insert (format "** %s\n" heading))))
    (switch-to-buffer headings-buffer)
    (goto-char (point-min))
    (org-gtd-clarify-item)
    (kill-buffer headings-buffer)))
```

This is the particular version that I tend to prefer over the generic form above.

```emacs-lisp
(defun my/turn-read-headings-into-project (project-title)
  "Get all Org mode headings with READ keyword and insert them into org-gtd-clarify buffer."
  (interactive "sProject title: ")
  (let* ((headings-buffer (generate-new-buffer "*New Project*"))
         (org-headings (save-excursion
                         (goto-char (point-min))
                         (cl-loop while (re-search-forward (format "^\*+\\s-+\\(%s\\)\\s-+" "READ") nil t)
                                  collect (org-get-heading t t t t)))))
    (with-current-buffer headings-buffer
      (org-mode)
      ;(insert "* Test Headings\n")
      (insert (concat "* " project-title "\n"))
      (dolist (heading org-headings)
        (insert (format "** Chapter: %s\n" heading))))
    (switch-to-buffer headings-buffer)
    (goto-char (point-min))
    (org-gtd-clarify-item)
    (kill-buffer headings-buffer)))
```
