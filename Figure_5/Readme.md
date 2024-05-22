## Figure 5

## Figure 5B-Phenotype Analysis

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
   pheno5<- read_xlsx("figure_5.xlsx", sheet=3)
    colnames(pheno5)
```

 #### Step 3: Organize data

``` Java
pheno5 <- pheno5 %>%
      pivot_longer(
        cols = c("WT","arl-13","mks-5","nphp-4","W07G11.5", "w07g11.5; nphp-4","nphp-4; mks-5"),
        names_to = "Names",
        values_to = "Value",
        values_drop_na = TRUE)
    
    level_order <- c("WT","arl-13","mks-5","nphp-4","W07G11.5", "w07g11.5; nphp-4","nphp-4; mks-5")
```
#### Step 4: Draw bar plot using ggplot()

``` Java 
pheno5 %>%
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

## Figure 5C-Cilia Length Analysis

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
Length5<- read_xlsx("figure_5.xlsx", sheet=1)
    colnames(Length5)
```

 #### Step 3: Organize data

``` Java 
data<- select(Length5, c("wt","arl-13","mks-5","nphp-4","w07g1.5","w07g1.5; nphp-4","mks-s; nphp-4"))
    
    level_order <- c("wt","arl-13", "mks-5","nphp-4", "w07g1.5","w07g1.5; nphp-4","mks-s; nphp-4")
    
    data <- xx %>%
      pivot_longer(
        cols = c("wt","arl-13","mks-5", "nphp-4", "w07g1.5",  "w07g1.5; nphp-4","mks-s; nphp-4"),
        names_to = "Names",
        values_to = "Value",
        values_drop_na = TRUE)
    
    wt_my_comprasion <- list(c("wt","arl-13"),c("wt", "nphp-4"),c("wt", "mks-5"),c("wt","w07g1.5")
                             ,c("wt","w07g1.5; nphp-4"),c("wt","mks-s; nphp-4"))
    
    comp1 <- list(c("nphp-4","w07g1.5; nphp-4"),c("nphp-4","mks-s; nphp-4"))
    com2 <- list(c("w07g11.5","w07g1.5; nphp-4"))
    com3 <- list(c("mks-5","mks-s; nphp-4"))
```

#### Step 4: Draw box plot using ggplot() and Wilcoxon paired test

``` Java
data %>%
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
      labs( y = "Cilia Length (µm)")  +
      ylim(0,18) +
      stat_compare_means(comparisons = wt_my_comprasion,label = "p.signif",
                         label.y = 17, hide.ns = F) +
      stat_compare_means(comparisons = comp1,label = "p.signif",
                         label.y = 16, hide.ns = F)+
      stat_compare_means(comparisons = com2,label = "p.signif",
                         label.y = 15, hide.ns = F) +
      stat_compare_means(comparisons = com3,label = "p.signif",
                         label.y = 14, hide.ns = F)
```

## Figure 5E-Dendride Length Analysis

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
Length5d<- read_xlsx("dendride_lenght.xlsx", sheet=1)
    colnames(Length5d)
```

 #### Step 3: Organize data

``` Java 
    level_order <- c("wt","arl-13","mks-5","nphp-4","rpi-1","rpi-1;nphp-4","mks-5;nphp-4")
    
    
    Length5d <- Length5d %>%
      pivot_longer(
        cols = c("wt","arl-13","rpi-1","nphp-4","mks-5","rpi-1;nphp-4","mks-5;nphp-4"),
        names_to = "Names",
        values_to = "Value",
        values_drop_na = TRUE)
    
    wt_my_comprasion <- list(c("wt","rpi-1"), c("wt", "nphp-4")
                             ,c("wt","rpi-1;nphp-4"),c("wt","mks-5;nphp-4"),
                             c("wt","mks-5"),c("wt", "arl-13"))
    
    com2 <- list(c("rpi-1","rpi-1;nphp-4"))
    com3 <- list(c("nphp-4","rpi-1;nphp-4"), c("nphp-4","mks-5;nphp-4"))
    com4<- list(c("mks-5", "mks-5;nphp-4"))
```

#### Step 4: Draw box plot using ggplot() and Wilcoxon paired test

``` Java
Length5d %>%
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
      labs( y = "Dendride Length (µm)")  +
      ylim(0,40) +
      stat_compare_means(comparisons = wt_my_comprasion,label = "p.signif",
                         label.y = 38, hide.ns = F) +
      stat_compare_means(comparisons = com2,label = "p.signif",
                         label.y = 36, hide.ns = F) +
      stat_compare_means(comparisons = com3,label = "p.signif",
                         label.y = 34, hide.ns = F)+
      stat_compare_means(comparisons = com4,label = "p.signif",
                         label.y = 32, hide.ns = F)
```

## Figure 5F-Misposition Analysis of PHA&PHB

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
 misposition<- read_xlsx("figure_5.xlsx", sheet=4)
 colnames(misposition)
```

 #### Step 3: Organize data

``` Java 
misposition <- misposition %>%
      pivot_longer(
        cols = c("wt","arl-13","w07g1.5","nphp-4","mks-5","w07g1.5; nphp-4","mks-s; nphp-4"),
        names_to = "Names", 
        values_to = "Value",
        values_drop_na = TRUE)
    
    
    level_order <- c("wt","arl-13","w07g1.5","nphp-4","mks-5","w07g1.5; nphp-4","mks-s; nphp-4")
    
    wt_my_comprasion <- list(c("wt","arl-13"),c("wt", "nphp-4"),  c("wt", "w07g1.5"),c("wt", "w07g1.5; nphp-4"),
                             c("wt", "mks-5"), c("wt", "mks-s; nphp-4"))
    
    comparision_2 <- list(c("nphp-4", "w07g1.5; nphp-4"),c("nphp-4", "mks-s; nphp-4"))
    comparision_3 <- list(c("w07g1.5", "w07g1.5; nphp-4"))
    comparision_4 <- list(c("mks-5", "mks-s; nphp-4"))
```

#### Step 4: Draw box plot using ggplot() and Wilcoxon paired test

``` Java
misposition %>%
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
      labs( y = "Cilia Length (µm)")  +
      ylim(0,10) +
      stat_compare_means(comparisons = wt_my_comprasion,label = "p.signif",
                         label.y = 9, hide.ns = F) +
      stat_compare_means(comparisons = comparision_2,label = "p.signif",
                         label.y = 8, hide.ns = F) +
      stat_compare_means(comparisons = comparision_3,label = "p.signif",
                         label.y = 7, hide.ns = F) +
      stat_compare_means(comparisons = comparision_4,label = "p.signif",
                         label.y = 6, hide.ns = F)
```

## Figure S5

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
  Length5<- read_xlsx("figure_S5.xlsx", sheet=1)
  colnames(Length5)
```

 #### Step 3: Organize data

``` Java 
wt_my_comprasion <- list(c("wt","arl-13"), c("wt", "nphp-2"),
                             c("wt", "hdac-6; him-5"),
                             c("wt", "nphp-2;hdac-6"),c("wt",  "arl-13; hdac-6"), 
                             c("wt",  "Arl-13; hdac-6; nphp-2"))
    
    arl_13_my_comprasion <- list(c("arl-13", "arl-13; hdac-6"), 
                                 c("arl-13","Arl-13; hdac-6; nphp-2"))
    
    
    hdac_6_my_comprasion <- list(c("hdac-6; him-5", "arl-13; hdac-6"), c("hdac-6; him-5","Arl-13; hdac-6; nphp-2"))
    
    nphp_2_<-  list( c("nphp-2","Arl-13; hdac-6; nphp-2"), c("nphp-2", "nphp-2;hdac-6"))    
    
    level_order <- c("wt", "arl-13", "nphp-2",
                     "hdac-6; him-5",
                     "nphp-2;hdac-6", "arl-13; hdac-6", "Arl-13; hdac-6; nphp-2")
    
    Length5 <- Length5 %>%
      pivot_longer(
        cols = c("wt", "arl-13", "nphp-2",
                 "hdac-6; him-5",
                 "nphp-2;hdac-6", "arl-13; hdac-6", "Arl-13; hdac-6; nphp-2"),
        names_to = "Names", 
        values_to = "Value",
        values_drop_na = TRUE)
```

#### Step 4: Draw box plot using ggplot() and Wilcoxon paired test

``` Java 
Length5 %>%
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
      labs( y = "Cilia Length (µm)")  +
      ylim(0,18) +
      stat_compare_means(comparisons = wt_my_comprasion,label = "p.signif",
                         label.y = 16, hide.ns = F) +
      stat_compare_means(comparisons = arl_13_my_comprasion,label = "p.signif",
                         label.y = 15, hide.ns = F)+
      stat_compare_means(comparisons = hdac_6_my_comprasion,label = "p.signif",
                         label.y = 14, hide.ns = F) +
      stat_compare_means(comparisons = nphp_2_,label = "p.signif",
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
  pheno5<- read_xlsx("figure_S5.xlsx", sheet=3)
  colnames(pheno5)
```

#### Step 3: Organize data

``` Java 
level_order <- c("WT", "arl-13", "nphp-2",
                     "hdac-6; him-5",
                     "nphp-2; hdac-6" ,"arl-13; hdac-6","arl-13; hdac-6; nphp-2")
    
    
    pheno5 <- pheno5 %>%
      pivot_longer(
        cols = c("WT", "arl-13", "nphp-2",
                 "hdac-6; him-5",
                 "nphp-2; hdac-6","arl-13; hdac-6","arl-13; hdac-6; nphp-2"),
        names_to = "Names",
        values_to = "Value",
        values_drop_na = TRUE)
```

#### Step 4: Draw bar plot using ggplot()

``` Java 
    pheno5 %>%
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
  
  fig_<- data.frame("wt"=c(19,0), "arl-13"=c(23,31),
                    row.names = c("Normal", "Misdirection"))
  pairwise_fisher_test(as.matrix(fig_), p.adjust.method = "fdr")
```

