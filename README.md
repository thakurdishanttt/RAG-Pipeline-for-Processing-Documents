# RAG-Pipeline-for-Processing-Documents
 Automate document processing with this pipeline that handles PDFs, images, audio, and video files. Using OCR, Whisper, and GPT-4, it classifies documents and extracts key data fields, making it ideal for finance, legal, and compliance applications. Easy setup, robust logging, and extensible features streamline document workflows.

 # Document Classification and Information Extraction Pipeline

This project is a comprehensive document processing pipeline capable of handling various document formats, classifying them based on content, and extracting predefined fields based on document type. It leverages OCR, audio transcription, and OpenAI’s API for classification and field extraction. This pipeline aims to streamline workflows for processing large volumes of unstructured documents in various formats, offering a versatile solution for tasks such as identity verification, billing, and content summarization.

---

## Table of Contents

- [Introduction]
- [Features]
- [Requirements]
- [Installation]
- [Usage]
- [Pipeline Overview]
- [Detailed Explanations of Each Component]
- [Error Handling]
- [Troubleshooting]
- [Examples]
- [Contributing]
- [License]
- [Contact]


## Introduction

In document-intensive fields such as finance, administration, and compliance, manual processing of documents can be slow and error-prone. This Document Classification and Information Extraction Pipeline offers a solution by automating document intake, classification, and data extraction. Using state-of-the-art models like OpenAI’s GPT-4, Whisper, and Tesseract OCR, the pipeline efficiently processes documents of various types, including PDFs, images, audio, and video files, extracting valuable information from each.


## Features

1. **Automated Document Classification**:
   - Classifies documents into categories such as ‘invoice,’ ‘passport,’ ‘ID,’ ‘audio,’ ‘video,’ and others.
   - Uses OpenAI's GPT-4 model to analyze text content and assign a document type.

2. **OCR-Based Text Extraction**:
   - Utilizes Tesseract OCR to retrieve text from images and PDFs.
   - Preprocesses images to improve OCR accuracy through contrast enhancement and noise filtering.

3. **Audio and Video Transcription**:
   - Uses Whisper for high-accuracy transcription of audio and video files.
   - Handles audio extraction from videos and frame-based OCR for silent videos.

4. **Field Extraction**:
   - For specific document types, the pipeline extracts predefined fields (e.g., 'invoice number,' 'passport number,' etc.).
   - Queries OpenAI’s API to retrieve targeted information based on document type.

5. **Comprehensive Logging**:
   - Logs all operations for debugging, tracking errors, and performance analysis.
   - Includes both console and file logging for robust error tracking.



## Requirements

- **Python 3.7 or higher**
- **Tesseract OCR**: Required for OCR functionality on images and PDF files.
- **FFmpeg**: Necessary for processing audio and video files, specifically for audio extraction.
  
Dependencies listed in the `requirements.txt` file are Python libraries needed to run the project, such as `PyPDF2`, `pytesseract`, and `opencv-python`.

**Step 2: Install Python Dependencies**
Install required Python packages:

pip install -r requirements.txt

Step 3: Setup OpenAI API Key
Obtain an OpenAI API key from OpenAI's API page and set it as an environment variable:


export OPENAI_API_KEY='your_api_key_here'

Step 4: Install Tesseract OCR
Install Tesseract OCR by following instructions on the official Tesseract GitHub page. Ensure that tesseract is accessible in your system’s PATH.

Step 5: Download NLTK Data
This pipeline requires the NLTK 'punkt' package for tokenizing text. Run the following command to download it:
import nltk
nltk.download('punkt')


**Usage**
**Preparing to Run the Pipeline**
Specify the path of the document you want to process by updating the file_path variable in the code. Supported formats include:

PDFs (.pdf)
Images (.jpg, .jpeg, .png)
Audio files (.mp3, .wav)
Video files (.mp4, .avi, .mov, .mkv)


**Running the Pipeline**
Run the script to start processing the document:

python document_pipeline.py


**Output**
The pipeline outputs the document type and a JSON of extracted parameters. For example:


Document type: invoice
{
    "invoice number": "INV123456",
    "date": "2023-01-01",
    "total amount": "$500.00",
    "billing address": "123 Main St, Example City, Country"
}

**Pipeline Overview**
File Loading: Determines the file type and extracts text accordingly.
Text Extraction: Uses OCR for images/PDFs and Whisper for audio/video transcription.
Classification: Classifies document content using OpenAI’s API.
Field Extraction: Based on classification, retrieves specific fields using predefined queries.
Logging and Error Handling: Captures all actions and errors for transparency.


**Detailed Explanations of Each Component**
1. File Loading
PDF Processing: Reads each page of a PDF file and extracts text.
Image Processing: Loads the image and preprocesses it (grayscale, contrast enhancement) before OCR.
Audio/Video Processing: For videos, extracts audio first; if no audio is detected, performs OCR on specific frames.

2. Text Extraction
OCR for Image/PDF: Converts images to grayscale, applies contrast and filtering, and uses Tesseract OCR to recognize text.
Audio Transcription: Utilizes Whisper to transcribe audio and video files, handling various file formats.

3. Document Classification
Classification Model: Uses OpenAI's GPT-4 model to analyze text content and classify the document.
Supported Classes: The pipeline recognizes ‘invoice,’ ‘passport,’ ‘ID,’ ‘audio,’ and ‘video.’ Any unrecognized format is categorized as ‘other.’

4. Field Extraction
Field Retrieval: Once classified, OpenAI’s API is prompted with specific questions to extract data from each document.
Predefined Fields:
Invoice: Extracts 'invoice number', 'date', 'total amount', 'billing address'.
Passport: Extracts 'passport number', 'name', 'nationality', 'date of birth'.

5. Logging and Error Handling
Logging: Logs every step of the process, providing a detailed record of operations.
Error Handling: Catches and logs errors to avoid pipeline crashes and assist in debugging.


**Error Handling**
The pipeline includes robust error handling to address common issues, such as:

Unsupported File Format: Notifies the user if an unsupported file format is provided.
API Errors: Handles and logs any API errors from OpenAI, ensuring they do not stop the entire process.
OCR Failures: If Tesseract OCR fails to recognize text, the issue is logged, and the process continues.

**Troubleshooting**

Tesseract Not Found: Ensure Tesseract is installed and included in your PATH.
OpenAI API Key Issues: Verify the API key is correct and active.
OCR Quality: Poor OCR results? Adjust preprocessing in preprocess_image by tuning contrast and noise filtering.
Audio Issues: If the audio is not processed correctly, check that FFmpeg is installed and accessible.

**Examples**
Example 1: Processing an Invoice
Input:

File: sample_invoice.pdf
Output:
Document type: invoice
{
    "invoice number": "INV123456",
    "date": "2023-01-01",
    "total amount": "$500.00",
    "billing address": "123 Main St, Example City, Country"
}

Example 2: Processing a Passport
Input:

File: passport_image.jpg
Output:
Document type: passport
{
    "passport number": "A1234567",
    "name": "John Doe",
    "nationality": "USA",
    "date of birth": "1990-01-01",
    "expiration date": "2030-01-01"
}

