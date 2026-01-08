# 📄 Automated Document Generation & Conversion

A vibe-coded Python project — plug in your data, hit run, and let the docs generate themselves 😌

This project automates the creation of personalized Word documents (`.docx`) from a template using data from a CSV file. It can also optionally convert those documents to PDF based on a simple boolean flag — powered by **LibreOffice (headless)**.

Perfect for letters, invoices, certificates, or any bulk document workflow.

---

## ✨ Features

* **Placeholder Replacement:** Dynamically replaces placeholders like `{{COLUMN_HEADER}}` in a Word template with CSV data.
* **Conditional PDF Conversion:** Uses a `PDF` boolean column to decide whether each document should be saved as `.docx` or converted to `.pdf`.
* **LibreOffice Integration:** Converts `.docx` → `.pdf` using LibreOffice in headless (terminal) mode.
* **Organized Output:** Automatically separates outputs into clean folders for DOCX and PDF files.
* **Error Handling:** Handles missing LibreOffice installs and conversion failures gracefully.
* **Zero-Friction Setup:** Auto-generates sample `data.csv` and `template.docx` if they don’t exist.

---

## 📦 Requirements

Make sure you have the following installed:

* **Python 3.x**
* **pandas**
    ```bash
    pip install pandas
    ```
* **python-docx**
    ```bash
    pip install python-docx
    ```
* **LibreOffice**
    * **On Debian/Ubuntu/Colab:**
        ```bash
        sudo apt-get install libreoffice-writer libreoffice-calc
        ```
    * **On other systems:** Install [LibreOffice](https://www.libreoffice.org/download/download/) manually.

---

## 🚀 How to Use

### 1️⃣ Prepare Your CSV File
Create a `data.csv` file. Each column header becomes a placeholder in the Word template. 

> [!IMPORTANT]
> Include a case-sensitive boolean column named **PDF**:
> * `True` → Convert to PDF
> * `False` → Keep as DOCX

```bash
**Example `data.csv`:**
| NAME | ADDRESS | AMOUNT | PDF |
| :--- | :--- | :--- | :--- |
| Alice | 123 Main St | 100.50 | True |
| Bob | 456 Oak Ave | 200.75 | True |
| Charlie | 789 Pine Ln | 150.00 | True |
| David | 101 Elm Rd | 300.25 | False |
```
### 2️⃣ Prepare Your Word Template
Create `template.docx` and insert placeholders using double curly braces. The placeholder names must **exactly match** your CSV headers.

```bash
**Example `template.docx` content:**
> ### Personalized Document
> Dear {{NAME}},
> 
> This document is personalized for you at {{ADDRESS}}.
> 
> The amount due is ${{AMOUNT}}.
```

### 3️⃣ Run the Script
Place the script, `data.csv`, and `template.docx` in the same directory, then run:

```bash
python main.py
```

🧠 Execution Flow
The script will automatically perform the following:

Check Environment: Verifies if LibreOffice is installed for PDF conversion.

Load Data: Reads the data.csv file.

Generate Documents: Iterates through each row, replacing {{placeholders}} in the template.

Conditional PDF Conversion: If the PDF column is True, it triggers the LibreOffice headless converter.

Clean Up: Removes temporary files and organizes final versions.



📁 Output Structure
After running the script, your directory will be organized as follows:

Plaintext

project-folder/
│── main.py
│── data.csv
│── template.docx
├── output_documents_docx/   <-- Contains all generated .docx files
│   ├── document_1.docx
│   └── document_2.docx
└── output_documents_pdf/    <-- Contains all successfully converted PDFs
    ├── document_1.pdf
    └── document_2.pdf
DOCX folder: Contains all .docx files and any temporary files if conversion fails.

PDF folder: Contains all successfully converted PDFs.

💫 Final Notes
Works great in Google Colab, Linux servers, and local machines.

Easy to extend for email sending, branding, or batch workflows.

Built to be practical, flexible, and just a little bit ✨extra✨.
