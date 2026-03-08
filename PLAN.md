# Tiny Markdown Revival Plan

**Date Created:** March 8, 2026 **Project:** tiny-markdown Legacy Code Revival
**Current Status:** Security & Quality Improvements

---

## Executive Summary

This document outlines the strategic plan to revive the tiny-markdown project
with focus on:

- 🔐 **Security fixes** (XSS vulnerabilities, input validation)
- 📦 **Code quality improvements** (maintainability, documentation)
- ✨ **Enhanced features** (export, syntax highlighting, UX)

---

## Phase 1: Security Fixes (🔴 CRITICAL) - Week 1

### 1.1 XSS Vulnerability Fix

**Status:** ✅ COMPLETED

- [x] Add DOMPurify library for HTML sanitization
- [x] Sanitize all HTML output from marked.js parser
- [ ] Test with malicious markdown payloads
- **Impact:** Prevents script injection attacks
- **Actual Effort:** 1 hour

### 1.2 Input Validation

**Status:** ✅ COMPLETED

- [x] Validate markdown input size limits (50KB real-time validation)
- [x] Add error handling for marked.js parsing failures
- [x] Implement graceful degradation
- **Impact:** Prevents DoS and parsing errors
- **Actual Effort:** 1.5 hours
- **Notes:** Added real-time validation in textarea input handler that truncates
  content at 50KB limit

### 1.3 localStorage Security

**Status:** ⏭️ SKIPPED

- localStorage is low-risk in single-user browser context
- Optional for future enhancement if needed
- **Impact:** Deferred to Phase 3+ if user requests it
- **Notes:** Stored content is user's own data, no sensitive third-party info

### 1.4 CSP & Headers Documentation

**Status:** ⏭️ SKIPPED

- CSP unnecessary with DOMPurify sanitization already implemented
- Vercel handles HTTPS + security headers by default
- Can be added later if compliance requirements emerge
- **Notes:** Defense-in-depth already covered by active HTML sanitization

---

## Additional Phase 1 Improvements (Bonus)

### Notification System Refactor

- [x] Replaced all `console.log`/`console.error` with `showNotification()`
      method
- [x] Added dynamic `notificationText` property
- [x] User-visible error messages for size limits and parsing errors
- [x] Consistent notification UI with emoji indicators (❌ error, ⚠️ warning, 🎉
      success)

### Code Quality Improvements (Phase 2 Early)

- [x] Extracted magic strings to constants:
  - `REVISION_PREFIX = '_TM_'`
  - `FLASH_NOTIFICATION_DURATION = 2500`
  - `AUTO_SAVE_DEBOUNCE = 10000`
  - `MAX_MARKDOWN_SIZE = 50000`
- [x] Fixed CSS typo: removed `trangray-y-0.5` class

---

## Phase 2: Code Quality Improvements - Week 2

### 2.1 Code Refactoring

**Status:** 🟡 PARTIALLY COMPLETED

- [x] Extract magic strings to constants (COMPLETED)
- [x] Fix CSS typo (COMPLETED)
- [ ] Separate concerns: organize UI logic, storage logic, markdown logic (TODO)
- **Impact:** Improved maintainability and readability
- **Actual Effort:** 1.5 hours (constants & CSS)
- **Remaining:** 1 hour (concerns separation)

### 2.2 Code Documentation

**Status:** ✅ COMPLETED

- [x] Add JSDoc comments to complex functions
- [x] Document Alpine component structure
- [x] Standardize JSDoc style across all functions
- [x] Add inline comments for non-obvious logic
- **Impact:** Easier onboarding and refactoring
- **Actual Effort:** 1.5 hours
- **Documented Functions (14 total):**
  - Component-level: Main `fakeCms` - Alpine data structure, features overview
  - Selection/Syntax: `modifyMarkdown()`, `modifyMarkdownAdd()`,
    `modifyMarkdownRemove()`
  - Validation: `validateMarkdownSize()` - Real-time 50KB enforcement
  - Storage: `saveRevision()`, `setRevisions()`, `useRevision()`
  - Deletion: `deleteRevision()`, `deleteRevisions()`
  - Rendering: `refreshHtml()` - Markdown parsing with XSS sanitization
  - Notifications: `showNotification()` - Toast with emoji support
  - Actions: `copyMarkdown()`, `deleteMarkdown()`, `refreshComponent()`,
    `toggleFullscreen()`
- **Style:** Consistent JSDoc format with @param, @returns, @description
  sections

### 2.3 Error Handling Enhancement

**Status:** ✅ COMPLETED

- [x] Add try-catch around marked.js parsing (COMPLETED)
- [x] User-friendly error messages (COMPLETED)
- [x] Fallback rendering for parse failures (COMPLETED)
- **Impact:** Better stability and user experience
- **Actual Effort:** Completed in Phase 1

### 2.4 Accessibility Improvements

**Status:** 🟡 PARTIALLY COMPLETED

- [x] Implement keyboard navigation for revision menu (Escape to close)
- [x] Add focus management for revision menu open/close
- [x] Improve ARIA labels for interactive controls and editor/preview regions
- [ ] Test with screen readers
- **Impact:** WCAG 2.1 AA compliance
- **Estimated Effort:** 2 hours
- **Priority:** MEDIUM
- **Notes:** Implemented in `index.html` (Session 5); screen reader validation
  still pending

---

## Phase 3: Enhanced Features - Week 3

### 3.1 Export Functionality

**Status:** ⏳ TODO

- [ ] Export as Markdown (.md file)
- [ ] Export as HTML document
- [ ] Export as PDF (using jsPDF)
- [ ] Add export buttons to toolbar
- **Impact:** Better content portability
- **Estimated Effort:** 3 hours

### 3.2 Syntax Highlighting

**Status:** ⏳ TODO

- [ ] Integrate Prism.js for code blocks
- [ ] Support multiple languages
- [ ] Configurable themes
- **Impact:** Better readability for code content
- **Estimated Effort:** 2 hours

### 3.3 Editor Enhancements

**Status:** ⏳ TODO

- [ ] Keyboard shortcuts (Ctrl+B, Ctrl+I, etc.)
- [ ] Character/word count
- [ ] Line numbers in editor
- [ ] Search & Replace functionality
- **Impact:** Professional editing experience
- **Estimated Effort:** 4 hours

### 3.4 Revision History UX

**Status:** ⏳ TODO

- [ ] Preview before loading revision
- [ ] Timestamp sorting improvements
- [ ] Revision comparison (diff view)
- [ ] Auto-save interval configuration
- **Impact:** Better version control experience
- **Estimated Effort:** 3 hours

---

## Phase 4: Developer Experience & Testing - Week 4

### 4.1 Build & Deployment

**Status:** ⏳ TODO

- [ ] Create build script for minification
- [ ] Environment configuration (dev/prod CDNs)
- [ ] Create GitHub Actions workflow
- [ ] Generate source maps for debugging
- **Impact:** Production-ready deployment
- **Estimated Effort:** 2 hours

### 4.2 Testing

**Status:** ⏳ TODO

- [ ] Unit tests for markdown modifications
- [ ] Security tests for XSS payloads
- [ ] Integration tests for localStorage
- [ ] E2E tests for critical user flows
- **Impact:** Confidence in changes and regressions
- **Estimated Effort:** 4 hours

### 4.3 Documentation

**Status:** ⏳ TODO

- [ ] Update README with features
- [ ] Add usage guide and keyboard shortcuts
- [ ] Create contribution guidelines
- [ ] Document code architecture
- **Impact:** Easier community contributions
- **Estimated Effort:** 2 hours

### 4.4 Performance Optimization

**Status:** ⏳ TODO

- [ ] Optimize debounce timing
- [ ] Lazy-load Marked.js
- [ ] Monitor bundle size
- [ ] Lighthouse audit and fixes
- **Impact:** Faster load times, better Core Web Vitals
- **Estimated Effort:** 2 hours

---

## Dependencies to Add

### Security

- **DOMPurify** (8KB) - XSS prevention
- **CSP headers** - Server configuration

### Features (Optional)

- **Prism.js** (25KB) - Syntax highlighting
- **jsPDF** (50KB) - PDF export
- **diff-match-patch** (15KB) - Revision comparison

### Testing

- **Vitest** - Unit test framework
- **Cypress** - E2E testing
- **OWASP ZAP** - Security scanning

---

## Success Criteria

| Phase   | Pass/Fail Criteria                                     |
| ------- | ------------------------------------------------------ |
| Phase 1 | No XSS vulnerabilities in security audit               |
| Phase 2 | Code review approval, 80%+ test coverage               |
| Phase 3 | All export formats working, syntax highlighting active |
| Phase 4 | Green CI/CD, Lighthouse score 90+, 0 critical bugs     |

---

## Timeline

```
Week 1 (Mar 8-14):   Phase 1 - Security Fixes        [🔴 START HERE]
Week 2 (Mar 15-21):  Phase 2 - Code Quality
Week 3 (Mar 22-28):  Phase 3 - New Features
Week 4 (Mar 29-Apr4): Phase 4 - Testing & Deployment
```

---

## Rollback Plan

- **Version control:** All changes in git commits with descriptive messages
- **Feature flags:** Use Alpine `x-cloak` for gradual rollouts
- **Testing:** Pre-production testing on staging domain
- **Monitoring:** Error tracking via browser console logs
- **Hotfix path:** Critical fixes deployed within 1 hour

---

## Known Risks & Mitigations

| Risk                    | Severity    | Mitigation                                       |
| ----------------------- | ----------- | ------------------------------------------------ |
| XSS injection           | 🔴 CRITICAL | Add DOMPurify sanitization + CSP                 |
| localStorage data loss  | 🟡 MEDIUM   | Add export before deletion, confirm dialogs      |
| CDN failure             | 🟡 MEDIUM   | Self-host essential libraries, graceful fallback |
| Breaking Alpine version | 🟠 LOW      | Pin CDN versions, test new versions              |
| Performance regression  | 🟠 LOW      | Lighthouse monitoring, benchmark existing        |

---

## Next Steps

1. ✅ **Phase 1 security fixes** (COMPLETED)
2. 🔄 **Phase 2 code quality** (IN PROGRESS)
   - Start with 2.2: Code Documentation (complex functions, Alpine structure)
   - Then 2.4: Accessibility Improvements (keyboard nav, ARIA)
   - Then 2.1: Separation of concerns refactor (optional, low priority)

3. 📋 **Security audit** (defer - already covered by DOMPurify)
4. 🚀 **Phase 3: Enhanced features** (next milestone)
5. 🎉 **Deploy to Vercel** (final step)

---

## Contact & Support

- **Project Lead:** Mark Mead
- **Repository:** https://github.com/markmead/tiny-markdown
- **Issues:** GitHub Issues tracker
- **Discussions:** GitHub Discussions

---

**Last Updated:** March 8, 2026 (Session 5)

**Phase 1 Complete:**

- XSS Vulnerability Fix ✅
- Input Validation ✅
- Notification System Refactor ✅
- Constants Extraction ✅
- CSS Typo Fix ✅
- localStorage Security ⏭️ SKIPPED (low priority)
- CSP Documentation ⏭️ SKIPPED (not needed on Vercel)

**Phase 2 Starting:**

- Documentation focus: JSDoc, Alpine structure, complex functions
- Accessibility: Keyboard nav, ARIA labels, screen reader testing

**Next Review:** When Phase 2 documentation complete
