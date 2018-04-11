## Dark-Side-Networks
R Code and simulated dataset to reproduce analyses for 2017 SIOP Poster on Dark Triad as a causal network.

## Project and Data Description
This repository includes instructions, R syntax, and simulated data for the 2017 SIOP poster: "Dark personality as a causal system: A network approach." Note there will be slight variations in node position and centrality due to simulated nature of the dataset; however, a majority of conclusions about global configuration, centrality, and clustering remain the same. The following aspects of the project can be accessed.

- HDS item-level correlations (N = 62,997), descriptive statistics, and code for simulating a multivariate binary-item dataset in the `SimData-Syn.md` file.
- Simulated dataset of the 42-item Hogan Development Survey analog of the Dark Triad in `SimData.HDS.zip`
- R syntax for replicating network diagrams and analyses in `DarkNet.Syn`
- Full submission in `Dark Side Derailers as Causal Systems-2017 Poster.docx.` Item content removed to protect propietary key. 

## Requirements

- R > 3.0 (possibly earlier versions will work)

The following R packages should be installed and loaded to simulate the item-level data and run network analyses. 

```
install.packages("bindata")
install.packages("psych")
install.packages("qgraph")
install.packages("parcor")
```

## References

The inspiration, theory, and code for the following project comes from active applications in personality psychology. The primary work providing the logic, structure, and open source syntax for applying these algorithms comes from the following citation:

- [Schroeders, U., Wilhelm, O., & Olaru, G. (2016). Meta-heuristics in short scale construction: ant colony optimization and genetic algorithm. PloS one, 11(11), e0167110.](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0167110)

## License

This data and analysis are being prepared for publication and review. The repository is copyrighted and no permission is granted to re-analyse the data for publication or reuse any of the materials. After publication, code and data will ultimately be GPL-2; all measurement scales retain existing licence.
    
Any publication that re-uses the data should cite this publication.

