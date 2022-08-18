# Developer Notebook
## **MLPack Notes**
### **Errors + Solutions**
### Error in mlpack_sg_lasso in preprocess: std::out_of_range
Error: terminate called after throwing an instance of 'std::out_of_range'

Cause: response file is not correctly formatted

Solution: response matrix uses tab as delimiter, and every species/line needs a number (-1, 1, or 0)
### Error in mlpack_sg_lasso in preprocess: Segmentation fault
Error: segmentation fault

Cause: error can be cause by multiple different reasons, one possibility is that FAFSA file is not "unpacked" (i.e. there are carriage returns within sequences)

Solution: unpack FASTA file by removing any new line characters within the sequences- each sequence should be on one line only
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

### Running mlpack_sg_lasso_leastr
#### To run mlpack_sg_lasso or mlpack_overlapping_sg_lasso_leastr, replace "mpack_sg_lasso_leastr" with desired method
Outline (runs from directory that contains mlpack):

*All files used in command (except for xml file) have already been created by preprocessing*

```
mlpack-3.2.2/build/bin/mlpack_sg_lasso_leastr -v -f feature-file.txt -n group_indices-file.txt -r response-file.txt -w xml-file-to-write.xml
```

Example:

```
mlpack-3.2.2/build/bin/mlpack_sg_lasso_leastr -v -f retsat-fixed-input/feature_retsat-fixed-input.txt -n retsat-fixed-input/group_indices_retsat-fixed-input.txt -r retsat-fixed-input/response_retsat-fixed-input.txt
 -w retsat_fixed_out.xml
 ```
