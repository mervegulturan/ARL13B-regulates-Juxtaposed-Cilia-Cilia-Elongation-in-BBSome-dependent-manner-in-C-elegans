## Figure 3

## Figure 3C
##  Bar plot for presenting phenotypic differences in ASE and ASI cilia 

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

## Figure 3D
## Cilia lenght for ASE&ASI cilia in wild-type and arl-13 single mutant
![figure_3d](https://github.com/user-attachments/assets/fae3fe75-da5d-41bc-9251-8e38e10a1fff)

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
fig_3d<- read_xlsx("ASE_ASI_comp.xlsx", sheet = 1)
colnames(fig_3d)
```

 #### Step 3: Organize data

``` Java
fig_3d <- fig_3d %>%
  pivot_longer(
    cols = c("wt_ASE","wt_ASI","arl_13_ASE","arl_13_ASI"),
    names_to = "Names",
    values_to = "Value",
    values_drop_na = TRUE)

level_order <- c("wt_ASE","wt_ASI","arl_13_ASE","arl_13_ASI")
ase_my_comprasion <- list(c("wt_ASE", "arl_13_ASE"))
asi_my_comprasion <- list(c("wt_ASI", "arl_13_ASI"))
```

#### Step 4: Draw box plot using ggplot() and Wilcoxon paired test

``` Java
fig_3d %>%
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
  stat_compare_means(comparisons = ase_my_comprasion,label = "p.signif",
                     label.y = 9.7, hide.ns = F)  +
  stat_compare_means(comparisons = asi_my_comprasion,label = "p.signif",
                     label.y = 9, hide.ns = F)
```

## Figure 3F
## Phenotypic differances in arl-13 single mutant and rescue worms

![arl-13_rescue_phenotype](https://github.com/user-attachments/assets/829f08ec-e68b-43e5-bc67-ad64ffa97ec5)

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
fig_3f<- read_xlsx("Figure_3F.xlsx", sheet = 2)
colnames(fig_3f)
```

#### Step 3: Organize data

``` Java
fig_3f <- fig_3f %>%
  pivot_longer(
    cols = c("arl-13","arl-13_rescue"),
    names_to = "Names", 
    values_to = "Value",
    values_drop_na = TRUE)

level_order <- c("arl-13","arl-13_rescue")
wt_my_comprasion <- list(c("arl-13","arl-13_rescue"))
```

#### Step 4: Draw bar plot using ggplot()

``` Java
fig_3f %>%
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
  
  fig_<- data.frame("arl-13"=c(34,5), "rescue"=c(20,14),
                    row.names = c("Normal", "Misdirection"))
  pairwise_fisher_test(as.matrix(fig_), p.adjust.method = "fdr")
```
