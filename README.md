# Failure Report Builder

A single-file web app that creates failure reports (PowerPoint `.pptx`) from photos and job details. You upload photos, add descriptions and damage marks, fill in the job form and click **Create Report**. The report is generated in the browser and downloaded.

## Link

**Live app:** https://boshoffgp.github.io/failure-report-builder/

## Add it as a module (iframe)

```html
<iframe src="https://boshoffgp.github.io/failure-report-builder/"
        style="width:100%;height:100vh;border:0"
        allow="clipboard-write"
        title="Failure Report Builder"></iframe>
```

If your system **sandboxes** iframes, these permissions are required, otherwise the report/draft downloads, file pickers, confirm dialogs and storage will not work:

```html
<iframe src="https://boshoffgp.github.io/failure-report-builder/"
        style="width:100%;height:100vh;border:0"
        allow="clipboard-write"
        sandbox="allow-scripts allow-downloads allow-same-origin allow-modals allow-popups allow-forms"
        title="Failure Report Builder"></iframe>
```

Downloading the generated `.pptx` from inside an iframe works in current Chrome, Edge, Firefox and Safari.

## How it works / data

- **Fully client-side.** There is no server or database. Photos and report data never leave the user's browser. The `.pptx` is built locally (PptxGenJS is bundled in the file).
- **Each new open is a blank report.** To continue a report later, use **Save draft** (a `.json` file) and **Open draft…**.
- **Company profiles** (logo, colours, details), settings and the remembered drop-down lists are stored in the browser's `localStorage`. That storage is **per browser and per domain**: profiles made on `boshoffgp.github.io` do not show up when the app is served from another URL (for example your own system), or in another browser or PC.
  - To move them, use **Settings → Export profiles… / Import profiles…** for companies, and **★ Saved lists** (export/import) for the drop-down history.
- Works offline once loaded, and also by just double-clicking the downloaded HTML file.

## Self-hosting inside your own system

Download the single HTML file and serve it from your own domain (no build step, no dependencies):

- Raw file: https://raw.githubusercontent.com/BoshoffGP/failure-report-builder/main/index.html
- `curl -L -o failure-report-builder.html https://raw.githubusercontent.com/BoshoffGP/failure-report-builder/main/index.html`

Remember: if you self-host, it runs on your domain, so profiles need to be imported once there (see above).

## Built-in company profiles

Black Rock Equipment (default) and HJ Stander. More companies can be added under **Settings** (upload logo, pick colours, enter details).
