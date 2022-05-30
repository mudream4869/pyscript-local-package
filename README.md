# Pyscript load local package by prebuild wheel

Pyscript cannot include a local folder straightforward,
and the user has to compile it to be a wheel.

This repository is an example for pyscript to:

1. Compile package to a wheel
2. Include the wheel in pyscript

## Files

* Package files: a folder of python package and a setup.py for building wheel

```
myapp8763
├── myapp8763
│   ├── __init__.py
│   └── funcs.py
└── setup.py
```

* index.html:

```html
<py-env>
- ./myapp8763/dist/myapp8763-0.0.1-py3-none-any.whl
</py-env>
```

## Clone and Run

```bash
git clone https://github.com/mudream4869/pyscript-local-package.git
cd pyscript-local-package
cd myapp8763
python3 setup.py build bdist_wheel # generate wheel in dist folder
cd ..
python3 -m http.server # or other webserver command
```