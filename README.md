## Dark-Side-Networks
Code and simulated dataset to reproduce analyses for 2017 SIOP Poster on Dark Triad as a causal network

## Description
This repository includes instructions, R syntax, and simulated data for the 2017 SIOP poster: "Dark personality as a causal system: A network approach." 

## Requirements

- R > 3.0 (possibly earlier versions will work)

The following packages should install the required R packages for simulating 

```
install.packages("psych")
install.packages("qgraph"
install.packages("parcor")
```
## Data Description

A simulated dataset of the 42-item subset of the Dark Triad analog of the Hogan Developmental Survey (N = 62,997) is provided in the [SimData](https://github.com/Simmy56/Dark-Side-Networks/blob/readme-mods/SimData) folder. The code for simualting the multivariate binary-item dataset (i.e., True/False Items) is provided in the (/) folder. 

## References

The inspiration, theory, and code for the following project comes from the highly active [Psychosystems](http://psychosystems.org/) group. Notable citations and references with regard to personality and psychopathology constructs as networks of mutually reinforcing behaviors include:

- [Borsboom, D., & Cramer, A. O. (2013). Network analysis: an integrative approach to the structure of psychopathology. Annual review of clinical psychology, 9, 91-121.](https://www.ncbi.nlm.nih.gov/pubmed/23537483)

- [Cramer, A. O., Sluis, S., Noordhof, A., Wichers, M., Geschwind, N., Aggen, S. H., ... & Borsboom, D. (2012). Dimensions of normal personality as networks in search of equilibrium: You can't like parties if you don't like people. European Journal of Personality, 26(4), 414-431.](http://onlinelibrary.wiley.com/doi/10.1002/per.1866/full)

- [Costantini, G., Epskamp, S., Borsboom, D., Perugini, M., Mõttus, R., Waldorp, L. J., & Cramer, A. O. (2015). State of the aRt personality research: A tutorial on network analysis of personality data in R. Journal of Research in Personality, 54, 13-29.](www.sciencedirect.com/science/article/pii/S0092656614000701)
