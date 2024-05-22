
## Figure 1

## Figure 1B-ASE vs. ASI cilia length comparison 

![ase_ası](https://github.com/mervegulturan/BBSome-regulates-ARL13B-dependent-joint-elongation-of-two-distinct-cilia-in-C.-elegans/assets/96948625/eb828e6d-26d5-446b-b944-0f8573506670)

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
fig_1_head<- read_xlsx("Figure_1_ASE_ASI Cilia Length.xlsx", sheet = 1)
  colnames(fig_1_head)
```

#### Step 3: Organize data

``` Java
  fig_1_head<- select (fig_1_head, c("wt_ase", "wt_asi"))
  
  fig_1_head <- fig_1_head %>%
    pivot_longer(
      cols = c("wt_ase", "wt_asi"),
      names_to = "Names", 
      values_to = "Value",
      values_drop_na = TRUE)
  
  level_order <- c("wt_ase", "wt_asi")
  wt_my_comprasion <- list(c("wt_ase", "wt_asi"))
```

#### Step 4: Draw box plot using ggplot() and apply statistical analysis

``` Java
fig_1_head %>%
    ggplot(aes(x=factor(Names,level = level_order), 
               y=Value, fill= Names))+
    geom_boxplot(aes(color = Names,
                     fill = after_scale(desaturate(lighten(color, 0.4), .3))),
                 size = 1,width=0.8)  +
    scale_color_manual(values=c("#6698ff","#0da9dd")) +
    geom_jitter(width=0.1, alpha=0.5) +
    theme(axis.line = element_line(colour = "Black"),
          panel.grid.major = element_line(colour = "White"),
          panel.grid.minor = element_line(colour = "White"),
          panel.border = element_blank(),
          panel.background = element_blank(),
          axis.ticks.x=element_blank(),
          axis.text.x=element_text(angle=-270)) +
    labs( y = "Cilia Lenght (µm)")  +
    ylim(0,10) +
    stat_compare_means(comparisons = wt_my_comprasion,label = "p.signif",
                       label.y = 9.5, hide.ns = F) 
```


## Figure 1C-PHA vs. PHB cilia length comparison 
![Rplot](https://github.com/mervegulturan/BBSome-regulates-ARL13B-dependent-joint-elongation-of-two-distinct-cilia-in-C.-elegans/assets/96948625/ecad92b4-690c-4de3-919f-396b2aaaf6b0)

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
fig_1<- read_xlsx("figure_1.xlsx", sheet = 1)
colnames(fig_1)
```

#### Step 3: Organize data

``` Java
fig_1<- select (fig_1, c("PHA_WT","PHB_WT"))
level_order <- c("PHA_WT","PHB_WT")
wt_my_comprasion <- list(c("PHA_WT","PHB_WT"))

fig_1 <- fig_1 %>%
  pivot_longer(
    cols = c("PHA_WT","PHB_WT"),
    names_to = "Names", 
    values_to = "Value",
    values_drop_na = TRUE)
```

#### Step 4: Draw box plot using ggplot() and apply statistical analysis

``` Java
fig_1 %>%
  ggplot(aes(x=factor(Names,level = level_order), 
             y=Value, fill= Names))+
  geom_boxplot(aes(color = Names,
                   fill = after_scale(desaturate(lighten(color, 0.4), .3))),
               size = 1,width=0.8)  +
  scale_color_manual(values=c("#6698ff","#0da9dd")) +
  geom_jitter(width=0.1, alpha=0.5) +
  theme(axis.line = element_line(colour = "Black"),
        panel.grid.major = element_line(colour = "White"),
        panel.grid.minor = element_line(colour = "White"),
        panel.border = element_blank(),
        panel.background = element_blank(),
        axis.ticks.x=element_blank(),
        axis.text.x=element_text(angle=-270)) +
  labs( y = "Cilia Lenght (µm)")  +
  ylim(0,10) +
  stat_compare_means(comparisons = wt_my_comprasion,label = "p.signif",
                     label.y = 9, hide.ns = F)
 ```                    
