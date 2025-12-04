# Testing Plan — BookFlow

## 1. General Information

This document defines the testing strategy, environment, and objectives for the **BookFlow** desktop application — an e-reader for managing personal libraries, built on **Python 3.13**, **Kivy**, and **SQLite**.

The purpose of testing is to verify the correctness of the user interface (UI), file parsing logic (PDF/EPUB), reading progress saving, and stability when working with a local database.

## 2. Testing objectives

1. Verify the correctness of CRUD operations for books (adding, reading the list, deleting).
2. Validate the file parser (PyMuPDF) for PDF and EPUB formats.
3. Ensure the correctness of saving and restoring reading progress (page number).
4. Check the operation of UI components: adaptive library grid, file upload dialogue, page zooming.
5. Evaluate the stability of the application when working with the file system and database.
6. Check error handling (corrupted files, missing covers).

## 3. Testing area

### In the testing area
- **Core Logic:** Classes `PDFBook`, `EpubBook`, `DBManager` (unit testing).
- **UI/UX:** Screens `WelcomeScreen`, `LibraryScreen`, `ReaderScreen`, `LoadDialog`.
- **Database:** Data integrity in SQLite, duplicate checking.
- **File System:** File selection via native Kivy explorer, cover generation.
- **Reading Experience:** Page turning, zoom (Scatter), hide interface on click.

### Outside the scope of testing
- Mobile build (Android/iOS) — at this stage, the focus is on Windows/Desktop.
- Synchronisation between devices (Cloud).
- Editing book metadata.

## 4. Testing Strategy

Testing will be performed using a **hybrid method**:
1. **Manual functional testing** to verify UI, animations, and UX scenarios.
2. **Unit testing** (where applicable) to verify database and parsing methods.

### Tools

| Type | Tool | Description |
|-----|-----------|---------|
| Runtime | Python 3.13 | Runtime environment |
| Framework | Kivy 2.3.1 | UI Framework |
| PDF Engine | PyMuPDF (fitz) | Page and cover rendering |
| DB | SQLite Viewer | Data verification in library.db file |
| Logs | Kivy Console | Error tracking and Traceback | 

## 5. Test environment

| Component | Characteristics |
|-----------|----------------|
| OS | Windows 10 / 11 |
| Screen resolution | 1920x1080 (Full Screen), changeable window mode |
| Input data | Set of test files: PDF (text, scans), EPUB |
| Database | Local file `library.db` |

## 6. Test types and coverage

| Type | Purpose | Number of scenarios |
|------|---------|---------------------|
| **UI Tests** | Layout, responsiveness, dialogues verification | 10 |
| **Functional Tests** | Adding books, reading, navigation | 12 |
| **Data Integrity** | Progress saving, deletion, duplicates | 5 |
| **Negative Tests** | Uploading invalid files, cancelling actions | 4 |

**Total:** 31 test cases

## 7. Risks and measures to mitigate them

| Risk | Probability | Mitigation measures |
|------|-------------|------------------|
| ‘Broken’ book file | Medium | Add try-except blocks in `core.py` |
| Book duplication | High | Implemented `UNIQUE` check in the database |
| Encoding issues (Russian titles) | Medium | Use `os.path` and correct fonts in Kivy |
| Crash when zooming | Low | Limit `scale_min` and `scale_max` in Scatter |
| Kivy does not start (OpenGL) | Low | Check drivers, log startup |

## 8. Entry and exit criteria

### Entry criteria
- The application starts (`python main.py`) without critical errors.
- The `interface.kv` file loads correctly.
- The `pymupdf` library is installed.

### Exit criteria
- All main scenarios (UC1-UC4) are completed successfully.
- No graphic artefacts (grey stripes, overlaps).
- Reading progress is saved between restarts.

## 9. Test data

### Test files
1. `manual.pdf` (Text PDF, 50 pages)
2. `scan.pdf` (Heavy scan, 200 MB)
3. `book.epub` (Standard EPUB)
4. `broken.pdf` (Corrupted file)

### Test users (local profiles)
| Login | Password | Role |
|-------|--------|------|
| admin | 12345 | Test user |
| user | pass | Regular user |

## 10. Schedule

| Stage | Status |
|------|--------|
| UI development (Kivy) | Done |
| DB integration (SQLite) | Done |
| Reader implementation (PyMuPDF) | Done |
| Bug fixes (UI, duplicates) | Done |
| Regression testing | In Progress |

---
**Author:** Lizaveta  
**Project:** BookFlow
