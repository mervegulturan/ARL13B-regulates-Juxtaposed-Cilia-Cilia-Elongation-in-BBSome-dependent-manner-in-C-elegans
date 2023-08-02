## Figure 3

##  Bar plot for presenting phenotypic difference in ASE and ASI cilia 

![Rplot01](https://github.com/mervegulturan/BBSome-regulates-ARL13B-dependent-joint-elongation-of-two-distinct-cilia-in-C.-elegans/assets/96948625/da2de1a0-1c1f-49fb-b7cf-a27e4f27e23b)

#### Step 1: Upload required packages

``` Java  
library(dplyr)
library(ggplot2)
library(ggpubr)
library(tidyr)
library(colorspace)
library(forcats)
library(readxl)
```


#### Step 2: Read excel file and check column names

``` Java 
phenotype<- read_xlsx("ASE and ASI.xlsx", sheet = 2)

phenotype[is.na(phenotype)] <- 0  

colnames(phenotype)
```

#### Step 3: Organize data

``` Java 
  fig_3 <- fig_3 %>%
    pivot_longer(
      cols = c("WT","arl-13"),
      names_to = "Names",
      values_to = "Value",
      values_drop_na = TRUE)
  
  level_order <- c("WT","arl-13")
```  

#### Step 4: Draw bar plot using ggplot()

``` Java 
  fig_3 %>%
    ggplot(aes(x=factor(Names,level = level_order),
               y=Value, fill= Phenotype)) +
    geom_bar(aes(color = Phenotype,
                 fill = after_scale(desaturate(lighten(color, 0.6), .3))),
             size = 0.5, stat='identity', na.rm = TRUE) +
    scale_color_manual(values=c("#47a6de","#0f599c")) +
    theme(axis.line = element_line(colour = "Black"),
          panel.grid.major = element_line(colour = "White"),
          panel.grid.minor = element_line(colour = "White"),
          panel.border = element_blank(),
          panel.background = element_blank())
```

#### Step 5: Apply Fisher's exact test as statistical analysis

``` Java 
  library(rstatix)
  
  fig_<- data.frame("wt"=c(34,5), "arl-13"=c(30,24),
                    row.names = c("Normal", "Misdirection"))
  pairwise_fisher_test(as.matrix(fig_), p.adjust.method = "fdr")
```
