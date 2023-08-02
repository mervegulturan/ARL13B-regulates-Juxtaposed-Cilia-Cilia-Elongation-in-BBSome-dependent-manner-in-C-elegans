## Figure 7

## Length Analysis


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
lenght7<- read_xlsx("figure_6.xlsx", sheet=1)
    colnames(lenght7)
```

 #### Step 3: Organize data

``` Java 
wt_my_comprasion <- list(c("wt","arl-13"),c("wt", "bbs-8"), c("wt", "kap-1"), c("wt", "ift-81"),
                             c("wt", "arl-13; ift-81"),c("wt", "arl-13; bbs-8"), 
                             c("wt", "arl-13; kap-1"))
    
    arl_13_my_comprasion <- list(c("arl-13", "arl-13; bbs-8"), c("arl-13", "arl-13; ift-81"), 
                                 c("arl-13","arl-13; kap-1"))
    
    
    bbs_8_my_comprasion <- list(c("bbs-8", "arl-13; bbs-8"))
    
    kap_1_my_comprasion <- list(c("kap-1","arl-13; kap-1"))
    ift_81_my_comprasion <- list(c("ift-81", "arl-13; ift-81"))
    
    level_order <- c( "wt","arl-13","bbs-8","ift-81","kap-1","arl-13; bbs-8",
                      "arl-13; ift-81","arl-13; kap-1")
    
    lenght7 <- lenght7 %>%
      pivot_longer(
        cols = c("wt","arl-13","bbs-8","ift-81","kap-1","arl-13; bbs-8",
                 "arl-13; ift-81","arl-13; kap-1"),
        names_to = "Names", 
        values_to = "Value",
        values_drop_na = TRUE)
```

#### Step 4: Draw box plot using ggplot() and Wilcoxon paired test

``` Java 
lenght7 %>%
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
                         label.y = 17, hide.ns = F) +
      stat_compare_means(comparisons = arl_13_my_comprasion,label = "p.signif",
                         label.y = 16, hide.ns = F)+
      stat_compare_means(comparisons = bbs_8_my_comprasion,label = "p.signif",
                         label.y = 15, hide.ns = F) +
      stat_compare_means(comparisons = kap_1_my_comprasion,label = "p.signif",
                         label.y = 14, hide.ns = F)+
      stat_compare_means(comparisons = ift_81_my_comprasion,label = "p.signif",
                         label.y = 13, hide.ns = F)
```

## Phenotype Analysis

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
pheno7<- read_xlsx("figure_6.xlsx", sheet=3)
    colnames(pheno7)
```

#### Step 3: Organize data

``` Java 
 level_order <- c("wt","arl-13","bbs-8","ift-81","kap-1","bbs-8;arl-13",
                     "arl-13; ift-81","kap-1;arl-13")
    
    pheno7 <- pheno7 %>%
      pivot_longer(
        cols = c("wt","arl-13","bbs-8","ift-81","kap-1","bbs-8;arl-13",
                 "kap-1;arl-13","arl-13; ift-81"),
        names_to = "Names",
        values_to = "Value",
        values_drop_na = TRUE)
```

#### Step 4: Draw bar plot using ggplot()

``` Java 
    pheno7 %>%
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
  
  fig_<- data.frame("wt"=c(37,0), "arl-13"=c(21,30),
                    row.names = c("Normal", "Misdirection"))
  pairwise_fisher_test(as.matrix(fig_), p.adjust.method = "fdr")
```
