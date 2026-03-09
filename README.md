# cyclonedx2report

`cyclonedx2report` is an open-source, browser-first tool that converts a CycloneDX JSON SBOM into an interactive HTML report.

[![Live Demo](https://img.shields.io/badge/Live-GitHub%20Pages-2563eb?style=for-the-badge)](https://cyclonedx2report.github.io/)
![Open Source](https://img.shields.io/badge/Open%20Source-Yes-16a34a?style=for-the-badge)
![Runtime](https://img.shields.io/badge/Runtime-Browser%20Only-7c3aed?style=for-the-badge)
![Backend](https://img.shields.io/badge/Backend-None-0891b2?style=for-the-badge)
![Data Storage](https://img.shields.io/badge/Server%20Storage-None-f59e0b?style=for-the-badge)
![URL Payload](https://img.shields.io/badge/Share%20Format-%23pako-9333ea?style=for-the-badge)

## Project KPIs

| KPI | Value |
|---|---|
| Hosting | GitHub Pages (static) |
| Data processing | 100% client-side in browser |
| Server-side SBOM storage | None |
| Share link mode | URL fragment `#pako:...` |
| Backend requirement | Not required |
| Main report blocks | Summary, Sankey, Components, Vulnerabilities |

The report includes:
- Summary KPIs
- Dependency visualization (Sankey)
- Components table with filters
- Vulnerabilities table with impact context

## Privacy-first by design

This project is designed to run **entirely in the browser**.

- No backend is required
- No SBOM upload to a server
- No project data persistence on server-side storage
- SBOM data is compressed in the URL fragment as `#pako:...`

### Important detail about `#pako:...`

The payload is stored in the **URL fragment** (the part after `#`).
In browsers, the fragment is handled client-side and is **not sent to the web server** in the HTTP request.

That means report data stays in your navigator/browser session and link content, not in a backend database.

## How it works

1. Open [CycloneDx2Report](https://cyclonedx2report.github.io/)
2. Select a CycloneDX JSON file
3. Generate report
4. The app compresses data with `pako` and opens:
   - `report.html?...#pako:<compressed-payload>`
5. `report.html` decompresses the payload in-browser and renders the report

## Tech stack

- Plain HTML/CSS/JavaScript
- [ECharts](https://echarts.apache.org/) for the Sankey chart
- [Pako](https://github.com/nodeca/pako) for gzip compression/decompression in browser

## Run locally

Because browsers restrict some features on `file://`, serve the folder with a local HTTP server:

### Python

```bash
python -m http.server 8000
```

Then open:

- `http://localhost:8000/index.html`

## Shareability

Generated links are cross-device shareable as long as the URL length is accepted by the destination browser/tool.

For very large SBOMs, URL length can still be a practical limit.

## Contributing

Issues and pull requests are welcome.

If you contribute, please keep the project principles:
- Client-side only processing
- No server-side SBOM storage
- Clear, auditable JavaScript logic

## Security notes

- Treat shared links as sensitive when they contain private dependency data.
- Avoid posting report links publicly if your SBOM includes internal package names or metadata.
