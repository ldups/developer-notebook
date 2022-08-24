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

Incorrect FAFSA example:

```
>species name
ATCG\n
ATTC\n
ATGC\n
```

Correct FAFSA example:

```
>species name
ATCGATTCATGC
```

### **Scripts**
#### *All commands run in Unix. On Windows, these commands work in WSL 2.*
### Preprocess
Outline (runs from directory with matrix and path files):

```
../mlpack-3.2.2/build/bin/preprocess response-file.txt path-file.txt base-name-for-output-dir
```

Example:

```
../mlpack-3.2.2/build/bin/preprocess retsatResponse.txt retsatPaths.txt retsat_input/
```

The preprocess command will create 6 text files in a directory with the given base name. These files will be used when running further commands.

The files produced should have base names of:

```
feature_mapping
field
missing_seqs
feature
group_indices
response
```

### Running mlpack_sg_lasso_leastr
#### To run mlpack_sg_lasso or mlpack_overlapping_sg_lasso_leastr, replace "mpack_sg_lasso_leastr" with desired method
*mlpack_overlapping_sg_lasso_leastr should only be used when overlapping sequences are involved*

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
 
 These commands will produce an xml file with the name given.
 
 ### Processing results
These commands process the xml file (produced in the last step) by using the feature mapping file (produced by preprocessing). The final product will be a table with the position or gene and a score.
 
 Outline:
 
 ```
grep -P "<item>.*</item>" output-file.xml | sed -re "s/.*<item>(.*)<\/item>.*/\1/" > temporary-file.txt
paste <(sed -e "1d" feature-mapping-input.txt) temporary-file.txt | grep -v "0.00000000000000000e+00" > processed-output.txt
```

Example of output:

```
1       RETSAT.origin.seq.unpacked_186_I        -7.70832979778843241e-03
2       RETSAT.origin.seq.unpacked_186_L        4.04189659532450726e-03
3       RETSAT.origin.seq.unpacked_186_V        6.88962798969870401e-04
4       RETSAT.origin.seq.unpacked_187_S        6.88962798969870401e-04
5       RETSAT.origin.seq.unpacked_187_T        -7.70832979778843241e-03
6       RETSAT.origin.seq.unpacked_187_V        1.13480579121774863e-02
```

The most positive values are most associated with the ingroup species (given a 1 in the response matrix). The most negative values are most associated with the outgroup species (given a -1 in the response matrix).
