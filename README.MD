# CTK Forensic Search - Economic and Financial Crime Triage

This repository contains a set of custom tools for **KAPE (Kroll Artifact Parser and Extractor)**, specifically designed to optimize evidence collection and triage in economic and financial crime investigations.

## 📌 Overview

The tools provided here aim to bridge the gap in the selective acquisition of financial artifacts. They allow forensic examiners to perform rapid on-scene triage and determine data relevance before committing to full system seizures.

### Repository Content
* **Targets (`.tkape`)**: Focused on collecting Office productivity documents and financial databases.
* **Modules (`.mkape`)**: Automation for email extraction and advanced keyword searching.
* **Binary (`ctk_search.exe`)**: A standalone search engine developed in Python, optimized for forensic data volumes.

---

## 🛠️ Installation

1.  Copy the files from the `Targets` folder to `KAPE\Targets\Custom`.
2.  Copy the files from the `Modules` folder to `KAPE\Modules\Custom`.
3.  Copy the `bin\ctk_search` folder to `KAPE\Modules\bin\`.
4.  Ensure `readpst.exe` is present in the `bin\readpst` folder for email extraction modules to function correctly.

---

## 🚀 Usage and Arguments

The `ctk_search.exe` engine introduces two critical operational modes for field efficiency:

* **`--fast`**: Implements volume filters, ignoring Office files > 10MB and databases > 20MB. Ideal for ultra-rapid initial triage.
* **`--deep`**: Performs an exhaustive binary search across all triaged files, including files without clear extensions and extracted email data.



### Output Format (CSV)
Results are exported with the following fields to ensure forensic auditability:
* `Status`: Indicates a match found (MATCH).
* `Keyword`: The specific identified keyword.
* `Extension`: Original extension of the analyzed file.
* `SHA1`: SHA1 hash of the file for integrity verification.
* `Path`: Absolute path of the file within the evidence.

---

## 📜 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details. This license allows for academic, professional, and commercial use, provided that original authorship is attributed.

## 🎓 Citation

If you use these tools in your research or forensic work, please cite as follows:

> *[Bruno Cardoso & Paulo Gondar / CTK Kape Forensic Search] (2025). CTK Forensic Search: KAPE Integration for Economic Crime Investigation. GitHub Repository.*

---

## 🛡️ Integrity
| File | SHA256 Hash |
| :--- | :--- |
| `ctk_search.exe` | `[0d8463afa6fe6315dd03e0a8f2bd78d66e1d1f408b5345725e1a3b08062d3dce]` |