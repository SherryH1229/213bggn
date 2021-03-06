Class 7: R-Functions and packages
================
Xuerui Huang
4/24/2019

# Load Data and functions from source

``` r
source("http://tinyurl.com/rescale-R")
```

by source the rescale-R, 3 data and 9 functions appeared in the
environmnet

test the functions

``` r
#test the rescale function
rescale(1:10)
```

    ##  [1] 0.0000000 0.1111111 0.2222222 0.3333333 0.4444444 0.5555556 0.6666667
    ##  [8] 0.7777778 0.8888889 1.0000000

``` r
#test function to change number vector to string
x <- c(1:10,"string")
is.numeric(x) #check whether the output is numerical
```

    ## [1] FALSE

# Function for recognize NA in two vectors

Testing the function for recognize NA in two vectors

``` r
#sample input
x <- c( 1, 2, NA, 3, NA)
y<-c(NA,3,NA,3, 4)

#function for checking whether two elements on the same position of two vectors have NA
both_na <- function(x,y){
  sum(is.na(x)&is.na(y))
}

both_na(x,y)
```

    ## [1] 1

# function for grading homework

Function for alcualting the final score for every studnet. Method: The
lowest score is dropped. The absence should be punished (not count as
lowest score)

``` r
student1 <- c(rep(100,time= 8),90)
student2 <- c(100,NA,NA,rep(90,time = 4),97,80)

#forloop
overall_grade <- function(stud_vec){
  stud_vec <- stud_vec[!is.na(stud_vec)]
  min_val <- min(stud_vec)
  for (i in 1:length(stud_vec)){
    if (stud_vec[i] == min_val){
      stud_vec <- stud_vec[-i]
      break
    }
  }
  mean_score <- mean(stud_vec)
  return (mean_score)
}

#better way
overall_grade_2 <- function(stud_vec){
  if (sum(is.na(stud_vec) >0)){
    stud_vec_mod <- stud_vec[!is.na(stud_vec)]
  }
  else {
    stud_vec_mod <- stud_vec
  }
  
  (sum(stud_vec_mod)-min(stud_vec_mod))/(length(stud_vec)-1)
}

#calculate the final score
overall_grade_2(student1)
```

    ## [1] 100

``` r
overall_grade_2(student2)
```

    ## [1] 69.625
