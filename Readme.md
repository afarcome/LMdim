This project reports R code for implementing the methods in the paper "Dimensionality reduction for longitudinal multivariate data by optimizing class separation of projected latent Markov models".

The following libraries shall be installed in R before using code from
this project:

library(HiddenMarkov)

library(orthoDr)

library(pracma)

library(LMest)

library(GA) 

library(logisticPCA)

The main function for implementation is called LMdimCat, and it implements the methodology for a binary multivarate outcome.  

The function takes in input: 

  Y,                 # binary array n (subjects) by Ti (times) by H (items)

  k,                 # number of mixture components

  nproj              # number of projections, defaults 1
                     # if nproj=0, unidimensional projections orthogonal to
		     # the user specified matrix w0 are found (see "sequential 
                     # approach in the main paper")

  outerTol           # tolerance for the outer optimization (over weights, defaults 1e-3)
  
  innerTol           # tolerance for the inner optimization (over LM parameters, defaults 1e-3)

  w0                 # if nproj>0, initial solution; if nproj=0, solution is orthogonal to w0 (defaults NULL, and ignored)

  alg                # algorithm for outer optimization: "opt" for optim, "GA" for genetic (defaults "opt")

  inits              # algorithm for starting solution: "logisticSVD", "logisticPCA", "random" (defaults "logisticSVD") 

and gives in output, if nproj<1, a list with elements:

optD: class separation at convergence

w: optimal weight vector

xi: vector of k latent means

sd: vector of k latent standard deviations 

delta: vector of initial probabilities

Pi: transition matrix

Z: optimal unidimensional projection 

inits: initial solution

if nproj>1 the output is a list of length nproj in which each element of the list is a list itself with the same first sevel elements as above, plus

inits: initial solution

totDortho: sum of class separation values over the nproj projections.

Clearly, the nproj optimal weight vectors are orthonormal. 

