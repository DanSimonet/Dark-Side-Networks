### Step 1. Install and load required packages for correlations and partial correlations graphs.
------
`install.packages("qgraph")` #see [qgraph: Network Visualizations of Relationships in Psychometric Data](http://www.jstatsoft.org/v48/i04/) for details 

`library(qgraph)` #load qgraph

### Step 2. Load simulated HDS data and store as correlation matrix (pearson or tetrachoric).
------
For illustration purposes, code is illustrated using the *pearson* correlation matrix.

```Rouge
library(psych)
HDS.Sim.cor <- cor(SimData.HDS) #Pearson
HDS.Sim.tet <- tetrachoric(SimData.HDS) #Tetrachoric
```

### Step 3. Plot correlation and partial correlation networks (figures 2A and 2B).
------
```Rouge
groups <- c(rep("Narcissism", 14), rep("Psychoticism", 14), rep("Machievallianism", 14)) #color nodes by scale

##Correlation network##
netCor <- qgraph(HDS.Sim.cor, layout = "spring", labels = colnames(HDS.Sim.cor), groups = groups, 
vsize=4, title = "A. Correlation Network", legend = F)

##Partial correlation network - Cut edge correlations < .10##
netPcor <- qgraph(HDS.Sim.cor, layout = "spring", labels = colnames(HDS.Sim.cor), groups = groups, graph = "concentration", 
vsize = 4, title = "B. Partial Correlation Network", legend = F, cut = .10, esize = 10)
```

### Step 4. Plot Adaptive LASSO network - preferred when modeling multiple associations (figure 2c).
------
`install.packages("parcor")` #Package for regularized estimation of partial correlation matrices

`library(parcor)`

Estimate the adaptive lasso network<sup>1</sup>.

```Rouge
set.seed(100)
adls <- adalasso.net(HDS.Sim) #compute partial correlation matrix via LASSO technique
network <- as.matrix(forceSymmetric(adls$pcor.adalasso)) #extract adaptive LASSO matrix
colnames(network) <- rownames(network) <- colnames(HDS.Sim)
```

Plot adaptive lasso network
```Rouge
netal <- qgraph(network, layout = "spring", labels = colnames(HDS.Sim), groups=groups, vsize=4, Title = "C. Adaptive LASSO Network", legend = F, cut = .10, esize = 10)
```

Create a uniform layout based upon the adapative lasso network (see Figure 2)
```Rouge
L <- netal$layout
qgraph(netCor, layout = L)
qgraph(netPcor, layout = L)
```

### Step 5. Extracting, describing, and testing differences in LASSO partial correlations (Table 2).
------

Creating partial correlation table (Table 2)
```Rouge
ew <- round(network,2)
ew[upper.tri(ew)] <- ""
ew <- as.data.frame(ew)
```

Descriptives and t-test for comparing difference in weights between positive v. negative edges
```
ew <- network[upper.tri(network)]
describe(ew)
sum(ew != 0)
sum (ew > 0)
sum (ew < 0)
t.test(abs (ew [ew > 0]), abs(ew [ew < 0]), var.equal = TRUE)
```

### Step 6. Calculating and visualizing global and local network properties (Figures 3-4).
------

`smallworldness(network)` #Calculate small-worldness index (Humphries & Gurney, 2008) 
                          
`centrality <- centrality_auto(network)` #Calculate and store centrality indices (Betweenness, closeness, strength)

`centralityPlot(network, theme_bw = FALSE)` #Visualize centrality indices

`cluster <- clustcoef_auto(network)` #Calculate and store clustering coefficients

`clusteringPlot(network, theme_bw = FALSE)` #Visualize multiple clustering coefficients

###Notes

<sup>1</sup> qgraph implements a similiar yet slightly distinct [EBICglasso function](http://psychosystems.org/forums/topic/ebicglasso-lambda-values/).
