📄 Automated Document Generation & Conversion

A vibe-coded Python project — plug in your data, hit run, and let the docs generate themselves 😌

This project automates the creation of personalized Word documents (.docx) from a template using data from a CSV file.
It can also optionally convert those documents to PDF based on a simple boolean flag — powered by LibreOffice (headless).

Perfect for letters, invoices, certificates, or any bulk document workflow.

✨ Features

Placeholder Replacement
Dynamically replaces placeholders like {{COLUMN_HEADER}} in a Word template with CSV data.

Conditional PDF Conversion
Uses a PDF boolean column to decide whether each document should be saved as .docx or converted to .pdf.

LibreOffice Integration
Converts .docx → .pdf using LibreOffice in headless (terminal) mode.

Organized Output
Automatically separates outputs into clean folders for DOCX and PDF files.

Error Handling
Handles missing LibreOffice installs and conversion failures gracefully.

Zero-Friction Setup
Auto-generates sample data.csv and template.docx if they don’t exist.

📦 Requirements

Make sure you have the following installed:

Python 3.x

pandas

pip install pandas


python-docx

pip install python-docx


LibreOffice

On Debian/Ubuntu/Colab:

sudo apt-get install libreoffice-writer libreoffice-calc


On other systems, install LibreOffice manually.

🚀 How to Use
1️⃣ Prepare Your CSV File

Create a data.csv file.
Each column header becomes a placeholder in the Word template.

⚠️ Include a case-sensitive boolean column named PDF:

True → Convert to PDF

False → Keep as DOCX

Example data.csv:

NAME,ADDRESS,AMOUNT,PDF
Alice,123 Main St,100.50,True
Bob,456 Oak Ave,200.75,True
Charlie,789 Pine Ln,150.00,True
David,101 Elm Rd,300.25,False

2️⃣ Prepare Your Word Template

Create template.docx and insert placeholders using double curly braces.

The placeholder names must exactly match your CSV headers.

Example template.docx:

Personalized Document

Dear {{NAME}},

This document is personalized for you at {{ADDRESS}}.

The amount due is ${{AMOUNT}}.

3️⃣ Run the Script

Place the script, data.csv, and template.docx in the same directory, then run:

python main.py


The script will:

Install LibreOffice (if needed)

Load the CSV file

Generate one document per row

Convert to PDF when PDF=True

Clean up temporary files

🧠 Example Execution Flow
import pandas as pd
import os
from docx import Document
import subprocess

# ... full script logic ...

print("Document generation complete.")

📁 Output Structure

After running the script, you’ll get:

output_documents_docx/
│── document_1.docx
│── document_2.docx

output_documents_pdf/
│── document_1.pdf
│── document_2.pdf


DOCX folder
Contains all .docx files and any temporary files if conversion fails.

PDF folder
Contains all successfully converted PDFs.

💫 Final Notes

Works great in Google Colab, Linux servers, and local machines

Easy to extend for email sending, branding, or batch workflows

Built to be practical, flexible, and just a little bit ✨extra✨
