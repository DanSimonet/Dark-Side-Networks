### Step 1. Install and load required packages for correlations and partial correlations graphs.
------
`install.packages("qgraph")` #see [qgraph: Network Visualizations of Relationships in Psychometric Data](http://www.jstatsoft.org/v48/i04/) for details 

`library(qgraph)` #load qgraph

### Step 2. Load simulated HDS data and store as correlation matrix (pearson or tetrachoric).
------
For illustration purposes, code is illustrated using the *pearson* correlation matrix.

```Rouge
library(psych)
HDS.Sim.cor <- cor(HDS.Sim) #Pearson
HDS.Sim.tet <- tetrachoric(HDS.Sim) #Tetrachoric
```

### Step 3. Plot the correlation and partial correlation networks (figures 2A and 2B).
------
```Rouge
groups <- c(rep("Narcissism", 14), rep("Psychoticism", 14), rep("Machievallianism", 14))

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

Estimate the adaptive lasso network (NOTE: qgraph implements a similiar yet slightly distinct [EBICglasso function](http://psychosystems.org/forums/topic/ebicglasso-lambda-values/).) 

```Rouge
set.seed(100)
adls <- adalasso.net(HDS.Sim) #compute partial correlation matrix via LASSO technique
network <- as.matrix(forceSymmetric(adls$pcor.adalasso))
colnames(network) <- rownames(network) <- colnames(HDS.Sim)
```

Plot the adaptive lasso network
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

Printing partial correlation table
```Rouge
ew <- round(network,2)
ew[upper.tri(ew)] <- ""
ew <- as.data.frame(ew)
```

### Step 6. Calculating and visualizing global and local network properties (Figures 3-4).
------
