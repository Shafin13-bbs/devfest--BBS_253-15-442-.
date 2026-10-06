#Name: BAyezid Bostami 
#Email-ID: 253-15-442@diu.edu.bd


# Tender Package Builder

A simple website that helps office staff turn a pile of PDF files into **one complete, checked and correctly ordered tender package**, ready to submit.

No installation. No account. No technical skills needed. Everything runs inside your web browser.

---

## Why this exists

When a company bids for a tender, it must submit a set of documents, such as a trade license, TIN and VAT certificates, a bank solvency letter, experience certificates, and technical and financial proposals.

Preparing this by hand is risky. A single small mistake can get a bid rejected:

- a document is **missing**
- a license has **expired**
- the **same file** is included twice
- documents are in the **wrong order**
- pages are **not numbered**

This website checks all of these for you and builds the final PDF automatically.

---

## What you can do with it

| Feature | What it means for you |
|---|---|
| **Load the tender** | Open `requirements.json` and see the tender details and the list of documents you must submit. |
| **Upload many PDFs at once** | Each file shows its name and page count. Non-PDF files are rejected with a clear message. You can remove any file. |
| **Match files to documents** | Pick the right file for each required document. You can change or clear a match at any time. |
| **Enter expiry dates** | For documents that expire, a date box appears once a file is matched. |
| **Live status checking** | Every document shows one clear status that updates instantly. |
| **Duplicate detection** | Files with identical content are flagged, even if their names differ, and cannot be used for two different documents. |
| **Create the package** | One click builds a single PDF with a cover page, your documents in order, and page numbers. |
| **Download** | The file is saved as `<tender_id>_Package.pdf`. |
| **Two languages** | Switch the whole website between English and Bangla at any time. |

### Extra helpers

- **Suggest matches:** guesses which file belongs to which document from the file names.
- **Download checklist (CSV):** exports document, file name, pages, expiry date and status.
- **Safe handling of bad files:** damaged or password-protected PDFs show a message instead of crashing.
- **Next-step banner, progress steps, tips and a package preview:** guide you through the work.

---

## How to use it (step by step)

### Step 1. Open the website
Open `index.html` in **Google Chrome**. You need an internet connection, because the PDF tool and the Bangla font are loaded online.

### Step 2. Load the tender
Click the large box and choose `requirements.json`. The tender ID, title, procuring entity, bidder and submission deadline appear, along with the list of required documents in the correct order.

### Step 3. Upload your PDFs
Click **Add PDF files** (or drag files in) and select all your documents together. Limits: up to **30 files** and **50 MB** in total. Only PDF files are accepted.

### Step 4. Match each file to a document
On each document row, open the dropdown and choose its file. Use **Suggest matches** to save time, then check every row yourself.

Rules:
- One document gets **at most one** file.
- One file goes to **at most one** document.
- Identical (duplicate) files cannot be used for different documents.

### Step 5. Enter expiry dates
If a document has an expiry date and a file is matched, a date box appears. Type the expiry date printed on the document.

### Step 6. Read the statuses
Each document shows exactly one status:

| Status | When it appears | Stops the package? |
|---|---|---|
| **Missing** | A required document has no file. | Yes |
| **Expiry date needed** | A file is matched, but no expiry date is entered. | Yes |
| **Expired** | The expiry date is before the submission deadline. | Yes |
| **Not provided** | An optional document has no file. | No |
| **OK** | A file is matched and, if it expires, the date is on or after the deadline. | No |

A document that expires **on** the submission deadline is still **OK**.

### Step 7. Create and download
The **Create package** button stays disabled while any document blocks the package, and the website lists exactly what to fix. When everything is clear, press the button. Your file `<tender_id>_Package.pdf` downloads.

---

## What the final PDF looks like

1. **Page 1 is a cover page (in English)** showing the tender ID, tender title, procuring entity, bidder name, submission deadline, the date the package was made, and the list of included documents in order with their page numbers.
2. **Your documents follow**, sorted by the tender's order. All pages of each file are included in their original order. Optional documents with no file are skipped.
3. **Every page has a footer**, including the cover: `<tender_id> | Page X of Y`, where Y is the total number of pages. The footer sits in an extra white strip at the bottom, so it never covers your document's content.

---

## Example: the sample pack

The sample pack (tender `T-2026-0417`) has a few hidden problems that the website helps you find:

| Problem | What to do |
|---|---|
| Two trade licenses (2025 and 2026). The 2025 one expired on 2025-06-30. | Use `trade_license_2026.pdf` (valid until 2027-06-30). |
| Two identical experience certificates under different names. | Use only one. The website marks them as duplicates. |
| `scan_0042.pdf` has an unclear name. It is the signed declaration. | Match it by hand to **Signed Declaration**. |
| Two optional documents are not in the pack (audited financial statement, manufacturer's authorization). | Leave them empty. They show **Not provided** and do not block anything. |

Expiry dates to enter: **Trade License: 2027-06-30**, **Bank Solvency: 2026-12-31**.

With these fixes the package should have 16 pages: the cover plus 15 pages from the documents.

---

## Privacy

Your documents **never leave your computer**. All checking and PDF building happens inside your browser. Nothing is uploaded to any server, database or online storage.

---

## Running it on your computer

1. Download `index.html`.
2. Double-click it, or right-click and choose **Open with Google Chrome**.

Optional: in VS Code, install the **Live Server** extension, right-click `index.html` and choose **Open with Live Server**.

## Putting it online

Because it is a single file, you can publish it with any static hosting service. For example, with GitHub Pages:

1. Put `index.html` in a GitHub repository.
2. Open the repository's **Settings → Pages**.
3. Choose the main branch and save. You will get a public HTTPS link.

---

## Technical notes

- A single `index.html` file with plain HTML, CSS and JavaScript. There is no backend.
- **[pdf-lib](https://pdf-lib.js.org/)** (loaded from a CDN) reads PDFs, copies pages and adds the cover and footers.
- Duplicate files are found by comparing a SHA-256 fingerprint of each file's content.
- The cover page uses standard English fonts. Bangla appears in the website itself, not on the PDF cover.
- Built for the latest Google Chrome.

## Known limits

- The expiry dates are typed in by you. The website does not read them from the PDFs.
- The cover page is English only.
- Your work is not saved. If you close or reload the page, you start again.
- File-name matching is only a suggestion, so always check each row.

---

## Fictional data notice

All companies, people, numbers and documents in the sample pack are fictional and are for the AI DevFest contest only.
