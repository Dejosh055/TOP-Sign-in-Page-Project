# Sign-In Form

A responsive, accessible sign-in page built with **pure HTML and CSS**. No JavaScript, no frameworks, no libraries. Headings use the **Norse** font and body text uses **Roboto**, both self-hosted as `.woff2` files with `@font-face`.

## Preview

*(Add a screenshot here, e.g. `![Sign-in form](screenshots/preview.png)`)*

**Live demo:** *(add your GitHub Pages link here once deployed)*

## Features

- Centered card layout with a dark, Norse-inspired theme and amber accent
- Custom fonts loaded with `@font-face` (Norse for headings, Roboto for body text)
- Built-in HTML5 validation (`required`, `type="email"`, `minlength`)
- **Validation feedback with CSS only**: green border for valid fields, red border plus an error message for invalid ones, shown only after the user interacts with a field
- Visible focus states and keyboard-friendly controls
- Fully responsive down to small phones
- Respects the user's reduced-motion setting
- Zero JavaScript

## Built With

- HTML5
- CSS3 (custom properties, Flexbox, Grid, pseudo-classes, media queries)
- Fonts: [Norse](#getting-the-fonts) and [Roboto](https://fonts.google.com/specimen/Roboto), as `.woff2`

## Project Structure

```
signin-form/
├── index.html
├── style.css
├── fonts/
│   ├── Norse.woff2
│   ├── Roboto-Regular.woff2
│   └── Roboto-Bold.woff2
└── README.md
```

## Getting the Fonts

The `fonts/` folder is where the three `.woff2` files must go. The CSS expects these **exact file names**.

### 1. Download the fonts

| Font | Where to get it | Files needed |
|---|---|---|
| **Roboto** | [Google Fonts](https://fonts.google.com/specimen/Roboto) → *Get font* → *Download all* | Regular (400) and Bold (700) |
| **Norse** | A free font site such as [Font Squirrel](https://www.fontsquirrel.com), [DaFont](https://www.dafont.com) or [1001 Fonts](https://www.1001fonts.com) | The regular weight |

Always check each font's license before using it in a public project. Roboto is open source (Apache 2.0).

### 2. Convert to `.woff2` (if you only have `.ttf` or `.otf`)

Pick one method:

- **Online:** upload the files to the [Font Squirrel Webfont Generator](https://www.fontsquirrel.com/tools/webfont-generator) or [CloudConvert](https://cloudconvert.com/ttf-to-woff2) and download the `.woff2` output.
- **Command line** (requires Python):
  ```bash
  pip install fonttools brotli
  fonttools ttLib.woff2 compress Norse.ttf
  fonttools ttLib.woff2 compress Roboto-Regular.ttf
  fonttools ttLib.woff2 compress Roboto-Bold.ttf
  ```

### 3. Name and place the files

Rename them if needed and put them in the `fonts/` folder:

```
fonts/Norse.woff2
fonts/Roboto-Regular.woff2
fonts/Roboto-Bold.woff2
```

> Until the files are added, the page still works. It falls back to Georgia (headings) and your system's default sans-serif font (body).

## How `@font-face` Is Used

```css
@font-face {
    font-family: 'Norse';
    src: url('fonts/Norse.woff2') format('woff2');
    font-weight: 400;
    font-style: normal;
    font-display: swap;
}
```

- `font-family` is the name used elsewhere in the stylesheet (`var(--font-heading)`).
- `src` points to the file, **relative to `style.css`**.
- `font-display: swap` shows fallback text immediately, then swaps in the custom font once it loads, so text is never invisible.
- Roboto has two blocks (400 and 700) so bold text uses the real bold file instead of a browser-faked one.

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/signin-form.git
   cd signin-form
   ```
2. Add the font files as described in [Getting the Fonts](#getting-the-fonts).
3. Open `index.html` in your browser. No build step or server is needed.

## How the CSS-Only Validation Works

The form uses native HTML validation attributes, and the stylesheet reacts to the field state:

```css
.field input:user-invalid { border-color: var(--danger); }
.field input:user-valid   { border-color: var(--success); }

.field__error { display: none; }
.field input:user-invalid ~ .field__error { display: block; }
```

`:user-invalid` and `:user-valid` only match **after** the user has interacted with a field, so the page doesn't load covered in red. The sibling selector (`~`) reveals the error message that follows the invalid input.

**Browser note:** `:user-invalid` is supported in current versions of Chrome, Edge, Safari and Firefox. In an older browser the validity colors and error messages simply won't appear, but the form itself still works.

## Important Note on Submission

This project is front-end only. The form uses `action="#"`, so submitting a valid form does not send data anywhere. To make it functional, point `action` at a real server endpoint and always **validate again on the server**, since client-side validation can be bypassed.

## Future Improvements

- [ ] Show/hide password toggle (would need a little JavaScript)
- [ ] Light theme using `prefers-color-scheme`
- [ ] "Create account" and "Forgot password" pages
- [ ] Connect to a backend for real authentication

## Acknowledgments

- [Roboto](https://fonts.google.com/specimen/Roboto) by Christian Robertson (Apache License 2.0)
- Norse font by its original designer (see the license that came with your download)

## License

Released under the [MIT License](LICENSE). Fonts keep their own licenses.