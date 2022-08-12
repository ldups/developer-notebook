# Developer Notebook
## **MLPack Notes**
### **Errors + Solutions**
### Error in mlpack_sg_lasso in preprocess: std::out_of_range
Error: terminate called after throwing an instance of 'std::out_of_range'

Solution: response matrix uses tab + 1 space as delimiter, and every species/line needs a number (-1, 1, or 0)
### Error in mlpack_sg_lasso in preprocess: Segmentation fault

### **Scripts**
### Preprocess
Outline (runs from directory with matrix and path files):

```
../mlpack-3.2.2/build/bin/preprocess response-file.txt path-file.txt base-name-for-output-dir
```

Example:
```
../mlpack-3.2.2/build/bin/preprocess retsatResponse.txt retsatPaths.txt retsat_input/
```
