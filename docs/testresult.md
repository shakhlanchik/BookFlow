# Test results — BookFlow

## 1. General information

Functional and UI testing was performed on the **BookFlow** application (version with PDF/EPUB support and adaptive interface). Testing was performed on the desktop version (Windows).

**Key changes in this version:**
- Transition to `interface.kv` (solution to the double loading problem).
- New `LoadDialog` design (dark theme, no artefacts).
- Implementation of page scaling (`Scatter`).
- Saving reading progress in the database.

## 2. Execution summary

| Metric | Number |
|---------|-----------|
| Total test cases | 31 |
| Passed | 29 |
| Failed | 0 |
| Skipped | 2 (related to corrupted files) |
| Critical bugs | 0 |

**Overall result: SUCCESSFUL**  
**Version stability: High** 

## 3. Detailed results by module

| Module | Functionality | Status | Comment |
|--------|------------|--------|-------------|
| **Auth** | Registration/Login | Pass | Creates profiles in the database correctly |
| **Library** | Book list | Pass | Adaptive `StackLayout` works correctly |
| **Library** | Adding books | Pass | Duplicates are not created, `UNIQUE` check works |
| **Library** | Deleting books | Pass | Book is deleted from UI and database |
| **UI** | Download dialogue | Pass | Grey frames removed, colours configured |
| **Reader** | Opening PDF | Pass | Covers are generated, pages are turned |
| **Reader** | Opening EPUB | Pass | PyMuPDF correctly renders EPUB as pages |
| **Reader** | Zoom | Pass | `Scatter` works, borders are cropped `StencilView` |
| **Logic** | Saving progress | Pass | Last page opens on restart |

## 4. Fixed defects (Retest)

| ID | Problem description | Verification result | Status |
|----|-------------------|--------------------|--------|
| BUG-001 | Double display of books in the library | Books are displayed as a single copy. The KV file has been renamed. | Fixed |
| BUG-002 | Grey rectangle in `LoadDialog` | Window background configured, extra `canvas` removed. |  Fixed |
| BUG-003 | Text artefacts on top of cover | Text removed from button, `RelativeLayout` used. |  Fixed |
| BUG-004 | Scroll does not work in file selection | Scroll bar hidden, scroll works. |  Fixed |
| BUG-005 | Page was not saved | Added `current_page` field, progress is written to the database. | Fixed |

## 5. Performance

| Metric | Value | Rating |
|---------|----------|--------|
| Application launch | < 1 sec | Excellent |
| Cover generation (PDF) | ~0.1 - 0.3 sec |  Normal |
| Page turning | Instantaneous | Excellent |
| RAM consumption | ~150 MB (with book open) | Normal |

## 6. Test scenarios (User Journey)

### Scenario 1: Adding and reading
1. **Login:** The user logs in with their username. -> *Successful*.
2. **Library:** Presses ‘+’. A dark file selection window opens. -> *Successful, design is correct*.
3. **Selection:** Selects `manual.pdf`. Clicks ‘Upload’. -> *Successful, book appears in the grid*.
4. **Reading:** Clicks on the cover. Page 1 opens. -> *Successful*.
5. **Navigation:** Go to page 5. Zoom in on the text. -> *Success*.
6. **Exit:** Click ‘To library’. -> *Success*.
7. **Return:** Reopen the book. -> *Page 5 opened immediately*.

### Scenario 2: Adaptability
1. **Expanded window:** 5-6 books fit in a row.
2. **Reduced window:** Books are moved to the next lines (`StackLayout`).
3. **Result:** The layout does not break, there is no horizontal scrolling.

## 7. Recommendations and improvements (Backlog)

Although there are no critical bugs, there is room for improvement:
1. **Loading indicator:** When adding a large PDF (100+ MB), the interface may freeze for a split second. A spinner should be added.
2. **Reader settings:** Add the ability to change the zoom mode or page background (white/sepia/night).
3. **Search:** Currently, the search is case-sensitive (`lower()` has been added to the code and works correctly, but complex cases should be checked).

## 8. Conclusion

The **BookFlow v1.0 (Release Candidate)** application version has been tested.
Critical errors that prevent use (duplicates, UI issues) have been fixed. The functionality meets the SRS requirements.

**Decision:** Ready for demonstration/laboratory work submission.
---
**Date:** 25 November 2025

**Tester:** Lizaveta
