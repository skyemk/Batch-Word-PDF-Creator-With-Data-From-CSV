This is a vibe coded project, enjoy!

Automated Document Generation and Conversion
This project provides a Python script to automate the generation of personalized Word documents (.docx) from a template, using data from a CSV file. It further enhances this process by conditionally converting these generated Word documents into PDF format (.pdf) based on a specified column in the input data, leveraging LibreOffice for the conversion.

Features
Placeholder Replacement: Dynamically replaces placeholders (e.g., {{COLUMN_HEADER}}) in a Word template with corresponding data from each row of a CSV file.
Conditional Output Format: Determines whether to output a .docx or .pdf file for each record based on a 'PDF' boolean column in the input data.
LibreOffice Integration: Uses the headless (terminal) version of LibreOffice for robust and reliable .docx to .pdf conversion.
Organized Output: Creates separate directories for .docx and .pdf outputs to keep generated files neatly organized.
Error Handling: Includes error handling for LibreOffice installation and document conversion processes.
Sample Data and Template: Automatically creates a sample data.csv and template.docx if they don't exist, making it easy to get started.
Requirements
Before running the script, ensure you have the following installed:

Python 3.x
pandas: pip install pandas
python-docx: pip install python-docx
LibreOffice: The script attempts to install libreoffice-writer and libreoffice-calc using sudo apt-get install (for Debian-based systems like Colab). If running locally, you might need to install LibreOffice manually.
How to Use
1. Prepare Your Data File (CSV)
Create a CSV file (e.g., data.csv) with your data. The column headers in this file will correspond to the placeholders in your Word template. Include a boolean column named PDF (case-sensitive) where True indicates that the document for that row should be converted to PDF, and False indicates it should remain in DOCX format.

Example data.csv content:

NAME,ADDRESS,AMOUNT,PDF
Alice,123 Main St,100.50,True
Bob,456 Oak Ave,200.75,True
Charlie,789 Pine Ln,150.00,True
David,101 Elm Rd,300.25,False
2. Prepare Your Word Template (DOCX)
Create a Word document (e.g., template.docx) that will serve as your template. Insert placeholders for the dynamic content using double curly braces {{COLUMN_HEADER}}. Ensure that the placeholder names exactly match your CSV column headers.

Example template.docx content:

# Personalized Document

Dear {{NAME}},

This document is personalized for you at {{ADDRESS}}.

The amount due is ${{AMOUNT}}.
3. Run the Python Script
Place your data.csv and template.docx in the same directory as your Python script. The script will:

Install LibreOffice (if not already installed).
Load data.csv into a pandas DataFrame.
For each row in the DataFrame:
Load template.docx.
Replace all {{PLACEHOLDER}} with the row's data.
If the PDF column for that row is True, it will save a temporary DOCX, convert it to PDF using LibreOffice, and then delete the temporary DOCX.
If the PDF column is False, it will save the document as a DOCX.
Example execution flow (as seen in Colab):

# This code block (cell b2a713a9) contains the full script
# It will create/load data.csv and template.docx
# Install LibreOffice if needed, and then generate documents.
import pandas as pd
import os
from docx import Document
import subprocess

# ... (rest of the script as provided in the notebook)

print("Document generation complete.")
4. Output Files
The generated documents will be saved in the following directories:

output_documents_docx/: Contains all .docx files, including those that were not converted to PDF and temporary .docx files if the conversion failed.
output_documents_pdf/: Contains all .pdf files generated from the .docx templates.
