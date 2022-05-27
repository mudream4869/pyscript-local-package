# Pyscript load local package by prebuild wheel

```bash
cd myapp8763
python3 setup.py build bdist_wheel
cd ..
python3 -m http.server
```