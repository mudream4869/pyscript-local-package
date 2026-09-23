# Pyscript load local package

Examples of loading a local Python package in [PyScript](https://pyscript.net/) (2026.7.3):

1. **`files` (recommended)**: fetch `.py` files onto the in-browser filesystem, no build step
2. **Wheel**: build the package into a wheel and install it via `packages`

Both examples import the same package:

```
repo
├── myapp8763
│   ├── __init__.py
│   └── funcs.py
└── pyproject.toml   # only needed for the wheel example
```

## 1. `files` (index.html)

* pyscript.json:

```json
{
    "files": {
        "./myapp8763/__init__.py": "./myapp8763/",
        "./myapp8763/funcs.py": "./myapp8763/"
    }
}
```

Each source URL is fetched into the destination directory (a destination ending with `/` keeps the source filename).
Files land in the working directory, which is on `sys.path`, so the package is importable directly.
Every module of the package must be listed.

* index.html:

```html
<script type="py" config="./pyscript.json" terminal>
  import myapp8763.funcs
  myapp8763.funcs.main()
</script>
```

Tip: for a larger package, zip it and extract it in one line: `"./myapp8763.zip": "./*"`.

## 2. Wheel (wheel.html)

* pyscript-wheel.json:

```json
{
    "packages": ["./dist/myapp8763-0.0.1-py3-none-any.whl"]
}
```

* wheel.html: same as index.html, but uses `config="./pyscript-wheel.json"`.

Rebuild the wheel after changing the package source:

```bash
pip install build
python3 -m build --wheel # generate wheel in dist folder
```

## Clone and Run

```bash
git clone https://github.com/mudream4869/pyscript-local-package.git
cd pyscript-local-package
python3 -m http.server # or other webserver command
```

Open `http://localhost:8000/` (files) or `http://localhost:8000/wheel.html` (wheel).
