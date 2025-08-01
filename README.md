# Cropio — All-in-One Online File Toolkit

**Cropio** is a comprehensive, all-in-one web application for file manipulation, built with Flask and modern frontend technologies. It provides a suite of powerful tools including file conversion, compression, image cropping, and a full-featured PDF editor, all wrapped in a sleek, responsive, and user-friendly interface.

---

## ✨ Main Features

- **Multi-Tool Interface**: A single application that houses multiple file processing utilities.
- **Modern UI/UX**: Clean, responsive design with dark mode, built using Tailwind CSS.
- **Drag & Drop Uploads**: Simple drag-and-drop file uploads for all tools.
- **Real-time Previews**: Interactive previews for images, PDFs, and cropping.
- **Backend Processing**: Powered by a modular Flask backend using libraries like Pillow and PyMuPDF.
- **Automatic Cleanup**: Background scheduler deletes temporary files after one hour to save server space.

---

## 🛠️ Tools Included

### 1. File Converters
- **Image Converter**: Convert PNG, JPG, WEBP, BMP, TIFF files to various image formats, including PDF and ICO.
- **PDF Converter**: Convert PDF files into editable DOCX documents or CSV spreadsheets.
- **Document Converter**: Convert DOCX files into PDF or plain TXT files.
- **Excel Converter**: Convert XLSX or XLS spreadsheets into CSV or JSON format.

### 2. File Compressor
- **Supported Formats**: PNG, JPG, WEBP, and PDF.
- **Compression Levels**: Choose between Low, Medium, and High compression.
- **Batch Processing**: Upload and compress multiple files simultaneously.
- **Detailed Results**: Display original size, compressed size, and total percentage saved.

### 3. Image & PDF Cropper
- **Supported Formats**: PNG, JPG, WEBP, and PDF.
- **Interactive Preview**: Real-time cropping preview.
- **Aspect Ratio Control**: Lock crop box to standard ratios (16:9, 4:3, 1:1, etc.).
- **Multiple Output Formats**: Export cropped output as JPEG, PNG, WEBP, or PDF.

### 4. PDF EditX
- **PDF Rendering**: View all pages with a thumbnail sidebar.
- **Editing Tools**: Add text, draw freehand, and highlight.
- **Client-Side Editing**: Fast, local edits using PDF-lib.js and PDF.js.
- **Export Changes**: Download the modified PDF.

---

## ⚙️ Tech Stack

- **Backend**: Flask, Pillow, PyMuPDF, pdf2docx, pandas, APScheduler
- **Frontend**: HTML5, Tailwind CSS, JavaScript
- **Libraries**: Cropper.js, PDF.js, PDF-lib.js

---

## 📂 Modular Flask Application Structure

### Directory Tree
```
converter1/
├── app.py                          # Main modular application
├── app_backup.py                   # Backup of monolithic app.py
├── config.py                       # Configuration settings
├── test_routes.py                  # Route testing script
├── requirements.txt                # Python dependencies
├── runtime.txt                     # Python version specification
├── routes/                         # Route modules
│   ├── __init__.py
│   ├── main_routes.py
│   ├── image_converter_routes.py
│   ├── pdf_converter_routes.py
│   ├── document_converter_routes.py
│   ├── excel_converter_routes.py
│   ├── compressor_routes.py
│   ├── cropper_routes.py
│   ├── pdf_editor_routes.py
│   └── file_serving_routes.py
├── utils/
│   ├── __init__.py
│   └── helpers.py
├── static/
│   ├── css/
│   └── js/
│       ├── theme.js
│       ├── index.js
│       ├── compressor.js
│       ├── cropper.js
│       ├── converter.js
│       ├── pdf_editor.js
│       └── pdf_editor_simple.js
└── templates/
    ├── base.html
    ├── layout.html
    ├── index.html
    ├── compressor.html
    ├── cropper.html
    ├── pdf_editor.html
    └── [converter templates]
```

### Route Modules Overview

- `main_routes.py` → Home page
- `image_converter_routes.py` → Image conversions
- `pdf_converter_routes.py` → PDF to DOCX/CSV
- `document_converter_routes.py` → DOCX to TXT
- `excel_converter_routes.py` → XLSX/XLS to CSV/JSON
- `compressor_routes.py` → Image and PDF compression
- `cropper_routes.py` → Image/PDF cropping
- `pdf_editor_routes.py` → PDF editing interface
- `file_serving_routes.py` → Downloads & previews

### JavaScript Modules

- `theme.js` — Dark/light toggle
- `index.js` — Homepage interactivity
- `compressor.js` — Compressor logic
- `cropper.js` — Image/PDF crop tool
- `converter.js` — Converter utilities
- `pdf_editor.js` — Full PDF editor
- `pdf_editor_simple.js` — Lightweight alternative

### Configuration (config.py)
- Constants, path setup, file extension rules

### Utilities (utils/helpers.py)
- `allowed_file()` — File type check
- `compress_image()` / `compress_pdf()`
- `cleanup_files()` — Delete temporary files

---

## ▶️ How to Run

1. **Start the app**:
   ```bash
   python app.py
   ```

2. **Test all registered routes**:
   ```bash
   python test_routes.py
   ```

3. **Restore original monolithic file** (if needed):
   ```bash
   copy app_backup.py app.py
   ```

---

## 🚀 Benefits of Modular Architecture

- **Maintainable**: Clearly separated responsibilities
- **Scalable**: Easily add more converters/editors
- **Testable**: Independent route testing
- **Debuggable**: Issues isolated by feature
- **Collaborative**: Multiple developers can contribute without conflict
- **Reusable**: Shared logic centralized in `utils/`

---

## ➕ Adding a New Route

1. Create a file in `routes/`, e.g., `new_converter_routes.py`
2. Define a `Blueprint`
3. Register it in `app.py`
4. Add frontend files if needed
5. Update UI templates

**Example:**
```python
# routes/new_converter_routes.py
from flask import Blueprint, render_template

new_converter_bp = Blueprint('new_converter', __name__)

@new_converter_bp.route('/new-converter')
def new_converter():
    return render_template('new_converter.html')
```

**Then in `app.py`:**
```python
from routes.new_converter_routes import new_converter_bp
app.register_blueprint(new_converter_bp)
```

---

Made with 💻 using Flask + Tailwind + PDF-lib.js
