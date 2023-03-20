## Figure 4

## Lenght Analysis

###  Box plot for presenting cilia lenght of IFT-74::GFP


#### Step 1: Upload required packages

``` Java  
library(dplyr)
library(ggplot2)
library(ggpubr)
library(tidyr)
library(ggplot2)
library(colorspace)
library(forcats)
library(readxl)
```

#### Step 2: Read excel file and check column names

``` Java 
  leng4a<- read_xlsx("figure_4.xlsx", sheet=4)
  colnames(leng4a)
```
 
 #### Step 3: Organize data

``` Java 
leng4a <- leng4a %>%
    pivot_longer(
      cols = c("wt","arl-13", "cdkl-1","ift-139","arl-13; cdkl-1"
               ,"arl-13; ift-139",),
      names_to = "Names",
      values_to = "Value",
      values_drop_na = TRUE
    )
  
  wt_my_comprasion <- list(c("wt","arl-13"),
                           c("wt", "ift-139"), c("wt", "cdkl-1"),
                           c("wt", "arl-13; ift-139"), c("wt", "arl-13; cdkl-1"))
  
  arl_13_my_comprasion <- list(c("arl-13", "arl-13; ift-139"),
                               c("arl-13", "arl-13; cdkl-1"))
  
  other_my_comprasion2 <- list(c("ift-139","arl-13; ift-139"))
  other_my_comprasion3 <- list(c("cdkl-1","arl-13; cdkl-1"))
  
  level_order <- c("wt","arl-13", "cdkl-1","ift-139", 
                   "arl-13; cdkl-1", "arl-13; ift-139")
```

#### Step 4: Draw box plot using ggplot() and Wilcoxon paired test

``` Java 
leng4a%>%
    ggplot(aes(x=fct_relevel(Names,level = level_order ),
               y=Value, fill= Names))+
    geom_boxplot(aes(color = Names,
                     fill = after_scale(desaturate(lighten(color, 0.4), .3))),
                 size = 1,width=0.8)  +
    geom_jitter(width=0.1, alpha=0.5) +
    theme(axis.line = element_line(colour = "Black"),
          panel.grid.major = element_line(colour = "White"),
          panel.grid.minor = element_line(colour = "White"),
          panel.border = element_blank(),
          panel.background = element_blank(),
          axis.ticks.x=element_blank(),
          axis.text.x=element_text(angle=-270)) +
    labs( y = "Cilia Lenght (µm)")+
    ylim(0,18)+
    stat_compare_means(comparisons = wt_my_comprasion,label = "p.signif" ,
                       label.y = 17, hide.ns = F) +
    stat_compare_means(comparisons = arl_13_my_comprasion,label = "p.signif" ,
                       label.y = 16, hide.ns = F) +
    stat_compare_means(comparisons = other_my_comprasion2,label = "p.signif" ,
                       label.y = 14, hide.ns = F)+
    stat_compare_means(comparisons = other_my_comprasion3,label = "p.signif" ,
                       label.y = 13, hide.ns = F)
```

###  Box plot for presenting cilia lenght of SRB-6::GFP

#### Step 1: Upload required packages

``` Java  
library(dplyr)
library(ggplot2)
library(ggpubr)
library(tidyr)
library(ggplot2)
library(colorspace)
library(forcats)
library(readxl)
```

#### Step 2: Read excel file and check column names

``` Java 
lenght4<- read_xlsx("figure_4.xlsx", sheet=1)
colnames(lenght4)
```

 #### Step 3: Organize data

``` Java 
  lenght4_additional<- select (lenght4, c("wt","arl-13","nekl-4","arl-13; nekl-4" ))

  wt_my_comprasion <- list(c("wt","arl-13"), c("wt", "nekl-4"),
                           c("wt",  "arl-13; nekl-4"))
  
  arl_13_my_comprasion <- list( c("arl-13", "arl-13; nekl-4"))
 
  nekl_4_comp <- list(c("nekl-4","arl-13; nekl-4"))
  
  
  level_order <- c("wt", "arl-13", "nekl-4","arl-13; nekl-4")
  
  lenght4_additional <- lenght4_additional %>%
    pivot_longer(
      cols = c("wt", "arl-13", "nekl-4","arl-13; nekl-4"),
      names_to = "Names", 
      values_to = "Value",
      values_drop_na = TRUE)
```

#### Step 4: Draw box plot using ggplot() and Wilcoxon paired test

``` Java 
 lenght4_additional %>%
    ggplot(aes(x=factor(Names,level = level_order), 
               y=Value, fill= Names))+
    geom_boxplot(aes(color = Names,
                     fill = after_scale(desaturate(lighten(color, 0.4), .3))),
                 size = 1,width=0.8)  +
    geom_jitter(width=0.1, alpha=0.5) +
    theme(axis.line = element_line(colour = "Black"),
          panel.grid.major = element_line(colour = "White"),
          panel.grid.minor = element_line(colour = "White"),
          panel.border = element_blank(),
          panel.background = element_blank(),
          axis.ticks.x=element_blank(),
          axis.text.x=element_text(angle=-270)) +
    labs( y = "Cilia Lenght (µm)")  +
    ylim(0,18) +
    stat_compare_means(comparisons = wt_my_comprasion,label = "p.signif",
                       label.y = 16, hide.ns = F) +
    stat_compare_means(comparisons = arl_13_my_comprasion,label = "p.signif",
                       label.y = 15, hide.ns = F)+
    stat_compare_means(comparisons = nekl_4_comp,label = "p.signif",
                       label.y = 12, hide.ns = F)
```

## Phenotype Analysis

### SRB-6::GFP

#### Step 1: Upload required packages

``` Java  
library(dplyr)
library(ggplot2)
library(ggpubr)
library(tidyr)
library(ggplot2)
library(colorspace)
library(forcats)
library(readxl)
```

#### Step 2: Read excel file and check column names

``` Java 
 pheno4<- read_xlsx("figure_4.xlsx", sheet=3)
  colnames(pheno4)
```

#### Step 3: Organize data

``` Java 
pheno4_additional<- select (pheno4, c("WT","arl-13","nekl-4","arl-13; nekl-4", "Phenotype" ))
  
level_order <- c("WT", "arl-13", "nekl-4", "arl-13; nekl-4")
    
  pheno4_additional <- pheno4_additional %>%
      pivot_longer(
        cols = c("WT", "arl-13", "nekl-4", "arl-13; nekl-4"),
        names_to = "Names",
        values_to = "Value",
        values_drop_na = TRUE)
```

#### Step 4: Draw bar plot using ggplot()

``` Java 
    pheno4_additional %>%
      ggplot(aes(x=fct_relevel(Names,level = level_order),
                 y=Value, fill= Phenotype)) +
      geom_bar(aes(color = Phenotype,
                   fill = after_scale(desaturate(lighten(color, 0.3), .3))),
               size = 0.5, stat='identity', na.rm = TRUE) +
      scale_color_manual(values=c("#cdf4c8","#9de0ab")) +
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








