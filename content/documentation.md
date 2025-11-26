---
title: "Documentation"
---

keeps your project files in a standard `.txt` format. Documents, tags, and coded segments of documents are stored in a SQLite database whose organization is legible, explicit, and published to the end-user.

Work in Mise is organized around "projects", containers for documents, the project database, configuration files and metadata related to the coding and analysis being done. Each project should contain a discrete collection of data from a specific social scientific intervention.

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

```SQL
CREATE TABLE documents (
    id                INTEGER PRIMARY KEY,
    original_filename TEXT,
    display_name      TEXT NOT NULL,
    text_path         TEXT NOT NULL,
    created_at        TEXT NOT NULL,
    doc_uuid          TEXT UNIQUE NOT NULL
);
```

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

```SQL
CREATE TABLE codes (
    id          TEXT PRIMARY KEY,
    label       TEXT NOT NULL,
    parent_id   TEXT REFERENCES codes(id),
    description TEXT,
    color       TEXT,
    sort_order  INTEGER
);
```

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

```SQL
CREATE TABLE coded_segments (
    id            INTEGER PRIMARY KEY AUTOINCREMENT,
    document_id   INTEGER NOT NULL REFERENCES documents(id),
    code_id       TEXT NOT NULL REFERENCES codes(id),
    start_offset  INTEGER NOT NULL,
    end_offset    INTEGER NOT NULL,
    memo          TEXT,
    created_at    TEXT NOT NULL
);
```