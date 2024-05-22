## Figure 6

## Figure 6B-Phenotype Analysis

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
pheno6<- read_xlsx("figure_6.xlsx", sheet=3)
    colnames(pheno6)
```

#### Step 3: Organize data

``` Java 
 level_order <- c("wt","arl-13","bbs-8","ift-81","kap-1","bbs-8;arl-13",
                     "arl-13; ift-81","kap-1;arl-13")
    
    pheno6 <- pheno6 %>%
      pivot_longer(
        cols = c("wt","arl-13","bbs-8","ift-81","kap-1","bbs-8;arl-13",
                 "kap-1;arl-13","arl-13; ift-81"),
        names_to = "Names",
        values_to = "Value",
        values_drop_na = TRUE)
```

#### Step 4: Draw bar plot using ggplot()

``` Java 
    pheno6 %>%
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

## Figure 6C-Length Analysis

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
Length6<- read_xlsx("figure_6.xlsx", sheet=1)
    colnames(Length6)
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
    
    Length6 <- Length6 %>%
      pivot_longer(
        cols = c("wt","arl-13","bbs-8","ift-81","kap-1","arl-13; bbs-8",
                 "arl-13; ift-81","arl-13; kap-1"),
        names_to = "Names", 
        values_to = "Value",
        values_drop_na = TRUE)
```

#### Step 4: Draw box plot using ggplot() and Wilcoxon paired test

``` Java 
Length6 %>%
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
      stat_compare_means(comparisons = arl_13_my_comprasion,label = "p.signif",
                         label.y = 16, hide.ns = F)+
      stat_compare_means(comparisons = bbs_8_my_comprasion,label = "p.signif",
                         label.y = 15, hide.ns = F) +
      stat_compare_means(comparisons = kap_1_my_comprasion,label = "p.signif",
                         label.y = 14, hide.ns = F)+
      stat_compare_means(comparisons = ift_81_my_comprasion,label = "p.signif",
                         label.y = 13, hide.ns = F)
```


-------------------------------------------------------------------------------
## Figure S6

## Figure S6A-Phenotype Analysis

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
pheno7<- read_xlsx("figure_7_supp.xlsx", sheet=3)
colnames(pheno7)
```

#### Step 3: Organize data

``` Java
level_order <- c("wt","arl-13","tbb-4","arl-13;tbb-4")

pheno7 <- pheno7 %>%
  pivot_longer(
    cols = c("wt","arl-13","tbb-4","arl-13;tbb-4"),
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
           linewidth = 0.5, stat='identity', na.rm = TRUE) +
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

fig_<- data.frame("wt"=c(7,12), "arl-13"=c(21,24),
                  row.names = c("Normal", "Misdirection"))
pairwise_fisher_test(as.matrix(fig_), p.adjust.method = "fdr")
```

## Figure S6B-Length Analysis

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
 Length7<- read_xlsx("figure_7_supp.xlsx", sheet=1)
colnames(Length7)
```

#### Step 3: Organize data

``` Java
wt_my_comprasion <- list(c("wt","arl-13"),c("wt", "tbb-4"), c("wt", "arl-13;tbb-4"))

arl_13_my_comprasion <- list(c("arl-13", "arl-13;tbb-4"))

tbb_4_my_comprasion <- list(c("tbb-4", "arl-13;tbb-4"))

level_order <- c("wt","arl-13","tbb-4","arl-13;tbb-4")

Length7 <- Length7 %>%
  pivot_longer(
    cols = c("wt","arl-13","tbb-4","arl-13;tbb-4"),
    names_to = "Names", 
    values_to = "Value",
    values_drop_na = TRUE)
```


#### Step 4: Draw box plot using ggplot() and Wilcoxon paired test

``` Java
Length7 %>%
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
  ylim(0,18) +
  stat_compare_means(comparisons = wt_my_comprasion,label = "p.signif",
                     label.y = 17, hide.ns = F) +
  stat_compare_means(comparisons = arl_13_my_comprasion,label = "p.signif",
                     label.y = 16, hide.ns = F)+
  stat_compare_means(comparisons = tbb_4_my_comprasion,label = "p.signif",
                     label.y = 15, hide.ns = F)
```
