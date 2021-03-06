
# Coursera Peer-Graded Assignment: Catching the Inverse of a Matrix

Matrix inversion is usually a costly computation and there may be some benefit to caching the inverse of a matrix rather than compute it repeatedly (there are also alternatives to matrix inversion that we will not discuss here). Your assignment is to write a pair of functions that cache the inverse of a matrix.

## Write the following functions:

makeCacheMatrix: This function creates a special “matrix” object that can cache its inverse. cacheSolve: This function computes the inverse of the special “matrix” returned by makeCacheMatrix above. If the inverse has already been calculated (and the matrix has not changed), then the cachesolve should retrieve the inverse from the cache. Computing the inverse of a square matrix can be done with the solve function in R. For example, if X is a square invertible matrix, then solve(X) returns its inverse.

### For this assignment, assume that the matrix supplied is always invertible.

The following functions are used to create a special object that stores a matrix and caches its inverse. The first function, makeCacheMatrix creates a special “matrix”, which is really a list containing a function to:
  1.  set the value of the matrix
  2.	get the value of the matrix
  3.	set the value of the inverse
  4.	get the value of the inverse


    makeCacheMatrix <- function(x = matrix()) {
  
        i <- NULL
      
      set <- function(y) {
    
              x <<- y
            
              i <<- NULL
             
      }
     
      get <- function() x
    
      setinverse <- function(inverse) i <<- inverse
    
      getinverse <- function() i
    
      list(set = set,
    
           get = get,
         
           setinverse = setinverse,
         
           getinverse = getinverse)
         
      }
  
This function computes the inverse of the special “matrix” returned by makeCacheMatrix above. If the inverse has already been calculated (and the matrix has not changed), then cacheSolve should retrieve the inverse from the cache.

    cacheSolve <- function(x, ...) {
  
      i <- x$getinverse()
    
      if (!is.null(i)) {
    
              message("getting cached data")
            
              return(i)
            
      }
    
      data <- x$get()
    
      i <- solve(data, ...)
    
      x$setinverse(i)
    
      i
    
    }
  
# Solution

For this assignment, assume that the matrix supplied is always invertible.

# Testing

Below we call the function with a matrix, compute the inverse, retrieve the inverse from the cache list, change the call matrix to the inverse, compute the inverse on that and return the original function.

     B <- matrix(c(1,2,3,4),2,2)

     B1 <- makeCacheMatrix(B)
     cacheSolve(B1) #inverse returned after computation

     ##       [,1] [,2]

     ##[1,]   -2  1.5

     ##[2,]    1 -0.5

     cacheSolve(B1) #inverse returned from cache

     ##getting cached data
 
     ##      [,1] [,2]
     ##[1,]   -2  1.5
     ##[2,]    1 -0.5

