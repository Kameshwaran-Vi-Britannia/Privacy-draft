# Weekly Privacy Checklist — PrivacyGuard

A static, browser-only privacy-awareness dashboard. It reads the real sections and items from `02_privacy_checklist.html`, selects a featured weekly item, and makes editable/shareable awareness drafts. The original checklist is kept as a separate file and is not modified by this app.

## Project files

```text
weekly-privacy-checklist/
├── index.html                  # Complete app: markup, styles, and vanilla JavaScript
├── 02_privacy_checklist.html   # Your original source checklist; keep this beside index.html
├── manus-routes.json           # Preview route declaration; harmless on GitHub Pages
└── README.md                   # These instructions
```

Do not rename the checklist file. Its filename and location must remain exactly `02_privacy_checklist.html` in the same published folder as `index.html`. The app fetches it using a same-origin path, then reads the checklist's literal JavaScript `DATA` array as data; it does not execute the source script or use `eval()`.

## Upload to GitHub

1. Sign in to GitHub and create a repository, or open the repository where you want the site. The repository root is the folder that GitHub Pages will publish.
2. In the repository, choose **Add file → Upload files**.
3. Upload `index.html`, `02_privacy_checklist.html`, and `manus-routes.json` to the repository root. You may also upload this `README.md`. Keep the original checklist file unchanged.
4. Scroll to **Commit changes**, use the `main` branch (or the repository's default branch), and commit the files.

The two HTML files must be next to each other at the root. For example, do not upload only `index.html`, and do not put the checklist inside a different folder.

## Enable GitHub Pages

1. In the repository, open **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
3. Choose the branch where you uploaded the files (usually `main`) and select the `/(root)` folder, then choose **Save**.
4. Wait for the Pages deployment to finish. Open the site URL shown on the Pages settings screen. For a project repository, the URL is normally under `https://<your-account>.github.io/<repository>/`.
5. Confirm that the site loads and that the banner says the categories and items were loaded from the source checklist.

To publish later edits, upload or commit the changed file(s) to the same branch and folder. If you change the original checklist, keep its filename and ensure its content still has a supported literal `DATA` array; the app reports an error rather than inventing replacement items if it cannot parse the source.

## Local preview

Opening `index.html` by double-clicking it (`file://`) cannot load the checklist because browsers restrict local-file fetches. Preview it through GitHub Pages or a local static HTTP server. For example, from the project folder you may run `python3 -m http.server 8000` if Python is installed, then open `http://localhost:8000/`.

## Testing checklist

- The page loads the adjacent checklist and reports the extracted category and item counts (the supplied checklist currently has 8 sections and 47 items).
- The featured weekly card shows the exact source section and original item. Refresh the page during the same week; the featured item should stay the same in that browser.
- Select a category chip or dropdown category and generate a draft; check that the source label and quoted original checklist item match that category.
- Copy the complete draft and paste it into a text editor. Download a draft and confirm the `.txt` file includes its source reference.
- Save a draft, refresh, confirm it remains listed, then try deleting one draft. Try **Clear all drafts** and cancel once, then confirm it when ready.
- Open the site using the repository URL (including its repository subpath), not only from a local root URL.
- For a missing-source check, temporarily move or rename `02_privacy_checklist.html` in a test copy, reload, and confirm the app shows a clear error and no generated checklist tip. Restore the source file afterward.
- Resize the browser to a narrow phone width and check that the dashboard, category controls, generated draft, and saved-draft actions remain readable and usable.

## Known limitations

- GitHub Pages is static hosting. The weekly selection and draft are computed in the visitor's browser when the page is opened; no job runs while the site is closed. The same browser keeps the current week's selection so ordinary refreshes do not randomly change it.
- Saved drafts use `localStorage` on the current browser/device. They do not synchronize to another device or browser and may be cleared with browser data.
- The draft generator is a deterministic, offline template; it is not generative AI and does not look up live legal or policy information. It uses the actual source checklist item, a plain-language action transformation, and a conservative closing reminder. For current details on rights-related topics, check an appropriate official source independently.
- The source reader supports the supplied checklist's literal, JSON-compatible JavaScript `DATA` array. It intentionally does not execute arbitrary JavaScript. If the source structure changes to computed data or a non-JSON-compatible literal, the page displays an extraction error until its parser is updated.
- Clipboard permission and file downloads depend on the browser. Clipboard copy may be restricted in some contexts; the app announces failures. Drafts are generated and stored locally and are not sent to an external service.
