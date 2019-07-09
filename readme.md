# Distributed Multiplication of Sparse Matrices

This C program uses a combination of multithreading and multiprocessing to compute the product of two sparse matrices. [OpenMP](https://www.openmp.org/) was used for
thread parallelism and [Message Passing Interface](https://en.wikipedia.org/wiki/Message_Passing_Interface) (MPI) for distribution over a compute cluster.

This project was undertaken in 2018 as the final assignment for *CITS3402: High Performance Computing*
\([website](http://teaching.csse.uwa.edu.au/units/CITS3402/)/[description](http://handbooks.uwa.edu.au/unitdetails?code=CITS3402)\) at The University of Western Australia.
The written report is included for completeness, take its conclusions and analysis with a grain of salt.

## Usage

Compile code using the `mpicc`:
```
$ mpicc -std=gnu99 -fopenmp dmm.c -o dmm
```

Execute program locally (not on cluster):
```
$ ./dmm matrix1 matrix2
```

Note that the number of compute nodes and threads are determined by cluster specific configuration.

### Matrix format requirements

Matrices should be formatted as follows:

- non-zero matrix elements shall be formatted as `x y value`, separated by a single space character
- only one element per line
- all unlisted elements are zero

eg.
```
//Original Matrix
3 0 0 0
0 0 1 0
0 5 0 2
0 0 0 0
  | |
  V V
//Formated
0 0 3
2 1 1
1 2 5
3 2 2
```

See attached report for a further example.

## Improvements

At the time of writing, I was not aware of `mpi_broadcast`, and hence there is a significant performance hit as the number of compute nodes increases (unmentioned in the performance report).
As I no longer have access to the university's compute cluster, I am not able to test/verify the performance of the program using broadcasting. ~~I have instead
created an experimental branch implementing these features.~~ (This would require a significant rewrite, and hence will not be happening in the foreseeable future)

## Learning HPC?

If you are learning HPC and/or have a similar assessment feel free to first _*learn*_ from the code and only then use it if you need (don't
forget to reference!).
