# Usage Guide: CTK Forensic Search for KAPE

This guide explains how to use the custom Targets and Modules developed for economic and financial crime investigations using KAPE.

## 1. Workflow Overview

The toolset follows a three-step forensic process:
1.  **Acquisition (Targets):** Selective collection of financial and office documents.
2.  **Extraction (Modules):** Conversion of email databases (PST/OST) into searchable formats.
3.  **Analysis (Modules):** Keyword searching using the `ctk_search.exe` engine with optimized performance modes.

---

## 2. Target Selection (Data Collection)

When running KAPE, select the following Targets to gather relevant financial evidence:

* **CTK_OfficeDocumentsUsers**: Use this to collect productivity files (`.docx`, `.pdf`, `.xlsx`, etc.) from user profiles.
* **CTK_FinancialDocumentsUsers**: Use this to collect specific financial artifacts, including accounting databases (`.sqlite`, `.db`), SAF-T files, and email containers (`.pst`, `.ost`).

---

## 3. Module Configuration (Processing)

### Email Extraction
Before searching, you must run the **CTK_EmailKeywordExtract** module. 
* **Requirement:** Ensure `readpst.exe` is located in `KAPE\Modules\bin\readpst\`.
* **Function:** It converts Outlook files into individual `.eml` or `mbox` files for keyword indexing.

### Keyword Searching (`ctk_search.exe`)
The core analysis is performed by two modules that invoke the `ctk_search.exe` engine. You must place your keyword list in `KAPE\Keywords\keywords.txt`.

#### A. Office and General File Search (Fast Mode)
**Module:** `OfficeSearch_Gondar`
* **Command:** `--fast`
* **Logic:** Optimized for speed on live systems. It skips Office documents larger than **10MB** and Databases larger than **20MB**.
* **Best Use:** Initial triage to find "low-hanging fruit" without locking the system or consuming excessive RAM.

#### B. Email and Deep Search (Deep Mode)
**Module:** `CTK_EmailKeywordSearch`
* **Command:** `--deep`
* **Logic:** No file size restrictions. It performs a comprehensive binary and text search across all extracted emails and triaged files.
* **Best Use:** Thorough investigation where missing a single keyword hit could compromise the case.

---

## 4. Understanding the Results

All search modules output a **CSV report** (e.g., `FinancialSearchHits.csv`) in the destination folder. Each hit includes:

| Column | Description |
| :--- | :--- |
| **Status** | Confirmation of the hit (e.g., MATCH). |
| **Keyword** | The specific term found from your `keywords.txt`. |
| **Extension** | The file type where the hit was found. |
| **SHA1 Hash** | The forensic hash of the file for chain of custody. |
| **Path** | The full path to the evidence file. |

---

## 5. Troubleshooting

* **No hits found?** Check if `keywords.txt` is encoded in UTF-8 and contains one keyword per line.
* **Module Error?** Verify that `ctk_search.exe` is in `KAPE\Modules\bin\ctk_search\`.
* **PST not processing?** Ensure the `CTK_EmailKeywordExtract` ran successfully before the search module, as the search engine cannot read encrypted/locked PST files directly.

---
*Developed by BRC / Gondar as part of a Master's Research Project in Digital Forensics.*