# Smart Drug Store Management System

**An OCR-assisted pharmacy inventory system for prescription medicine availability verification**

> A software-engineering project exploring how prescription text extraction and a structured medicine inventory can help pharmacists check whether prescribed medicines are available, with the pharmacist remaining responsible for reviewing the prescription and confirming the result.

## 1. Objective

Traditional pharmacy workflows often require a pharmacist to visually interpret a prescription and then manually search the store's medicine records or shelves to determine whether each prescribed medicine is in stock. This can take time, particularly when prescriptions contain several medicines, handwriting is difficult to read, or inventory records are large.

The objective of this project is to build a web-based Smart Drug Store Management System that connects prescription scanning with medicine availability verification. Rather than requiring every medicine name to be entered manually, the system uses **Optical Character Recognition (OCR)** to extract text from an uploaded prescription image and then checks the extracted medicine names against the pharmacy's medicine inventory. The user can review which medicines appear to be available and which need further checking.

The intended benefit is to reduce repetitive manual searching, make inventory lookups more convenient, and provide a clearer workflow from prescription input to stock-status review. The project also explores how a familiar pharmacy-management workflow can be supported by a lightweight document-processing component.

**OCR is an assistive step—not a substitute for a pharmacist.** Prescription images may be blurred, handwritten, incomplete, or ambiguous, and OCR can misread medicine names, strengths, or dosage text. Extracted text and availability matches must therefore be reviewed by an authorised human before any dispensing decision. The system does not diagnose conditions, prescribe medicines, or independently approve substitutions.

## 2. Introduction

Pharmacy operations depend on accurate medicine records and timely access to stock information. In a manual or predominantly paper-based workflow, checking a prescription can involve two separate tasks: interpreting the medicine information on the prescription and locating the corresponding product in the pharmacy's inventory. Repeating these tasks for every prescription can introduce avoidable effort and may create opportunities for transcription or search errors.

This project brings those tasks into one web-based workflow. The OCR component aims to convert prescription-image text into machine-readable text, while the inventory component provides a structured source against which extracted medicine names can be checked. By connecting these components, the application demonstrates how document processing and database-backed lookup can support a practical pharmacy workflow.

The project is also an applied software-engineering exercise: it brings together a web interface, server-side application logic, a database, and an OCR-based document-processing step. Its value is not a claim that OCR is perfectly accurate, but an exploration of how these components can be integrated into a workflow that remains reviewable by a pharmacist.

## 3. Problem Statement

A manual medicine-availability workflow can require a pharmacist or staff member to read the prescription, interpret each medicine name, and search inventory records individually. This is repetitive and may become inconvenient as the number of medicines and prescriptions grows. OCR can help reduce the amount of text that must be typed, but OCR output may contain errors, and a text match alone does not establish that a product is clinically appropriate or safe to dispense.

The system addresses the narrow operational question:

**“Given the medicine names extracted from a prescription, which corresponding items appear in the pharmacy inventory, and which require further review?”**

## 4. Project Objectives

- Reduce repetitive manual searching: use OCR to obtain candidate medicine text from a prescription image rather than relying exclusively on manual transcription.
- Support inventory lookup: compare extracted medicine names with medicine records maintained by the pharmacy.
- Make availability status easier to review: present the result of the inventory check so a pharmacist can identify items that appear available or need additional checking.
- Integrate complementary components: demonstrate a web application workflow connecting the user interface, server-side logic, OCR, and a database.
- Keep the workflow human-verifiable: allow the pharmacist to review OCR output and confirm matches rather than treating an automated text extraction as authoritative.
- Provide a foundation for future improvement: make it possible to investigate OCR quality, medicine-name matching, inventory consistency, and usability in later iterations.

## 5. Intended Workflow

1. **Prescription input:** the user uploads a prescription image through the website.
2. **Text extraction:** the OCR component attempts to extract readable text from the image.
3. **Medicine-name review:** extracted text is inspected to identify candidate medicine names. Incorrect or uncertain text should be checked by a human.
4. **Inventory lookup:** candidate medicine names are compared with the pharmacy's stored medicine records.
5. **Availability display:** the application displays the lookup outcome, such as an apparent match or a need for further checking, according to the functionality implemented in the current version.
6. **Pharmacist verification:** the pharmacist confirms the medicine identity and stock status before taking any dispensing-related action.

> **Implementation note:** This workflow describes the project's intended purpose. The exact behaviour depends on the current implementation; do not interpret OCR extraction or an inventory match as a guarantee of prescription correctness, product equivalence, or physical stock availability.

## 6. Core Features

The repository should describe only features that are implemented and working in the current version. The core project scope is:

- Web-based pharmacy-management interface.
- OCR-assisted text extraction from prescription images.
- Medicine availability verification against pharmacy inventory records.
- Database-backed medicine information.
- A result view that helps a user review detected medicine names and inventory lookup outcomes.

If the current version includes additional modules—such as adding or editing medicines, stock updates, authentication, expiry tracking, or reporting—document them here only after verifying them in the application.

## 7. Technology Stack

The project has been developed around the following technologies; update the OCR library and any additional frontend tools to match the source code exactly.

- **Backend:** PHP
- **Database:** MySQL
- **Local development environment:** XAMPP (or another compatible PHP/MySQL environment)
- **OCR:** the OCR library or engine configured in the project
- **Editor:** Visual Studio Code may be used for development
- **Frontend:** HTML, CSS, and JavaScript if present in the implementation

## 8. Repository Structure

The exact structure may vary according to the current source code. A reader-friendly project should make the following items easy to locate:

```text
pharmacy-smart-drugstore/
├── README.md
├── assets/                 # Stylesheets, scripts, and interface assets (if used)
├── database/               # Sanitised database schema or setup SQL (if provided)
├── docs/
│   └── screenshots/        # Screenshots of the real application
├── includes/               # Shared PHP/database connection files (if used)
├── uploads/                # Runtime uploads; do not commit real prescriptions
└── ...                     # Existing application files and directories
```

This is an illustrative layout, not a requirement to move files blindly. Preserve working include paths and existing application routes. Organise folders only when the change can be tested without breaking the application.

## 9. Setup and Run Locally

The precise setup depends on the filenames and configuration in this repository. The following is a general local-development checklist; adjust the database file and configuration paths to match the actual code.

1. **Clone the repository**

   ```bash
   git clone https://github.com/KubraCSE06/pharmacy-smart-drugstore.git
   ```

2. **Start the local environment**

   Install and start a compatible PHP/MySQL stack, such as XAMPP. Start Apache and MySQL if your setup uses XAMPP.

3. **Place the project in the web root**

   For a standard XAMPP installation, place the project folder inside `htdocs`, unless your web server is configured to use a different document root.

4. **Create the database**

   Open phpMyAdmin or your preferred MySQL client and create the database expected by the application. If the repository includes a `.sql` schema or database dump, import that file. If no schema is included, consult the project's existing database setup before proceeding.

5. **Configure the database connection**

   Set the local database name, username, password, and host in the PHP configuration file used by the project. Do not commit real credentials; keep local secrets out of Git and provide a placeholder configuration example when appropriate.

6. **Configure OCR**

   Install and configure the OCR engine required by the code. Follow the engine's own installation instructions and verify that PHP can access it. The specific requirements depend on the OCR library actually used.

7. **Open the application**

   Navigate to the project's local URL in a browser, for example `http://localhost/pharmacy-smart-drugstore/`, and use the entry page defined by the repository.


## 📁 Project Structure

```
pharmacy/
├── login.php               ← Login page
├── logout.php              ← Logout
├── dashboard.php           ← Main dashboard
├── database.sql            ← Import this into MySQL!
├── css/
│   └── style.css           ← All styles
├── includes/
│   ├── config.php          ← DB connection + helpers
│   ├── header.php          ← Shared navbar/sidebar
│   ├── footer.php          ← Shared footer
│   └── ocr_match.php       ← 🧠 Fuzzy drug-name matching engine
├── uploads/
│   └── prescriptions/      ← Uploaded prescription photos land here
└── modules/
    ├── users.php           ← 👤 User Management 
    ├── medicines.php       ← 💉 Inventory 
    ├── expiry.php          ← ⏰ Expiry Alerts 
    ├── sales.php           ← 🛒 New Sale
    ├── sales_history.php   ← 📋 Sales Records 
    ├── invoice.php         ← 🧾 Invoice Print
    └── prescription.php    ← 📷 OCR Prescription Scanner 
```

---

## 🚀 How to Run (XAMPP)

### Step 1 — Copy the project
Copy the `pharmacy/` folder to:
```
C:\xampp\htdocs\pharmacy\
```

### Step 2 — Import the database
1. Open your browser → go to `http://localhost/phpmyadmin`
2. Click **"New"** on the left → create a database named `pharmacy_db`
3. Click on `pharmacy_db` → click **"Import"** tab at the top
4. Choose the file `pharmacy/database.sql` → click **"Go"**

### Step 3 — Configure database
Open `includes/config.php` and set:
```php
define('DB_USER', 'root');   // your MySQL username
define('DB_PASS', '');       // your MySQL password (blank by default in XAMPP)
```

### Step 4 — Open in browser
```
http://localhost/pharmacy/login.php
```

---

## 🔐 Login Credentials

| Role        | Username     | Password   |
|-------------|--------------|------------|
| **Admin**   | `admin`      | `password` |
| Pharmacist  | `pharmacist` | `password` |
| Manager     | `manager`    | `password` |

]

## ✅ Features Implemented

### 1️⃣ User Management 
- [x] Login with username & password
- [x] Logout
- [x] Role-based access: Admin, Pharmacist, Manager
- [x] Add / Edit / Delete users (Admin only)
- [x] Password hashing (secure, using PHP password_hash)
- [x] Active / Inactive user status

### 2️⃣ Inventory Management 
- [x] Add medicine (name, batch, supplier, category, expiry, price, qty)
- [x] Edit / Update medicine details
- [x] Delete medicine (Admin only)
- [x] View all stock
- [x] Low stock alert (highlighted in red)
- [x] Search by name, supplier, batch number
- [x] Filter: All / Low Stock / Expiring Soon

### 3️⃣ Expiry Tracking
- [x] Automatic expiry date checking
- [x] Color-coded: Red = Expired, Yellow = ≤30 days, Green = Safe
- [x] Expired medicines list (remove immediately)
- [x] Expiring soon list with days remaining
- [x] Summary stats on dashboard

### 4️⃣ Sales 
- [x] Record sales with multiple items
- [x] Auto-deducts stock after each sale
- [x] Unique invoice number generation
- [x] Printable invoice
- [x] Sales history with search
- [x] Filter by date range, customer, invoice number
- [x] Revenue totals

### 5️⃣ 🧠 Smart Prescription Scanner
- [x] Upload a photo of a handwritten/printed prescription
- [x] OCR runs **entirely in the browser** via [Tesseract.js](https://github.com/naptha/tesseract.js) — no server-side OCR engine to install
- [x] Editable OCR output — pharmacist can correct misreads before saving
- [x] Smart fuzzy-matching engine (`includes/ocr_match.php`) tokenises the recognized text, strips dosage/instruction noise (mg, tab, BD, TDS…), and matches drug names against inventory using similarity scoring — so "Amoxicilin" still matches "Amoxicillin 250mg"
- [x] Live availability check per matched drug: **Available / Low Stock / Out of Stock / Not in Inventory**
- [x] Full scan history with patient name/phone, confidence score, and matched item count
- [x] One-click hand-off to **New Sale** after reviewing matches

---

## 🧠 How the OCR Feature Works (Architecture)

```
[Browser]                                   [Server: PHP + MySQL]
   │
   │ 1. User selects prescription image
   ▼
Tesseract.js (client-side OCR)
   │
   │ 2. Extracts raw text + confidence score
   ▼
Pharmacist reviews/edits text in <textarea>
   │
   │ 3. Form POST (multipart/form-data): image + ocr_text + confidence
   ▼
modules/prescription.php  ──save_scan──▶  uploads/prescriptions/*.jpg
   │
   │ 4. calls matchPrescriptionText($conn, $ocrText)
   ▼
includes/ocr_match.php
   ├── extractCandidateLines()  → splits OCR text into drug-name candidates,
   │                               strips dosage/frequency noise
   └── fuzzyMatchMedicine()     → similar_text() + containment scoring
                                   against the `medicines` table
   │
   │ 5. INSERT prescriptions + prescription_items
   ▼
MySQL (pharmacy_db)
   │
   │ 6. Redirect to prescription.php?view=ID
   ▼
Results page: matched drug ↔ live stock qty ↔ price ↔ availability badge
```

**Why client-side OCR?** Running Tesseract.js in the browser means zero server
setup (no `tesseract-ocr` binary, no PHP extension, no PATH configuration) —
it works the moment you open the page, on any XAMPP install. The trade-off is
that OCR quality depends on the device's browser/CPU, so the UI always lets
the pharmacist review and fix the recognized text before it's matched and saved.

**New database tables** (already included in `database.sql`):
- `prescriptions` — one row per scanned prescription (patient info, image path, raw OCR text, confidence, status)
- `prescription_items` — one row per detected drug line, linked to a `medicines.id` when matched, with the match score and stock snapshot at scan time

- ## Testing and Verification

Testing should focus on both the web application and the OCR-to-inventory workflow. Useful cases include:

- A clear sample prescription where the medicine name is readable.
- A blurry or low-resolution image where OCR may be uncertain.
- A medicine name that exists in the database.
- A medicine name that does not match any inventory record.
- A spelling variation or OCR character error.
- An empty or unsupported file upload.
- An inventory record whose stock information is missing or outdated.

Record actual results rather than marking these cases as passed before testing. For OCR, distinguish text-extraction quality from inventory-matching quality: a correct database lookup cannot repair a medicine name that was extracted incorrectly.

## Safety, Privacy, and Limitations

- **OCR limitations:** handwritten or poor-quality prescriptions can result in incorrect or incomplete extraction.
- **Name matching:** similar medicine names may refer to different products; a textual match alone is insufficient to establish equivalence.
- **Inventory freshness:** a database result is only as reliable as the inventory data and its update process.
- **Human oversight:** a qualified pharmacist must verify the prescription and medicine before dispensing decisions.
- **Privacy:** use synthetic or anonymised data for screenshots and testing; do not publish sensitive prescription uploads or credentials.
- **Scope:** this is an educational/software-engineering project, not a validated clinical decision-support device or a substitute for professional judgement.

## Future Work

Potential improvements, subject to the scope and resources of future development, include:

- Measuring OCR quality on a carefully defined set of synthetic or permissioned prescription samples.
- Improving medicine-name normalisation and handling uncertain OCR results.
- Presenting confidence or review-needed indicators where supported by a validated method.
- Improving inventory update and stock-verification workflows.
- Adding automated tests for uploads, OCR output, and inventory matching.
- Improving authentication, access control, input validation, and secure file handling.
- Conducting usability evaluation with appropriate supervision and without exposing patient information.

These are proposed directions, not claims about features already delivered.

## Project Status

This project demonstrates an OCR-assisted approach to prescription text extraction and medicine availability checking in a pharmacy-management workflow. Its current capabilities and limitations should be assessed from the implementation and tests in this repository. Further validation is required before considering use in a real pharmacy setting.

## License

Add a `LICENSE` file and specify the intended reuse terms before presenting the repository as open source. Until a license is added, do not assume that others have permission to reuse or redistribute the code.


