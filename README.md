
# ifxss — Improved XSS Reflection Scanner (kxss but better)

**ifxss** is a fast XSS reflection detection tool that works similar to **kxss by tomnomnom**,
but with several important improvements that make it more practical for real‑world testing.

##  Why ifxss is Better than kxss

* **Supports custom headers (`-H`)**
  → Useful for passing cookies, tokens, API keys, JWTs, or custom headers.

* **Can scan authenticated endpoints**
  → Unlike kxss, you can hit pages behind login, dashboards, admin areas, etc.

* **Readable, structured output **
  → Shows parameter, reflected characters, risk level, total findings, and tested URLs.

* **Works directly with stdin pipelines**
  → Perfect with katana, gau, wayback, hakrawler, zap, etc.

##  Example Usage

```
cat urls.txt | python3 ifxss.py
```

With headers:

```
cat urls.txt | python3 ifxss.py -H "Cookie: session=abc123"
```

Pipeline:

```
cat katana.txt | zap | python3 ifxss.py
```

##  Example Output

```
────────────────────────────────────────────────────────────────────────────────
Reflected Payloads
────────────────────────────────────────────────────────────────────────────────
[1] Risk   : HIGH
     Param  : search
     Chars  : < > " ' ${ ` ;
     URL    : https://0af9007a04f318f8822e932600ba002d.web-security-academy.net/?search=FUZZ
────────────────────────────────────────────────────────────────────────────────
Total findings: 1
URLs tested: 2
```

##  What It Does

ifxss scans each URL for reflected characters using a precise per‑character method.

It tests:

```
< > " ' ${ ` ;
```

Each character is injected with a unique token → reflected → categorized → reported.

The output only shows **unfiltered** characters, making it immediately clear whether an endpoint is vulnerable.

## 🛠 Installation

```
chmod +x ifxss.py
python3 ifxss.py
```

