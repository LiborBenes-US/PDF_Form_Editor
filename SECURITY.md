## Security Note: CVE-2024-4367

This tool uses PDF.js version **3.4.120**, which is affected by
[CVE-2024-4367](https://github.com/advisories/GHSA-wgrm-67xf-hhpq) — a
high-severity vulnerability that allows a malicious PDF to execute
arbitrary JavaScript in the browser context where it is opened.

**The vulnerability is mitigated in this file.** The `getDocument` call
explicitly sets `isEvalSupported: false`, which disables the vulnerable
font-rendering code path, as recommended by the official security
advisory.

The `eval` usage still physically exists inside the bundled `pdfjs.js`,
but with `isEvalSupported: false` that code path is never reached.

**If you fork or modify this file, do not remove that option.** Removing
it will re-enable the vulnerability.

A permanent fix requires upgrading to PDF.js **4.2.67 or later**, where
the `eval` usage was removed entirely.

Running this file as provided locally in your browser is safe.
The mitigation is applied, and the vulnerable code path is unreachable.
Do not modify the file in ways that remove the mitigation.
