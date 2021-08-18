# REML

## Description
The REML function  in R


## Installation
```R
install.packages("devtools")
devtools::install_github("LeonSong1995/REML", build_vignettes=F)
```


## Usage
```R
library(MLM)
###example##
n = 1000
#fixed component
x = replicate(10,rnorm(n,0,1))
#random component1
z1 = replicate(200,rnorm(n,0,1))
#random component2
z2 = replicate(200,rnorm(n,0,1))
#simulated y 
y = x %*% rnorm(ncol(x)) +  
  z1 %*% rnorm(ncol(z1)) + 
  z2 %*% rnorm(ncol(z2)) + rnorm(n)

#reml function
R = reml(start = c(1,1),X = as.matrix(x),y = y,Z = list(z1,z2),maxiter = 1000)

beta = R[[1]][1,]
blup = R[[2]][1,]

##predication
y_pred = x %*% beta + cbind(z1,z2) %*% blup
cor(y,y_pred)

```

