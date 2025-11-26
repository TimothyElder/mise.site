---
title: "Documentation"
---

## Core Design

The core design principle of Mise is to intentionally organize data to promote the cognitive task of creating and assigning analytic codes to qualitative material. Data is kept in as accessible a format as possible and project data is never obscured by elaborate or obtuse storage schemes.

Specifically, the text to be analyzed, imported from `.docx`, `.pdf` and `.md` files, are stored in a standard `.txt` format, so source files are never touched during analysis. Document metadata, tags, and coded segments of documents are stored in a SQLite database whose organization is legible, explicit, and published to the end-user.

Conceptually, you can think of Mise as a thin software layer that sits atop a more substantial layer that organizes data, functioning as an API that allows the user to create relationships between codes and text, and then examine these relationships systematically.

## Projects

Work in Mise is organized around “projects”, containers for documents, the project database, configuration files and metadata related to the coding and analysis being done. Each project should contain a discrete collection of data from a specific social scientific intervention.

Every project in Mise follows this schema:

```
my_project.mise/
    project.db         # SQLite, main metadata
    memos/             # Project memos
        memo_1.md
    texts/
        doc_0001.txt   # normalized UTF-8 text
        doc_0002.txt
    meta/
        codebook.json  # optional export/import format
        config.json    # view prefs, etc.
    .mise              # Software internal information
```

All information related to codes, the relationship of codes to documents, and document information is stored in an SQLite database.

## Database Schema

One of the primary differences between Mise and proprietary QDA software is that Mise uses an intelligible and transparent schema for organizing data in the database. The data base for all project information has three tables: "documents", "codes", and "coded_segments", storing information about the documents being analyzed, the codes used to analyze them, and the relationship between the two respectively.

### `documents` table 

Documents are the units of data that are being analyzed in Mise and can include interview transcripts, ethnographic field notes, or any other long form textual file with qualitative data in it. Documents on import into Mise are converted from their original format into `.txt` format, so they can be preserved in a legible and stable format.

| Column            	| Type    	| Description                                                               	|
|-------------------	|---------	|---------------------------------------------------------------------------	|
| id                	| Integer 	| Canonical unique document ID                                              	|
| original_filename 	| Text    	| The filename on import into the project                                   	|
| display_name      	| Text    	| Name displayed to user, editable                                          	|
| text_path         	| Text    	| Path to where the document is stored in /texts directory                  	|
| created_at        	| Text    	| Date document created in project                                          	|
| doc_uuid          	| Text    	| Universally Unique Identifier for export, import, and merging of projects 	|

### `codes` table

Codes are the analytic objects assigned to documents in the course of creating a structured analytical framework in the project.

| Column      	| Type    	| Description                                                    	|
|-------------	|---------	|----------------------------------------------------------------	|
| id          	| Text    	| Canonical unique code ID                                       	|
| label       	| Text    	| Code name, editable                                            	|
| parent_id   	| Text    	| Code id of parent code, for sub/child codes                    	|
| description 	| Text    	| User inputed code description (optional)                       	|
| color       	| Text    	| Color associated with code for segment highlighting (optional) 	|
| sort_order  	| Integer 	| Order in which codes appear                                    	|

### `coded_segments` table

"Coded segments" are the relationships between codes and documents.

| Column       	| Type    	| Description                            	|
|--------------	|---------	|----------------------------------------	|
| id           	| Integer 	| Canonical unique segment ID            	|
| document_id  	| Text    	| ID of document segment belongs to      	|
| code_id      	| Text    	| ID of code associated with segment     	|
| start_offset 	| Integer 	| Index in document where segment begins 	|
| end_offset   	| Integer 	| Index in document where segment ends   	|
| memo         	| Text    	| Order in which codes appear            	|
| created_at   	| Text    	| Date the segment was created           	|