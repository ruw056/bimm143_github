# Class 06: R Functions
Eric Wang PID: 17678188

- [Background](#background)
- [A first function](#a-first-function)
- [A second function](#a-second-function)
- [A new cool function](#a-new-cool-function)

## Background

Functions are at the heart of using R. Everything we do involves calling
and using functions (from data input, and analysis to results output).

All functions in R have at least 3 things:

- A **name** the thing we use to call the function.
- One or more input **arguments** that are comma separated
- The **body**, lines of code between curly brackets {} that does the
  work of the function.

## A first function

Let’s write a silly wee function to add some numbers:

``` r
add <- function(x) {
  x + 1
}
```

Let’s try it out

``` r
add(100)
```

    [1] 101

Will this work

``` r
add( c(100,200,300))
```

    [1] 101 201 301

Modify to be more useful and add more than just 1

``` r
add <- function(x, y = 0) {
  x + y
}
```

``` r
add(60,50)
```

    [1] 110

Will this work?

``` r
add(100)
```

    [1] 100

``` r
log(10, base = 10)
```

    [1] 1

**N.B.** input arguments can be required or optional. Optional ones have
a default. You can specifiy it in the function code with an equals sign.

``` r
#add(11,200,300)
```

## A second function

All functions in R look like this

    Name <- function(arg) {
      Body
    }

The `sample()` function in R will randomize the numbers within a certain
data set.

- By default, the function samples without replacement (no repeats).

- If you want to have repeats you can have
  `sample(x, size, replace = True)`

- If you want to find the probability for a value to show up you can
  also include `sample(x,size,replacement = True, prob = )`

``` r
sample(1:100)
```

      [1]  66  69  46   7  71  60  87   6 100  32  64  45  54  23  58  74   4  89
     [19]  61  93  57   5  31  49  19  30  37  73  81  83  17  68  18  67  43  40
     [37]  21  10  77  26  90  59  96  25  41  91  11  22  79  98  75  29  44   2
     [55]   3   1  97  24  72  76  12   9  20  13  53  85  70  27  55  62  92  99
     [73]  86  78  80  34  35  14  65  33  16  39  28  51  15  48  95  56  94  36
     [91]  47  50   8  88  42  63  84  52  38  82

> Q. Return 12 numbers picked randomly from input 1:10

``` r
sample(1:10, 12, TRUE)
```

     [1] 10  1  3  9  3  1  5  9  3  3  2  2

> Q. Write the code to generate a random 12 nucleotide long DNA sequence

sample(“A,G,T,C”, 12, TRUE)

``` r
x <- c("A", "T","C","G")
sample(x, 12, TRUE)
```

     [1] "A" "C" "A" "T" "A" "C" "G" "T" "C" "C" "C" "G"

> Q. Write a first version function called `generate_dna()` that
> generates a user specified length `n` random DNA sequence.

``` r
generate_dna <- function(n=6) {
  sample(x, n, replace = TRUE)
  
  }
generate_dna(40)
```

     [1] "C" "A" "G" "C" "C" "G" "A" "C" "T" "T" "G" "A" "A" "T" "T" "A" "A" "G" "A"
    [20] "G" "T" "T" "G" "G" "G" "G" "C" "G" "C" "G" "A" "C" "G" "T" "T" "T" "C" "G"
    [39] "G" "T"

> Q. Modify your function to return a FASTA like sequence so rather than
> \[1\] “T” “C” “T” “C” “C” “G” “C” “A” “T” “C” “C” “T” we want “GCAAT”

``` r
bases <- c("G","C","A", "T")
generate_dna <- function(n=6) {
  paste(sample(bases, n, replace = TRUE),collapse = "" )
  }
generate_dna(40)
```

    [1] "CGGACTGGGTTCACTTTCTCGCGAAAACTGCGGGACTACG"

> Q. Give the use an option to return FASTA format output sequence or
> standard multi-element vector format.

``` r
bases <- c("G","C","A", "T")
generate_dna <- function(n=6, fasta = TRUE) {
  bases <- c("G","C","A", "T")
  x <- sample(bases, n, replace = TRUE)
  
  if(fasta){
  x <- paste(x,collapse = "" )
  }
  return(x)
  }
generate_dna(40, FALSE)
```

     [1] "G" "T" "C" "C" "G" "T" "C" "A" "A" "C" "G" "A" "G" "A" "A" "A" "C" "G" "C"
    [20] "G" "C" "A" "C" "A" "C" "T" "T" "T" "C" "G" "G" "A" "G" "A" "T" "T" "T" "C"
    [39] "T" "G"

## A new cool function

> Q. Write a function called `generate_protein()` that generates a user
> specied length protein sequence in FASTA like format

``` r
generate_protein <- function(n=6){
  aa <- c("A","R","N","D","C",
          "Q","E","G","H","I",
          "L","K","M","F","P",
          "S","T","W","Y","V")
  fasta.aa <- sample(aa, n, replace = TRUE)
  fasta.aa <- paste(fasta.aa, collapse = "")
  return(fasta.aa)
}
generate_protein(6)
```

    [1] "TDFTDR"

> Q. Use your new `generate_protein()` function to generate sequences
> between length 6 and 12 amino-acids in length and check of any of
> these are unique in nature.

``` r
lengths <- 6:12
proteins <- lapply(lengths, generate_protein)
proteins
```

    [[1]]
    [1] "YNSHPG"

    [[2]]
    [1] "TRMGIIG"

    [[3]]
    [1] "IKVVYYQQ"

    [[4]]
    [1] "PCFVKACWQ"

    [[5]]
    [1] "RLRSCWLPKF"

    [[6]]
    [1] "VTRSRINYSNF"

    [[7]]
    [1] "IDGHDQAKRRMS"

``` r
#lapply(x,function)
```

- applies a function to each element of x

- always returns a list

``` r
#sapply(x,function)
```

- applies a function to each element of x

- always returns a vector or matrix

Or we could do a `for()` loop:

``` r
for(i in 6:12) {
  cat(">", i, sep="", "\n")
  cat(generate_protein(i), "\n")
}
```

    >6
    TKGNWK 
    >7
    NMMSGPT 
    >8
    DDALDQTE 
    >9
    KLHFMSAMH 
    >10
    PAILYDHSKE 
    >11
    PATLQYIQEDY 
    >12
    YPGSMAYGRFEF 

Identical matches with 100% coverage were only found in sequences of 6
and 7.
