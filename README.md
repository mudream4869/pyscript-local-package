# Pyscript load local package by prebuild wheel

Pyscript cannot include a local folder straightforward,
and the user has to compile it to be a wheel.

This repository is an example for pyscript to:

1. Compile package to a wheel
2. Include the wheel in pyscript

## Files

* Package files: a folder of python package and a setup.py for building wheel

```
repo
├── myapp8763
│   ├── __init__.py
│   └── funcs.py
└── setup.py
```

* pyscript.json:

```json
{
    "packages": ["./dist/myapp8763-0.0.1-py3-none-any.whl"]
}
```

* index.html:

```html
<script type="py" config="./pyscript.json" terminal>
  import myapp8763.funcs
  myapp8763.funcs.main()
</script>
```

## Clone and Run

```bash
git clone https://github.com/mudream4869/pyscript-local-package.git
cd pyscript-local-package
python3 setup.py build bdist_wheel # generate wheel in dist folder
python3 -m http.server # or other webserver command
```