# Mobile Responsiveness Plan for Hajo J. Theunissen Site

## Status

**Prototype (gedsmall/) - COMPLETED**
- Tested on `index 4.html` and `De bron.html`
- Desktop appearance verified identical via screenshot comparison
- Mobile rendering verified working at 390px viewport
- Long poem titles stay on single line (horizontal scroll enabled)
- Hover effect added (italic on mouseover, desktop only)

**Full site (gedichten/) - PENDING**

---

## Changes Required for Full Site (gedichten/)

### 1. Update style1.css

**File:** `/Users/sjsmit/Development/Caden/hajo/gedichten/style1.css`

**Action:** Append the following CSS at the end of the file:

```css
/* Mobile responsiveness */
@media screen and (max-width: 600px) {
    body {
        padding-top: 40px;
        padding-left: 20px;
        padding-right: 20px;
    }

    h1 {
        padding-bottom: 3em;
        font-size: 24px;
    }

    P {
        font-size: 18px;
        white-space: nowrap;
    }

    h2 {
        left: 0;
        text-align: right;
        padding-right: 20px;
    }

    h3 {
        padding-left: 20px;
    }

    h6 {
        padding-right: 20px;
    }
}
```

**Note:** The `white-space: nowrap` on `P` keeps poem titles on a single line in the index. Poems themselves still wrap correctly because they use `<br/>` tags for line breaks.

### 2. Add viewport meta tag to HTML files

**Files:** All HTML files in gedichten/ that are missing the viewport tag.

**Action:** For each HTML file that:
- Uses `style1.css` (111 files)
- Does NOT already have a viewport meta tag

Add the following line in the `<head>` section, after the `<meta http-equiv="Content-Type"...>` line:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

**Pattern to match for insertion point:**
```html
<meta http-equiv="Content-Type" content="text/html;charset=utf-8" />
```
Insert the viewport tag on the next line.

### 3. Add hover effect to index page(s)

**File:** `/Users/sjsmit/Development/Caden/hajo/gedichten/index 4.html` (and any other index pages)

**Action:** In the `<style>` block at the bottom of the file, change the `A:hover` rule:

**Find:**
```css
A:hover { COLOR: black; TEXT-DECORATION: none; font-weight: none }
```

**Replace with:**
```css
A:hover { COLOR: black; TEXT-DECORATION: none; font-style: italic }
```

**Note:** This hover effect only works on desktop (mouse). Mobile/touch devices don't have hover states.

---

## Implementation Script

The following approach can be used:

```bash
# 1. Update style1.css - append media queries
# (Use Edit tool to append the CSS block above to the end of style1.css)

# 2. Find all HTML files using style1.css that need viewport tag
cd /Users/sjsmit/Development/Caden/hajo/gedichten
grep -l "style1.css" *.html | xargs grep -L "viewport"

# 3. Find index files that need hover effect update
grep -l "font-weight: none" *.html
```

For viewport meta tag - for each file in the list:
- Read the file
- Find: `<meta http-equiv="Content-Type" content="text/html;charset=utf-8" />`
- Insert after: `<meta name="viewport" content="width=device-width, initial-scale=1.0" />`

For hover effect - for each index file:
- Read the file
- Find: `A:hover { COLOR: black; TEXT-DECORATION: none; font-weight: none }`
- Replace with: `A:hover { COLOR: black; TEXT-DECORATION: none; font-style: italic }`

---

## Verification

After changes, verify with screenshot comparison:

1. **Desktop test** - Compare live site vs modified local:
   - `https://hajotheunissen.github.io/gedichten/index%204.html` vs local `index 4.html`
   - `https://hajotheunissen.github.io/gedichten/De%20bron.html` vs local `De bron.html`
   - Screenshots should be identical (no visual changes on desktop at rest)

2. **Mobile test** - Take screenshots at 390px viewport width:
   - Verify text is readable
   - Verify poem titles stay on single line (horizontal scroll for long titles)
   - Verify poem content line breaks and indentation preserved

3. **Hover test** (manual) - Open index page in browser, hover over poem titles:
   - Text should become italic on hover
   - Effect should be subtle and immediate

---

## File Counts (gedichten/)

- Total HTML files: 128
- Files using style1.css: 111
- Files already with viewport tag: 4
- Files needing viewport tag: ~107

---

## Reference: Prototype Changes (gedsmall/)

These files were modified in the prototype and serve as reference:

1. `gedsmall/style1.css` - Has mobile media queries appended (including `white-space: nowrap`)
2. `gedsmall/index 4.html` - Has viewport meta tag added + hover effect (font-style: italic)
3. `gedsmall/De bron.html` - Has viewport meta tag added

Screenshots saved in `gedsmall/screenshots/`:
- `index4_live.png` / `index4_local.png` - Desktop comparison (identical)
- `de_bron_live.png` / `de_bron_local.png` - Desktop comparison (identical)
- `index4_mobile.png` - Mobile rendering (all titles on single line)
- `de_bron_mobile.png` - Mobile rendering (poem formatting preserved)
- `index_home_mobile.png` - Homepage mobile rendering
