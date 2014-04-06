Tidy data
========================================================

- colonne NOTE: remplacer *absent* par NA
- colonne NOTE: remplacer la virgule par le point décimal


```r
source("../private.R")
d <- load()
```

```
## Loading required package: RCurl
## Loading required package: bitops
```

```r
names(d)
```

```
##  [1] "NUMERO"    "ECOLE"     "PROMO"     "SEXE"      "ANNEE"    
##  [6] "QUEST.1"   "QUEST.2"   "QUEST.3"   "QUEST.4"   "QUEST.5"  
## [11] "QUEST.6"   "QUEST.7"   "QUEST.8"   "QUEST.9"   "QUEST.10" 
## [16] "QUEST.11"  "QUEST.12"  "QUEST.13"  "QUEST.14"  "QUEST.15" 
## [21] "QUEST.16"  "QUEST.17"  "QUEST.18"  "QUEST.19"  "QUEST.20" 
## [26] "QUEST.21"  "QUEST.22"  "QUEST.23"  "QUEST.24"  "QUEST.25" 
## [31] "QUEST.26"  "RANG"      "M.PLACE"   "AFFINITES" "HABITUDE" 
## [36] "PAS.BRUIT" "PRATIQUE"  "PLACE.RES" "CONCENTR"  "DECROCHE" 
## [41] "REDOUBLA"  "NOTE"
```

```r
summary(d)
```

```
##      NUMERO           ECOLE          PROMO    SEXE       ANNEE     
##  Min.   :  1.0   AUX PUER:39   2010/2014:24   F:95   Min.   :1961  
##  1st Qu.: 30.2   ETCADRE :16   2012/2014:22   M:23   1st Qu.:1979  
##  Median : 59.5   ET IADE :37   2013     :39          Median :1984  
##  Mean   : 59.5   ET IADE : 2   2013/2014:16          Mean   :1983  
##  3rd Qu.: 88.8   MAIEU   :24   2013/2015:17          3rd Qu.:1990  
##  Max.   :118.0                                       Max.   :1994  
##                                                                    
##     QUEST.1        QUEST.2        QUEST.3        QUEST.4    
##  Min.   :3.00   Min.   :2.00   Min.   :1.00   Min.   :1.00  
##  1st Qu.:6.00   1st Qu.:5.00   1st Qu.:4.25   1st Qu.:4.00  
##  Median :7.00   Median :6.00   Median :5.00   Median :5.00  
##  Mean   :6.53   Mean   :5.66   Mean   :5.26   Mean   :4.58  
##  3rd Qu.:7.00   3rd Qu.:7.00   3rd Qu.:6.00   3rd Qu.:5.00  
##  Max.   :7.00   Max.   :7.00   Max.   :7.00   Max.   :7.00  
##                                                             
##     QUEST.5        QUEST.6        QUEST.7        QUEST.8    
##  Min.   :1.00   Min.   :1.00   Min.   :1.00   Min.   :1.00  
##  1st Qu.:4.00   1st Qu.:4.00   1st Qu.:4.00   1st Qu.:5.00  
##  Median :5.00   Median :5.00   Median :6.00   Median :6.00  
##  Mean   :4.58   Mean   :4.61   Mean   :5.43   Mean   :5.48  
##  3rd Qu.:6.00   3rd Qu.:6.00   3rd Qu.:7.00   3rd Qu.:6.00  
##  Max.   :7.00   Max.   :7.00   Max.   :7.00   Max.   :7.00  
##                                                             
##     QUEST.9        QUEST.10       QUEST.11      QUEST.12       QUEST.13   
##  Min.   :1.00   Min.   :3.00   Min.   :1.0   Min.   :1.00   Min.   :3.00  
##  1st Qu.:4.00   1st Qu.:6.00   1st Qu.:2.0   1st Qu.:3.00   1st Qu.:5.00  
##  Median :5.00   Median :6.00   Median :4.0   Median :4.00   Median :6.00  
##  Mean   :4.82   Mean   :6.18   Mean   :3.9   Mean   :4.17   Mean   :6.06  
##  3rd Qu.:6.00   3rd Qu.:7.00   3rd Qu.:5.0   3rd Qu.:5.00   3rd Qu.:7.00  
##  Max.   :7.00   Max.   :7.00   Max.   :7.0   Max.   :7.00   Max.   :7.00  
##                                                                           
##     QUEST.14       QUEST.15       QUEST.16       QUEST.17   
##  Min.   :1.00   Min.   :1.00   Min.   :1.00   Min.   :1.00  
##  1st Qu.:4.00   1st Qu.:5.00   1st Qu.:4.00   1st Qu.:4.00  
##  Median :5.00   Median :6.00   Median :5.00   Median :5.00  
##  Mean   :4.82   Mean   :5.75   Mean   :4.61   Mean   :4.75  
##  3rd Qu.:6.00   3rd Qu.:7.00   3rd Qu.:5.00   3rd Qu.:6.00  
##  Max.   :7.00   Max.   :7.00   Max.   :7.00   Max.   :7.00  
##                                                             
##     QUEST.18       QUEST.19       QUEST.20       QUEST.21   
##  Min.   :2.00   Min.   :1.00   Min.   :1.00   Min.   :1.00  
##  1st Qu.:5.00   1st Qu.:5.00   1st Qu.:4.00   1st Qu.:3.00  
##  Median :6.00   Median :6.00   Median :5.00   Median :4.00  
##  Mean   :5.46   Mean   :5.51   Mean   :5.05   Mean   :3.89  
##  3rd Qu.:7.00   3rd Qu.:6.00   3rd Qu.:6.00   3rd Qu.:5.00  
##  Max.   :7.00   Max.   :7.00   Max.   :7.00   Max.   :7.00  
##  NA's   :1      NA's   :1      NA's   :1                    
##     QUEST.22       QUEST.23       QUEST.24       QUEST.25   
##  Min.   :1.00   Min.   :1.00   Min.   :1.00   Min.   :1.00  
##  1st Qu.:4.00   1st Qu.:5.00   1st Qu.:4.00   1st Qu.:3.00  
##  Median :5.00   Median :6.00   Median :5.00   Median :4.00  
##  Mean   :4.69   Mean   :5.47   Mean   :4.75   Mean   :4.14  
##  3rd Qu.:6.00   3rd Qu.:6.00   3rd Qu.:6.00   3rd Qu.:6.00  
##  Max.   :7.00   Max.   :7.00   Max.   :7.00   Max.   :7.00  
##                                                             
##     QUEST.26         RANG      M.PLACE AFFINITES HABITUDE PAS.BRUIT
##  Min.   :2.00   Min.   :1.00    : 2     :89       :90      :111    
##  1st Qu.:5.00   1st Qu.:2.00   N:29    O:29      O:28     O:  7    
##  Median :5.00   Median :4.00   O:87                                
##  Mean   :5.42   Mean   :4.08                                       
##  3rd Qu.:6.00   3rd Qu.:5.00                                       
##  Max.   :7.00   Max.   :9.00                                       
##                                                                    
##  PRATIQUE PLACE.RES CONCENTR DECROCHE REDOUBLA            NOTE      
##   :93      :103      :109     :115    Mode:logical   Min.   : 4.42  
##  O:25     O: 15     O:  9    O:  3    NA's:118       1st Qu.: 9.25  
##                                                      Median :12.25  
##                                                      Mean   :11.62  
##                                                      3rd Qu.:14.50  
##                                                      Max.   :16.50  
##                                                      NA's   :57
```

```r
str(d)
```

```
## 'data.frame':	118 obs. of  42 variables:
##  $ NUMERO   : int  1 2 3 4 5 6 7 8 9 10 ...
##  $ ECOLE    : Factor w/ 5 levels "AUX PUER","ETCADRE",..: 5 5 5 5 5 5 5 5 5 5 ...
##  $ PROMO    : Factor w/ 5 levels "2010/2014","2012/2014",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ SEXE     : Factor w/ 2 levels "F","M": 1 1 1 1 1 1 1 1 1 1 ...
##  $ ANNEE    : int  1990 1990 1972 1990 1989 1990 1990 1990 1991 1990 ...
##  $ QUEST.1  : int  7 7 7 7 7 6 7 7 5 6 ...
##  $ QUEST.2  : int  6 6 6 6 4 5 4 5 6 6 ...
##  $ QUEST.3  : int  7 6 6 6 6 4 4 4 3 5 ...
##  $ QUEST.4  : int  5 4 7 5 1 3 2 5 3 4 ...
##  $ QUEST.5  : int  6 4 5 4 4 3 4 3 4 4 ...
##  $ QUEST.6  : int  7 7 2 5 4 4 4 3 6 4 ...
##  $ QUEST.7  : int  7 7 3 6 7 6 5 6 4 7 ...
##  $ QUEST.8  : int  7 7 7 6 7 5 6 3 5 4 ...
##  $ QUEST.9  : int  6 6 1 3 7 3 6 7 5 3 ...
##  $ QUEST.10 : int  7 6 7 6 6 5 5 3 4 5 ...
##  $ QUEST.11 : int  4 1 1 3 4 2 5 1 3 1 ...
##  $ QUEST.12 : int  5 4 5 2 1 3 2 2 4 4 ...
##  $ QUEST.13 : int  7 7 7 7 3 5 5 7 3 6 ...
##  $ QUEST.14 : int  7 5 4 4 3 4 4 3 3 4 ...
##  $ QUEST.15 : int  5 7 6 5 4 5 4 5 5 5 ...
##  $ QUEST.16 : int  4 5 6 4 1 3 2 3 2 4 ...
##  $ QUEST.17 : int  5 5 5 4 3 3 2 3 4 4 ...
##  $ QUEST.18 : int  7 5 7 5 3 5 4 4 5 4 ...
##  $ QUEST.19 : int  6 7 7 6 5 5 6 5 6 5 ...
##  $ QUEST.20 : int  6 4 6 3 6 4 5 7 4 4 ...
##  $ QUEST.21 : int  7 4 1 2 2 3 3 4 6 4 ...
##  $ QUEST.22 : int  7 5 4 3 2 3 3 3 4 3 ...
##  $ QUEST.23 : int  7 6 7 4 4 4 7 6 6 3 ...
##  $ QUEST.24 : int  5 2 7 4 2 3 3 3 5 4 ...
##  $ QUEST.25 : int  6 2 2 6 1 2 5 5 2 3 ...
##  $ QUEST.26 : int  6 6 7 6 6 5 4 5 5 5 ...
##  $ RANG     : int  1 1 2 2 2 2 3 3 3 3 ...
##  $ M.PLACE  : Factor w/ 3 levels "","N","O": 3 3 3 3 3 3 3 3 3 3 ...
##  $ AFFINITES: Factor w/ 2 levels "","O": 1 1 1 2 2 1 2 2 2 1 ...
##  $ HABITUDE : Factor w/ 2 levels "","O": 1 1 2 1 1 1 1 1 2 2 ...
##  $ PAS.BRUIT: Factor w/ 2 levels "","O": 1 1 1 1 1 1 1 1 1 1 ...
##  $ PRATIQUE : Factor w/ 2 levels "","O": 1 2 1 1 1 1 1 1 1 1 ...
##  $ PLACE.RES: Factor w/ 2 levels "","O": 1 1 1 1 1 1 1 1 1 1 ...
##  $ CONCENTR : Factor w/ 2 levels "","O": 2 1 1 1 1 1 2 1 1 1 ...
##  $ DECROCHE : Factor w/ 2 levels "","O": 1 1 1 1 1 1 1 1 1 1 ...
##  $ REDOUBLA : logi  NA NA NA NA NA NA ...
##  $ NOTE     : num  11.83 13.54 6.88 9.25 9.33 ...
```

```r

d$NOTE <- as.numeric(d$NOTE)
```


Etude de la note
----------------

```r
mean(d$NOTE, na.rm = TRUE)
```

```
## [1] 11.62
```

```r
sd(d$NOTE, na.rm = TRUE)
```

```
## [1] 3.193
```

```r
summary(d$NOTE)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
##    4.42    9.25   12.20   11.60   14.50   16.50      57
```

```r
tapply(d$NOTE, d$RANG, length)
```

```
##  1  2  3  4  5  6  7  8  9 
## 14 17 21 19 21  5 11  8  2
```

```r
tapply(d$NOTE, d$RANG, mean, na.rm = TRUE)
```

```
##     1     2     3     4     5     6     7     8     9 
## 13.87 10.96 10.62 10.99 10.62 12.75 13.81 11.78 12.00
```

```r
hist(d$NOTE, ylab = "Fréquence", xlab = "Notes", main = "Histogramme des notes", 
    col = "gray90")
```

![plot of chunk note](figure/note1.png) 

```r
boxplot(d$NOTE ~ d$RANG, ylab = "Note", xlab = "Rang de l'étudiant", main = "Répartition des notes en fonction du rang", 
    col = "yellow")
```

![plot of chunk note](figure/note2.png) 

en fonction du sexe
-------------------

```r
tapply(d$NOTE, d$SEXE, mean, na.rm = TRUE)
```

```
##      F      M 
## 11.813  7.877
```

```r
boxplot(d$NOTE ~ d$SEXE, ylab = "Note", main = "Répartition des notes en fonction du sexe", 
    col = "pink")
```

![plot of chunk sexe](figure/sexe.png) 


Résultats selon la filière
==========================

Il faut corriger ECOLE car un niveau est mal orthographié:

```r
summary(ECOLE)
```

```
## Error: objet 'ECOLE' introuvable
```

```r
ECOLE[as.character(ECOLE) == "ET IADE "] <- "ET IADE"
```

```
## Error: objet 'ECOLE' introuvable
```

```r
ECOLE <- factor(ECOLE)
```

```
## Error: objet 'ECOLE' introuvable
```

```r
summary(ECOLE)
```

```
## Error: objet 'ECOLE' introuvable
```

```r
barplot(ECOLE)
```

```
## Error: objet 'ECOLE' introuvable
```


Motivation selon la filière
----------------------------


```r
tapply(motivation, ECOLE, mean, na.rm = TRUE)
```

```
## Error: objet 'ECOLE' introuvable
```

```r
boxplot(motivation ~ ECOLE)
```

```
## Error: objet 'motivation' introuvable
```




