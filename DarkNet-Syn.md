### Step 1. Install and load required packages for correlations and partial correlations graphs.
------
`install.packages("qgraph")` #see [qgraph: Network Visualizations of Relationships in Psychometric Data](http://www.jstatsoft.org/v48/i04/) for details 

`library(qgraph)` #load qgraph

### Step 2. Load simulated HDS data and store as correlation matrix (pearson or tetrachoric).
------
For illustration purposes, code is illustrated using the *pearson* correlation matrix.

```Rouge
`library(psych)` 
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

Estimate the adaptive lasso network

```Rouge
set.seed(100)
adls <- adalasso.net(HDS.Sim) 
network <- as.matrix(forceSymmetric(adls$pcor.adalasso))
colnames(network) <- rownames(network) <- colnames(HDS.Sim)
```


netqg <- qgraph(network, layout = "spring", labels = colnames(Data), groups=groups)
```
