---
title: "About"
menu:
  main:
    weight: 10
---

>For the professional, one's meez is an obsession, one's sword and shield, the only thing standing between you and chaos. If you have your meez right, it means you have your head together, you are "set up", stocked, organized, ready with everything you need and are likely to need for the tasks at hand.

— Anthony Bourdain, *Le Halles Cookbook*

Qualitative scientists use a variety of methods for analyzing their data. Some of these are informal and specialized to the task and researcher, and others rely upon a paradigm long-established and reliant upon software to complete successfully. Computer-assisted qualitative data analysis software is largely proprietary and closed, obscuring project files into obscure objects that bind the researcher to that software, as well as providing an excess of features that force a steep learning curve. The open source alternatives narrowly focus on a particular discipline or type of data, poorly supported, or have a steep learning curve. [Mise](https://en.wikipedia.org/wiki/Mise_en_place) fills the gap between the highly functional, but closed and proprietary software packages, and the narrow open source software.

Mise is open source, free to use and extend, and capable of running on macOS, Linux, and Windows. It keeps your data in open formats that will endure indefinitely, and the design of Mise keeps you as close to your data as possible. Further, it is not bloated with features or narrow functions. If you have used Atlas.ti, Nvivo, or Dedoose before, you will quickly be able to take up and use Mise.

## Design Principles

1. **You control *your* data**

Mise is designed with a plain text paradigm of completing research in mind, and keeps your project files in a standard `.txt`. Document, tags, and coded segments of documents are stored in a SQLite database whose organization is legible and explicit to the end-user.

2. **Simplicity first**

Mise's design is straightforward, and encourages the qualitative coder to assign mutually exclusive tags to segments of text. This is a methodological decision not simply for software, but for the generative process of engaging in the coding process. Further, nested codes are confined to a parent-child relationship, where a parent code can have many child, or sub-codes, but child codes have no progeny.

3. **Portability**

Mise is meant to be accessible regardless of the specific OS you use. Windows, macOS, and Linux are included, and the open-source format for data storage means that it can be stored in a cloud service for collaboration.

For more information about the specific design choices made in the development of Mise, please see the [Documentation]({{< relref "documentation.md" >}}) page.