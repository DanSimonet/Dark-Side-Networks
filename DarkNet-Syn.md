#### Step 1. Install and load required packages for correlations and partial correlations graphs.
`install.packages("qgraph")` #see [qgraph: Network Visualizations of Relationships in Psychometric Data](http://www.jstatsoft.org/v48/i04/) for details 

`library(qgraph)` #load qgraph

#### Step 2. Load simulated HDS data and store as a correlation matrix (or tetrachoric as items are dichotomous).

```Rouge
install.packages("qgraph")
HDS.Sim.cor <- cor(HDS.Sim) #Pearson
HDS.Sim.tet <- tetrachoric(HDS.Sim)
```
