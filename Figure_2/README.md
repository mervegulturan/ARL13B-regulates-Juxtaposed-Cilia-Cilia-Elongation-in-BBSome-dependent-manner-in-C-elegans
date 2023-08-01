## Figure 2

##  Bar plot for presenting phenotypic differeances in single mutants


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
fig_2_p<- read_xlsx("figure_2.xlsx", sheet = 3)
  
  colnames(fig_2_p)
```

#### Step 3: Organize data

``` Java 
fig_2p<- select(fig_2_p, c("WT", "bbs-5", "bbs-7","hdac-6; him-5",
                               "mksr-1","mks-2", "mks-5","mks-6","dyf-5", "nphp-2","nphp-4","kap-1", "klp-13",
                               "W07G11.5", "nekl-4","elmd-1", "cdkl-1","cep-104", "ccep-290",
                               "ttll-4", "ttll-11","wdr-31", "wdr-54","arl-13",
                               "Phenotype"))
    
    
    fig_2p <- fig_2p %>%
      pivot_longer(
        cols = c("WT", "bbs-5", "bbs-7","hdac-6; him-5",
                 "mksr-1","mks-2", "mks-5","mks-6","dyf-5", "nphp-2","nphp-4","kap-1", "klp-13",
                 "W07G11.5", "nekl-4","elmd-1", "cdkl-1","cep-104", "ccep-290",
                 "ttll-4", "ttll-11","wdr-31", "wdr-54","arl-13"),
        names_to = "Names",
        values_to = "Value",
        values_drop_na = TRUE)
    
    level_order <- c("WT", "bbs-5", "bbs-7","hdac-6; him-5",
                     "mksr-1","mks-2", "mks-5","mks-6","dyf-5", "nphp-2","nphp-4","kap-1", "klp-13",
                     "W07G11.5", "nekl-4","elmd-1", "cdkl-1","cep-104", "ccep-290",
                     "ttll-4", "ttll-11","wdr-31", "wdr-54","arl-13")
```

#### Step 4: Draw bar plot using ggplot()

``` Java 
fig_2p %>%
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
    
    fig_<- data.frame("wt"=c(20,0), "arl-13"=c(51,3),
                      row.names = c("Normal", "Misdirection"))
    pairwise_fisher_test(as.matrix(fig_), p.adjust.method = "fdr")
```

##  Box plot for presenting cilia lenght results in single mutants

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
  fig_2_l<- read_xlsx("figure_2.xlsx", sheet = 1)
  colnames(fig_2_l)
```

#### Step 3: Organize data

``` Java
wt_my_comprasion <- list(c("wt", "arl-13"), c("wt", "nekl-4"),
                             c("wt", "ccep-290"), c("wt","cdkl-1"),c("wt", "dyf-5"), c("wt", "hdac-6; him-5"),
                             c("wt", "mks-5"), c("wt","nphp-4"),c("wt", "nphp-2"), c("wt", "kap-1"),
                             c("wt", "klp-13"), c("wt","mksr-1"),c("wt", "cep-104"), c("wt", "ttll-11"),
                             c("wt", "bbs-5"),   c("wt","bbs-7"),c("wt", "ttll-4"), c("wt", "w07g11.5"), c("wt", "wdr-31"),
                             c("wt", "wdr-54"), c("wt", "mks-2"), c("wt", "elmd-1"), c("wt", "mks-6"))  
    
    level_order <- c("wt", "bbs-5", "bbs-7","hdac-6; him-5",
                     "mksr-1","mks-2", "mks-5","mks-6","dyf-5","nphp-2","nphp-4","kap-1", "klp-13",
                     "w07g11.5", "nekl-4","elmd-1", "cdkl-1","cep-104","ccep-290",
                     "ttll-4", "ttll-11", "wdr-31", "wdr-54","arl-13")
                     
      fig_2_l <- fig_2_l %>%
      pivot_longer(
        cols = c("wt", "bbs-5", "bbs-7","hdac-6; him-5",
                 "mksr-1","mks-2", "mks-5","mks-6","dyf-5","nphp-2","nphp-4","kap-1", "klp-13",
                 "w07g11.5", "nekl-4","elmd-1", "cdkl-1","cep-104","ccep-290",
                 "ttll-4", "ttll-11", "wdr-31", "wdr-54","arl-13"),
        names_to = "Names", 
        values_to = "Value",
        values_drop_na = TRUE)                
```  

#### Step 4: Draw box plot using ggplot() and apply Wilcoxon paired test

``` Java
fig_2_l %>%
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
      ylim(0,15) +
      stat_compare_means(comparisons = wt_my_comprasion,label = "p.signif",
                         label.y = 13, hide.ns = F)
 ```
 
 
