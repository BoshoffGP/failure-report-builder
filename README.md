# Failure Report Builder

A single-file web app that creates failure reports (PowerPoint `.pptx`) from photos and job details.

- **Home screen:** **Create Report** starts a new blank report. **Previous reports** lists every report created or saved, newest first, with search, a thumbnail, **Open** and **Delete**.
- **Dashboard:** choose the company at the top of Job details, upload photos, add descriptions and damage marks, and fill in the job form. The heading beside the photos defaults to DESCRIPTION; you can pick COMMENTS or type your own, which is remembered.
- **Sign in:** the home screen asks for an email address and the access code before Create Report / Previous reports are available. The sign-in lasts for the browser session (a reload keeps you signed in); **⎋ Sign out** is in the top bar. The last email is remembered to prefill the form. Note: this is a simple client-side gate for an offline file, not server-side security.
- **Top bar:** **New report** clears the current report. **Save report** saves the editable report (`.json` with photos, descriptions, marks, company and heading) to a folder you choose (Chrome/Edge "Save as" dialog; other browsers download it) and keeps it in Previous reports. **Create Report** downloads the `.pptx` and keeps a full copy in Previous reports. Re-creating a report you opened updates its entry. ⌂ (or the title) goes back to Home.
- **Colour codes (Settings → Colour scheme):** type a hex code and click **✔ Apply** (or press Enter) to preview it on the sample report and the builder. Invalid codes show an error. The preview is only kept when you click **💾 Save** or **✔ Use for this report**; leaving Settings, switching company or going Home without saving puts the saved colours back. The colour-picker swatches and suggested colours preview the same way.
- **✨ AI colour match (Settings → Colour scheme):** optional per company. When switched on, the logo is analysed on this computer (no internet, nothing uploaded) and the accent colour, dark colour and header style are set to match it, with contrast checked for readable header text. It re-matches when you upload a new logo or click **↻ Re-match**. Switching it off again restores the colours and header style you had before it was switched on (remembered per company, even after closing the app). Changing a colour by hand while it is on switches it off and keeps your hand-picked colour.

## Link

**Live app:** https://boshoffgp.github.io/failure-report-builder/

## Add it as a module (iframe)

```html
<iframe src="https://boshoffgp.github.io/failure-report-builder/"
        style="width:100%;height:100vh;border:0"
        allow="clipboard-write"
        title="Failure Report Builder"></iframe>
```

If your system **sandboxes** iframes, these permissions are required, otherwise the report downloads, the Save report dialog, file pickers, confirm dialogs and storage will not work:

```html
<iframe src="https://boshoffgp.github.io/failure-report-builder/"
        style="width:100%;height:100vh;border:0"
        allow="clipboard-write"
        sandbox="allow-scripts allow-downloads allow-same-origin allow-modals allow-popups allow-forms"
        title="Failure Report Builder"></iframe>
```

Downloading the generated `.pptx` from inside an iframe works in current Chrome, Edge, Firefox and Safari. Inside a cross-origin iframe the Save report "Save as" dialog may be blocked by the browser; the app then falls back to a normal download.

## How it works / data

- **Fully client-side.** There is no server or database. Photos and report data never leave the user's browser. The `.pptx` is built locally (PptxGenJS is bundled in the file).
- **Each open starts at the home screen with a blank report.** To continue a report later, open it from **Previous reports**.
- **Previous reports** are stored in the browser's IndexedDB (photos included), also per browser and per domain.
- **Company profiles** (logo, colours, details), settings and the remembered drop-down lists are stored in the browser's `localStorage`. That storage is **per browser and per domain**: profiles made on `boshoffgp.github.io` do not show up when the app is served from another URL (for example your own system), or in another browser or PC.
- **Moving companies between computers / browsers:** Settings → **⬇ Export companies** downloads `frb-companies.json` (all companies with logos, colours and details). On the other computer or the online version, Settings → **⬆ Import companies** adds them (companies with the same name are updated, nothing is duplicated).
  - The export/import controls for profiles and drop-down history are hidden in this version (the functions are still built in). Ask us if you need to move them to another URL.
- Works offline once loaded, and also by just double-clicking the downloaded HTML file.

## Self-hosting inside your own system

Download the single HTML file and serve it from your own domain (no build step, no dependencies):

- Raw file: https://raw.githubusercontent.com/BoshoffGP/failure-report-builder/main/index.html
- `curl -L -o failure-report-builder.html https://raw.githubusercontent.com/BoshoffGP/failure-report-builder/main/index.html`

Remember: if you self-host, it runs on your domain, so profiles need to be imported once there (see above).

## Built-in company profiles

Black Rock Equipment (default) and HJ Stander. Companies are managed in the **Settings** tab (upload logo, pick colours, enter details, then click **Save**). The company for each report is chosen at the top of Job details.

Black Rock Equipment uses its original black & yellow scheme: gold `#F0B429`, navy-black `#14213D` and dark gold `#B7791F` for small accent text.
