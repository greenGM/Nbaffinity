# Nbaffinity a machine learning tool to predict nanobody affinity

GitHub Repository for [https://github.com/greenGM/Nbaffinity](https://github.com/greenGM/Nbaffinity)


[![Repository](https://img.shields.io/badge/View%20on-GitHub-blue.svg)](https://github.com/greenGM/Nbaffinity)

## Dependencies:

|     Name      | version            |
| ------------- | ------------------ |
| R             | 4.3.3 or higher    |
| tidyverse     | 2.0.0 or higher    |
| caret         | 6.0-94 or higher   |


## data genereation 

1. the data was generated by using ProtInter：

    [https://github.com/maxibor/protinter](https://github.com/maxibor/protinter)

2. All descriptors needs to be generated and fed into the model in the following order
   HI_ std, HI_ min, HI_ 0.5, HBMS_ count, HBMS_ mean, HBMS_ std, HBMS_ min, HBMS_ max, ASI_ count, ASI_ std,
   ASI_ min, HBSS_ count, HBSS_ std, HBSS_ min, DB_ count, DB_ std, DB_ 0.5, IoInt_ count, IoInt_ std, IoInt_ min,
   IoInt_ 0.25, HBMM_ count, HBMM_ mean, HBMM_ std, HBMM_ min, HBMM_ 0.25, HBMM_ 0.5, HBMM_ 0.75, HBMM_ max,  CPI_ count,
   CPI_ std, CPI_ min, AAI_ count, AAI_ std, AAI_ min.
   
   | Abbreviation | Full name                                      |
   | ------------ | ---------------------------------------------- |
   | HI           | hydrophobic interactions                       |
   | HBMS         | hydrogen bonding main-side chain interactions  |
   | ASI          | aromatic-sulphur interactions                  |
   | HBSS         | hydrogen bonding side-side chain interactions  |
   | DB           | disulphide bridges                             |
   | IoInt        | ionic interactions                             |
   | HBMM         | hydrogen bonding main-main chain interactions  |
   | CPI          | cation-pi interactions                         |
   | ASI          | aromatic-aromatic interactions                 |
   

## How to use this tool:

1. Download all files.

2. Open Rstudio.

3. Enter the following code：
   
     R
   
     load(".RData")
  
     library(tidyverse)
  
     library(caret)
  
     unknown <- read.csv("yourfile.csv",header = F,col.names = name)#Dependent on your data
  
     unknownS <- scale(unknown[,-1])
  
     unknownprediction <- data.frame(name=unknown$name,
                                  preclass=predict(TdataSW.roF1,unknownS),#Give the class of affinity of the candidate nanobody
                                  preprob=predict(TdataSW.roF1,unknownS,type = 'prob' ))#Give the probability of the class
                                  
  write.csv(unknownprediction,'unknownprediction.csv')
  

## Result explanation：
The result will be returned as a csv file.

   name--the name of the candidate nanobody.

  preclass--predicted class: Y represents MIC < 2000 and N represents MIC ≥ 2000.

   preprob.N preprob.--the probability of the class 


