# Design Plan: Kejar Sains 2026 - Museum Bank Indonesia

## Project Overview
A web-based form submission system for 350 students of SMP PGII 1 Bandung to complete worksheets during their visit to Museum Bank Indonesia. The system focuses on ease of use, data safety (auto-save), and mobile responsiveness.

## Architecture
- **Frontend**: Single Page Application (SPA) using HTML5, Tailwind CSS, and Vanilla JavaScript.
- **Backend/Database**: Firebase Firestore.
- **Hosting**: GitHub Pages.

## Key Features
1. **Student Identification**: Searchable dropdown for 350 students to prevent typos.
2. **Subject Navigation**: 3 main buttons for IPA, IPS, and PAI subjects.
3. **Auto-Save (Robust Sync)**: 
   - Debounced input (1.5s delay) to save essay answers automatically to Firestore.
   - Uses `{ merge: true }` to ensure answers from different subjects don't overwrite each other.
4. **Offline Support**: Firebase IndexedDB persistence enabled to handle spotty museum signals.
5. **Mobile-First Design**: Optimized for smartphone screens with large touch targets and 16px+ font sizes.

## Data Structure (Firestore)
- **Collection**: `submissions`
- **Document ID**: `[Student Name] - [Class]`
- **Fields**:
  - `student_info`: { name, class }
  - `answers_ipa`: { q1, q2, ... }
  - `answers_ips`: { q1, q2, ... }
  - `answers_pai`: { q1, q2, ... }
  - `metadata`: { last_updated, user_agent }

## Implementation Steps
1. **Setup Firebase**: Initialize project and Firestore rules.
2. **Frontend Skeleton**: Create HTML structure with Tailwind CSS.
3. **Student Data**: Integrate the list of 350 students (provided by user).
4. **Firebase Integration**: Implement `setDoc` with debounce logic.
5. **Testing**: Verify auto-save and offline persistence.
6. **Deployment**: Push to GitHub and enable Pages.

## Success Criteria
- 350 concurrent users can access the form.
- No data loss if the browser is closed or signal is lost.
- Easy data export for teachers (via Firebase Console or custom script).
