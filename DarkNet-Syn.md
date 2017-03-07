#### Step 1. Install and load required packages for correlations and partial correlations graphs.
`install.packages("qgraph")` #see [qgraph: Network Visualizations of Relationships in Psychometric Data](http://www.jstatsoft.org/v48/i04/) for details 

`library(qgraph)` #load qgraph

#### Step 2. Load simulated HDS data and store as a correlation matrix (or tetrachoric as items are dichotomous).

For illustration purposes, code is illustrated with the *Pearson* correlation matrix.

```Rouge
install.packages("qgraph")
HDS.Sim.cor <- cor(HDS.Sim) #Pearson
HDS.Sim.tet <- tetrachoric(HDS.Sim) #Tetrachoric
```

#### Step 3. Plot the correlation and partial correlation networks (figures A and B).

```Rouge
groups <- c(rep("Narcissism", 14), rep("Psychoticism", 14), rep("Machievallianism", 14))

##Correlation network##
netCor <- qgraph(HDS.Sim.cor, layout = "spring", labels = colnames(HDS.Sim.cor), groups = groups, 
vsize=4, title = "A. Correlation Network", legend = F)

##Partial correlation network##
netPcor <- qgraph(HDSDT.tr, layout = "spring", labels = colnames(HDSDT.tr), groups = groups, graph = "concentration", 
vsize = 4, title = "B. Partial Correlation Network", legend = F, cut = .10, esize = 10)
```
