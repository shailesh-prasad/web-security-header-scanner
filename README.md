# AegisHeaderAudit
**Author:** Sailesh Prasad  
**Project type:** Automated web security header and CORS configuration scanner

## Project description
AegisHeaderAudit is a lightweight Python tool that reviews HTTP response security headers and performs a controlled CORS `Origin` probe. It reports common headers that are present or missing, summarizes CORS response settings, and exports a JSON report with an optional CSV summary (CSV is available in the standalone `.py` version).

**Important:** Only scan websites you own or have explicit written permission to assess. This is a defensive configuration checker, not a full vulnerability scanner. Findings require manual validation.

## Technologies used
- Python 3.10+
- `requests` for HTTP requests
- Jupyter Notebook (`.ipynb`) for the notebook deliverable
- JSON and optional CSV for reports

## Files
- `SaileshPrasad_AegisHeaderAudit.ipynb` — notebook project code
- `SaileshPrasad_AegisHeaderAudit.py` — command-line version
- `requirements.txt` — Python runtime dependency list
- `SaileshPrasad_ProjectReport.docx` — project documentation
- `sample_urls.txt` — example target list (replace with authorized targets only)

## Dataset / reference link
The scanner does not require a downloaded dataset: it assesses live HTTP response headers for URLs supplied by the user. The included `sample_urls.txt` is a small example input list, not a benchmark dataset. For the security-header guidance used to frame the checks, see the [OWASP Secure Headers Project](https://owasp.org/www-project-secure-headers/).

## Setup
1. Install Python 3.10 or later.
2. (Recommended) Create and activate a virtual environment.
3. Install dependencies:
   ```bash
   python -m pip install -r requirements.txt
   ```
4. For the notebook, launch Jupyter:
   ```bash
   python -m pip install notebook
   jupyter notebook
   ```
   Open `SaileshPrasad_AegisHeaderAudit.ipynb` and set `TARGETS` to sites you are authorized to test.

## Run the command-line version
Single target:
```bash
python SaileshPrasad_AegisHeaderAudit.py https://example.com
```

Multiple targets:
```bash
python SaileshPrasad_AegisHeaderAudit.py https://example.com https://www.iana.org -o report.json --csv report.csv
```

From a text file:
```bash
python SaileshPrasad_AegisHeaderAudit.py --input sample_urls.txt -o report.json --csv report.csv
```

Output:
- JSON report (default: `aegis_audit_report.json`)
- Optional CSV summary when `--csv` is supplied
- Console summary of headers, CORS settings, and request errors

## Checks performed
The tool records presence/value of:
- `Strict-Transport-Security`
- `Content-Security-Policy`
- `X-Content-Type-Options`
- `X-Frame-Options`
- `Referrer-Policy`
- `Permissions-Policy`

It also reviews `Access-Control-Allow-Origin`, `Access-Control-Allow-Credentials`, methods/headers, and whether a controlled test origin is reflected.

## Limitations
- Missing headers are not automatically vulnerabilities; requirements depend on the application and deployment.
- CORS interpretation depends on endpoint sensitivity, credentials, and origin validation.
- This scanner does not crawl links, authenticate, submit forms, exploit issues, or access private data.
- Network failures, rate limiting, redirects, and application behavior can affect results.
- TLS certificate verification is enabled by default.

## Author
Sailesh Prasad
