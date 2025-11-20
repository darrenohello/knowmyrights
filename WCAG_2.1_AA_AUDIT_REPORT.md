# WCAG 2.1 AA Accessibility Audit Report
## Know My Rights Pre-Launch Page

**Date:** 2025-01-27  
**Scope:** `index.html`, `about.html`, `style.css`, and related assets  
**Standard:** WCAG 2.1 Level AA

---

## High-Level Summary

- **Critical:** Missing `<h1>` heading on homepage (index.html) - page structure relies on image logo instead of semantic heading
- **High:** Multiple decorative images have empty `alt=""` attributes, which is correct, but some functional images lack descriptive text
- **High:** Skip link is defined in CSS but not implemented in HTML, preventing keyboard users from bypassing navigation
- **High:** Missing visible focus indicators on interactive elements (links, buttons) - keyboard navigation is not clearly visible
- **Medium:** External links missing `rel="noopener noreferrer"` security attribute and indication that they open in new window

---

## Detailed Issues Table

| Severity | WCAG Criterion | Location | Problem | Suggested Fix |
|----------|---------------|----------|---------|---------------|
| **Critical** | 1.3.1 Info and Relationships | `index.html:50-51` | Missing `<h1>` heading on homepage. The main heading is an image (`kmr-hero-logo`), which breaks heading hierarchy and screen reader navigation. | Add `<h1 class="visually-hidden">Know My Rights</h1>` before the logo image, or uncomment and use the existing h1 on line 50. Alternatively, add `role="img" aria-label="Know My Rights"` to the image and ensure proper heading structure. |
| **High** | 2.4.1 Bypass Blocks | `index.html:17-34`, `about.html:16-33` | Skip link CSS exists (`.skip-link` in `style.css:191-207`) but no skip link is present in HTML. Keyboard users cannot bypass repetitive navigation. | Add `<a href="#main-content" class="skip-link">Skip to main content</a>` as the first element in `<body>`, and add `id="main-content"` to the `<main>` element. |
| **High** | 2.4.7 Focus Visible | `style.css` (throughout) | No visible focus styles defined for interactive elements (links, buttons). Default browser focus may be insufficient or removed by CSS resets. | Add focus styles: `a:focus-visible, button:focus-visible { outline: 3px solid var(--kmr-purple-700); outline-offset: 2px; }` and ensure buttons/links have visible focus indicators. |
| **High** | 1.1.1 Non-text Content | `index.html:85,93,101,109` | Decorative/icon images have empty `alt=""` which is correct, but screen readers won't announce them. Consider if they need descriptive text. | Verify these are purely decorative. If they convey meaning, add descriptive alt text (e.g., `alt="Clock icon representing time-efficient learning"`). |
| **High** | 1.1.1 Non-text Content | `index.html:39,51` | Hero images may be considered "images of text" (logo text). While they have alt text, consider if text equivalent is sufficient. | Ensure alt text matches the visual text exactly: `alt="Know My Rights"` for logo images. Consider adding text fallback if possible. |
| **Medium** | 4.1.2 Name, Role, Value | `index.html:126`, `about.html:185-186` | External links with `target="_blank"` missing `rel="noopener noreferrer"` (security) and indication they open in new window. | Add `rel="noopener noreferrer"` and `aria-label="[link text] (opens in new window)"` or append visually hidden text: `<span class="visually-hidden"> (opens in new window)</span>`. |
| **Medium** | 1.4.3 Contrast (Minimum) | `style.css:24,25,36,66,67` | Need to verify contrast ratios. `--kmr-purple-900` (rgb(35.7% 6.67% 42%)) on `--kmr-off-white` (rgb(97.3% 96.1% 93.7%)) and `--kmr-purple-700` (rgb(49% 21.2% 53.7%)) on white need testing. | Test contrast: Purple-900 (#5B1A6B) on off-white (#F8F5EF) and Purple-700 (#7D3A89) on white. Ensure 4.5:1 for normal text, 3:1 for large text. Adjust if needed. |
| **Medium** | 1.4.3 Contrast (Minimum) | `style.css:282,286` | Link colors `--kmr-blue-700` and `--kmr-blue-900` on white/off-white backgrounds need contrast verification. | Verify `--kmr-blue-700` (rgb(7.45% 35.7% 63.9%)) and `--kmr-blue-900` (rgb(0% 26.3% 43.9%)) meet 4.5:1 contrast ratio on background. |
| **Medium** | 2.4.4 Link Purpose (In Context) | `index.html:54` | Link text "About Know My Rights" is descriptive, but could be more specific in context. | Current text is acceptable, but consider if context makes purpose clear. Ensure link text is unique and descriptive. |
| **Medium** | 1.3.1 Info and Relationships | `index.html:78-119` | Section "The Learning Experience" uses `<h2>` followed by `<h3>`, which is correct. However, verify no heading levels are skipped elsewhere. | Verify heading hierarchy: h1 → h2 → h3 (no skipped levels). Current structure appears correct. |
| **Low** | 2.4.6 Headings and Labels | `index.html:51` | Logo image uses `alt="Know My Rights"` which is good, but if it's the primary heading, consider using `<h1>` with the image as background or alongside. | Consider using `<h1><img src="..." alt="Know My Rights"></h1>` structure if the logo is the primary heading. |
| **Low** | 4.1.3 Status Messages | N/A | No dynamic content or status messages detected. If JavaScript is added later, ensure ARIA live regions are implemented. | N/A - No current issues, but be mindful when adding interactive features. |
| **Low** | 2.5.3 Label in Name | `index.html:54` | Button link "About Know My Rights" - verify accessible name matches visible text. | Current implementation is correct - accessible name matches visible text. |
| **Low** | 1.4.11 Non-text Contrast | `style.css:669,677` | Button borders may need contrast verification. `--kmr-purple-500` border on buttons should meet 3:1 contrast ratio. | Verify button border colors meet 3:1 contrast ratio against button background. |

---

## Colour Contrast Review

### Critical Combinations to Test:

1. **Primary Text:**
   - `--kmr-purple-900` (#5B1A6B) on `--kmr-off-white` (#F8F5EF)
   - `--kmr-purple-700` (#7D3A89) on white (#FFFFFF)
   - `--kmr-purple-900` on white

2. **Links:**
   - `--kmr-blue-700` (#13335A) on white
   - `--kmr-blue-900` (#004370) on white
   - `--kmr-purple-700` on white/off-white

3. **Buttons:**
   - White text on `--gradient-kmr-brand` (purple-900 to purple-700 gradient)
   - Purple-900 text on `--kmr-purple-100` background

4. **Footer:**
   - Text on `--kmr-purple-100` background

**Recommendation:** Use a contrast checker tool (e.g., WebAIM Contrast Checker) to verify all combinations meet WCAG AA requirements (4.5:1 for normal text, 3:1 for large text/UI components).

---

## Keyboard & Focus Review

### Issues Found:

1. **Missing Focus Styles:** No explicit focus styles defined in CSS. Default browser focus may be removed or insufficient.

2. **Skip Link Missing:** CSS for skip link exists but HTML implementation is missing.

3. **Tab Order:** Appears logical (header → main content → footer), but verify with keyboard navigation.

4. **Interactive Elements:**
   - Navigation links: Should have visible focus
   - Button links: Should have visible focus
   - External links: Should have visible focus

### Recommended Fixes:

```css
/* Add to style.css */
a:focus-visible,
button:focus-visible {
    outline: 3px solid var(--kmr-purple-700);
    outline-offset: 2px;
    border-radius: 2px;
}

a.btn:focus-visible {
    outline: 3px solid white;
    outline-offset: 2px;
}

/* Ensure skip link is visible on focus */
.skip-link:focus {
    top: 88px; /* Already defined, ensure it works */
    outline: 3px solid var(--kmr-purple-700);
}
```

---

## Headings, Landmarks & DOM Structure

### Current Structure Analysis:

**index.html:**
- ✅ Has `<main>` landmark
- ✅ Has `<header>` landmark  
- ✅ Has `<footer>` landmark
- ✅ Has `<nav>` with `aria-label`
- ❌ **Missing `<h1>`** - Critical issue
- ✅ Section uses `<h2>` appropriately
- ✅ No skipped heading levels detected

**about.html:**
- ✅ Has `<h1>` ("About Know My Rights")
- ✅ Proper heading hierarchy (h1 → h2 → h3)
- ✅ All landmarks present

### Recommendations:

1. **Add h1 to index.html** (Critical)
2. Consider adding `aria-label` to sections if they have specific purposes
3. Verify all sections have appropriate headings

---

## Link & Button Text Improvements

### Current Link Text Analysis:

| Location | Current Text | Assessment | Recommendation |
|----------|--------------|------------|----------------|
| `index.html:54` | "About Know My Rights" | ✅ Descriptive | Keep as is |
| `index.html:126` | "Ausmed Education" | ✅ Descriptive | Add "(opens in new window)" indicator |
| `index.html:126` | "National Disability Insurance Agency" | ✅ Descriptive | Add "(opens in new window)" indicator |
| `about.html:173` | "Add to my calendar 🗓️" | ⚠️ Emoji may not be announced | Consider text alternative or `aria-label` |
| `about.html:185-186` | External links | ✅ Descriptive | Add "(opens in new window)" indicator |

**Recommendations:**
- All link text is descriptive and contextually clear
- Add visual and screen reader indication for external links
- Consider replacing emoji with text or adding `aria-label` for calendar link

---

## ARIA & Custom Components

### Current ARIA Usage:

**Good Practices:**
- ✅ `<nav aria-label="Primary site navigation">` on both pages
- ✅ Semantic HTML used appropriately

**Issues:**
- ❌ No ARIA landmarks beyond basic HTML5 elements (acceptable, but could be enhanced)
- ❌ Commented-out mobile menu button has proper ARIA attributes, but since it's commented, no issue

**Recommendations:**
- Current ARIA usage is minimal and appropriate
- No custom widgets detected that require ARIA
- When mobile menu is implemented, ensure proper ARIA states (`aria-expanded`, `aria-controls`)

---

## Prioritised Action Plan

### 🔴 Must Fix Before Launch (Critical/High)

1. **Add `<h1>` heading to index.html**
   - **File:** `index.html`
   - **Location:** Line 50-51
   - **Fix:** Uncomment h1 or add `<h1 class="visually-hidden">Know My Rights</h1>` before logo image
   - **WCAG:** 1.3.1 Info and Relationships

2. **Implement skip link in HTML**
   - **File:** `index.html`, `about.html`
   - **Location:** First element in `<body>`
   - **Fix:** Add `<a href="#main-content" class="skip-link">Skip to main content</a>` and `id="main-content"` to `<main>`
   - **WCAG:** 2.4.1 Bypass Blocks

3. **Add visible focus styles**
   - **File:** `style.css`
   - **Location:** Add after line 207 (after skip-link styles)
   - **Fix:** Add focus-visible styles for all interactive elements (see code above)
   - **WCAG:** 2.4.7 Focus Visible

4. **Verify and fix color contrast**
   - **File:** `style.css`
   - **Location:** Variables section and throughout
   - **Fix:** Test all text/background combinations, adjust colors if needed
   - **WCAG:** 1.4.3 Contrast (Minimum)

5. **Add descriptive alt text to icon images (if needed)**
   - **File:** `index.html`
   - **Location:** Lines 85, 93, 101, 109
   - **Fix:** Verify if icons are decorative (keep `alt=""`) or informative (add descriptive text)
   - **WCAG:** 1.1.1 Non-text Content

### 🟡 Should Fix Soon (Medium)

6. **Add `rel="noopener noreferrer"` to external links**
   - **File:** `index.html`, `about.html`
   - **Location:** Lines with `target="_blank"`
   - **Fix:** Add `rel="noopener noreferrer"` to all external links
   - **WCAG:** 4.1.2 Name, Role, Value (security best practice)

7. **Indicate external links open in new window**
   - **File:** `index.html`, `about.html`
   - **Location:** External links
   - **Fix:** Add `aria-label` with "(opens in new window)" or visually hidden text
   - **WCAG:** 3.2.4 Consistent Identification

8. **Review calendar link emoji**
   - **File:** `about.html`
   - **Location:** Line 173
   - **Fix:** Add `aria-label` or replace emoji with text alternative
   - **WCAG:** 1.1.1 Non-text Content

### 🟢 Nice to Improve (Low)

9. **Consider h1 structure for logo**
   - **File:** `index.html`
   - **Location:** Line 51
   - **Fix:** Consider wrapping logo in `<h1>` if it's the primary heading
   - **WCAG:** 2.4.6 Headings and Labels

10. **Add visually-hidden utility class**
    - **File:** `style.css`
    - **Location:** Utilities section
    - **Fix:** Add `.visually-hidden { position: absolute; width: 1px; height: 1px; padding: 0; margin: -1px; overflow: hidden; clip: rect(0,0,0,0); white-space: nowrap; border: 0; }`
    - **Purpose:** For screen reader-only text

11. **Verify button border contrast**
    - **File:** `style.css`
    - **Location:** Button styles
    - **Fix:** Ensure button borders meet 3:1 contrast ratio
    - **WCAG:** 1.4.11 Non-text Contrast

---

## Implementation Notes

### CSS Additions Needed:

```css
/* Add visually-hidden utility */
.visually-hidden {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border: 0;
}

/* Focus styles */
a:focus-visible,
button:focus-visible {
    outline: 3px solid var(--kmr-purple-700);
    outline-offset: 2px;
    border-radius: 2px;
}

a.btn:focus-visible {
    outline: 3px solid white;
    outline-offset: 2px;
}

a.btn.kmr-primary:focus-visible {
    outline: 3px solid white;
    outline-offset: 2px;
}
```

### HTML Changes Needed:

**index.html:**
- Add skip link as first element in `<body>`
- Add `id="main-content"` to `<main>`
- Add or uncomment `<h1>` heading
- Add `rel="noopener noreferrer"` to external links
- Add external link indicators

**about.html:**
- Add skip link as first element in `<body>`
- Add `id="main-content"` to `<main>`
- Add `rel="noopener noreferrer"` to external links
- Add external link indicators

---

## Testing Recommendations

1. **Keyboard Navigation:** Tab through entire page, verify focus is visible and logical
2. **Screen Reader Testing:** Test with NVDA (Windows) or VoiceOver (Mac)
3. **Color Contrast:** Use WebAIM Contrast Checker or browser DevTools
4. **Automated Testing:** Run axe DevTools or WAVE browser extension
5. **Manual Review:** Verify all images have appropriate alt text

---

**End of Audit Report**

