# Randomized Nyström Algorithm

This repository contains an implementation of the Randomized Nyström Algorithm using MPI.

The code was developed for the course "HPC for numerical methods and data analysis" at EPFL in the academic year 2023-2024, fall semester.

Check out the final report here: [`ferioli_koiner_project2.pdf`](./ferioli_koiner_project2.pdf).

## Authors
- Stefano Ferioli ([@ferioliste](https://github.com/ferioliste))
- Oskar Okoiner ([@okoiner](https://github.com/okoiner))

## Implementations of the algorithm
* `code/seqNystrom.py` contains our implementation of the sequential algorithm
* `code/parallelNystrom.py` contains our implementation of the parallelised algorithm 

## How to quickly run a test
The csv file `testing/test_default.csv` is used to input the testing parameters, the file is already filled with some default parameters. 
Call
```
python3 seqNystrom.py
```
or
```
mpirun -n 4 python3 parallelNystrom.py
```
from `/code` to run the test. The number of processors `4` can be changed to any other power of 4.

## Testing parameters
The following parameters have to be set inside `testing/test_default.csv`, in order to run a test:
* `matrix_type` specifies the testing matrix.
  - `0`: PolyDecay
  - `1`: ExpDecay
  - `2`: MNIST
  - `3`: YearPredictionMSD
* `R`, `p`, and `sigma` specify the parameters to build the testing matrix. Unused parameters are ignored.
* `l` and `k` specify the sketching size and the target rank, respectively.
* `sketch_matrix` specify the type of sketch matrix used.
  - `0`: SRHT
  - `1`: SASO
  - `2`: Gaussian
  - `3`: block SRHT
* `t` specifies the number of non-zeros for SASO. It is ignored otherwise.

More information about what this settings are can be found in the final report.

## Run an array of tests saving the results
1. Create a csv file like `testing/test_default.csv` with one line of settings per test.
2. Set `save_results = True` in `seqNystrom.py` or `parallelNystrom.py`.
3. Run `setup_test.py` from `/code` and enter the name of the csv file and from which line to start (`1` is the smallest possible).
4. Run `seqNystrom.py` or `parallelNystrom.py` from `/code` multiple times until the csv file is filled (this can be done for example using a shell script).
   
To rerun the same tests remove the generated data from the csv file and restart from running `setup_test.py`.

## Data folder
* `data/dataMNIST.npy` contains a reduced version of the MNIST dataset (16384 lines).
* `data/dataYearPredictionMSD.npy` contains a reduced version of the YearPredictionMSD dataset (16384 lines).
* `data/generated_matrices/` stores the testing matrices once they have been generated for the first time, so they don't need to be generated from scratch in every subsequent test.
* `data/nuclears_norms/` stores the nuclear norms of the testing matrices once they have been generated for the first time (again, for performance reasons).

