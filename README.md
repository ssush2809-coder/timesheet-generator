# USK Systems IT INC Timesheet Generator

This is a Streamlit web app that fills the USK Systems IT INC timesheet PDF by using the original PDF as the background/template and overlaying only the entered values.

It does not redesign the form. The logo, watermark, table structure, supervisor signature, footer, borders, spacing, and layout stay inside the original PDF template.

## Features

- Upload and save the original USK timesheet PDF template once
- Save employee name and supervisor name for future weeks
- Upload, save, and replace employee signature image anytime
- Keep the supervisor signature already present in the original PDF
- Auto-populate Monday through Sunday dates from the selected reporting week
- Enter daily hours and automatically calculate total hours
- Generate a submission-ready PDF
- Export a Word file that visually preserves the generated PDF
- Keep history of generated timesheets
- Edit/regenerate any previous week from the sidebar
- Advanced overlay coordinate editor for small alignment adjustments

## Folder structure

```text
usk_timesheet_app/
  app.py
  timesheet_engine.py
  storage.py
  requirements.txt
  README.md
  config/default_overlay_config.json
  data/
  output/
```

## How to run on Windows

1. Open Command Prompt or PowerShell inside this folder.
2. Create a virtual environment:

```bash
python -m venv .venv
```

3. Activate it:

```bash
.venv\Scripts\activate
```

4. Install the packages:

```bash
pip install -r requirements.txt
```

5. Start the app:

```bash
streamlit run app.py
```

6. In the browser, upload the original PDF template: `Time sheets - USK Systems IT INC (1) (2).pdf`.

The app will save the template in `data/template.pdf` and reuse it every week.

## How PDF generation works

The app opens the original template PDF using PyMuPDF, places the typed values in the configured positions, inserts the saved employee signature image, and saves a new PDF. Since the supervisor signature is already part of the template, it automatically appears in every generated PDF.

## Signature behavior

- Upload PNG, JPG, or JPEG signature file.
- The app saves it locally in the `data` folder.
- Every new PDF uses the saved signature automatically.
- Upload a new signature anytime to replace the old one.

## Word export note

The Word export is image-based. It places the generated PDF page as a full-page image inside a DOCX file. This keeps the Word version visually consistent with the PDF template instead of rebuilding the form manually.

## Adjusting placement

If a field is slightly misaligned, open **Advanced: adjust overlay positions** in the app. The coordinates are stored as percentages of page width/height.

Example field:

```json
"employee_name": {"x": 0.218, "y": 0.340, "w": 0.308, "h": 0.030}
```

- `x`: distance from left side of page
- `y`: distance from top of page
- `w`: field width
- `h`: field height

Small changes like `0.340` to `0.345` move the value slightly down.
