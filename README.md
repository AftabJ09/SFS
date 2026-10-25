# FileShelf — static Google Drive download library

A plain HTML/CSS/JavaScript website. No database, backend, framework, or build step is required.

## Files
- `index.html` — website UI and search/tag filtering
- `data.json` — edit this to add/change the site title, description, tags, file links, and images
- `assets/default-file.svg` — fallback image used when an image is blank or fails to load

## Add a file
Add an object to `items` in `data.json`:

```json
{
  "id": "java-notes",
  "title": "Java Notes PDF",
  "description": "Concise notes for revision.",
  "tags": ["java", "notes", "pdf"],
  "image": "assets/java-notes.jpg",
  "driveUrl": "https://drive.google.com/file/d/FILE_ID/view?usp=sharing",
  "fileName": "java-notes.pdf"
}
```

- JSON must use double quotes and commas correctly.
- Put local images in `assets/` and use paths such as `assets/java-notes.jpg`, or use a publicly accessible image URL.
- `fileName` is currently informational; Google Drive determines the actual download filename.
- `id` should be unique, but is not currently used by the page.
- Use `[]` for no tags and `""` for no custom image.

## Google Drive download behavior
1. In Drive, set the file's General access to **Anyone with the link** (only for files you are allowed to distribute).
2. Copy a link like `https://drive.google.com/file/d/FILE_ID/view?usp=sharing`.
3. The page converts the common `/file/d/FILE_ID/view` form to `https://drive.google.com/uc?export=download&id=FILE_ID`.
4. Google may still show a warning/confirmation, preview, or download prompt for large files, quota-limited files, or certain file types. A static website cannot guarantee a silent download for every Drive file. If a link is not a standard Drive file URL, it is left unchanged.

## Run locally
Browsers often block `fetch("data.json")` from a `file://` URL. Start a local server in this folder instead.

If Python is installed:
```bash
python -m http.server 8000
```
Then open `http://localhost:8000`.

Alternatively, deploy the folder to any static host (for example GitHub Pages, Cloudflare Pages, or Netlify). Upload the whole folder, keeping `index.html`, `data.json`, and `assets/` together.

## Updating content
Edit `data.json` and redeploy/upload the changed JSON file. The page fetches it with `cache: "no-store"`; some hosting/CDN layers may still cache it briefly.
