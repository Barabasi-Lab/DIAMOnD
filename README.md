# DIAMOnD

This is a guide on how to run the DIAMOnD algorithm, as described in [Ghiassian et al. PLoS Comput Biol (2015)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4390154/).


## Introduction

DIAMOnD is a network-based methodology to uncover the disease module associated with a particular phenotype. DIAMOnD uses as input the interactome and a set of proteins *known* to be associated with the phenotype of interest, which we call **seeds**. Then, it uses an iterative algorithm to calculate the significance of the interactions of the proteins in the neighborhood of the seeds (i.e. a p-value indicating if the number of interactions is higher than a random expectation). The proteins are ranked according to their respective p-values, and the protein with the highest rank (i.e. lowest p-value) is added to the set of seeds, increasing their number. These procedure is is repeated, increasing progressively the size of the disease module until a given number of steps is reached.


## Python

- **Version**: [V1]
- **Creator**: Susan Dina Ghiassian, Joerg Menche & Albert-Laszlo Barabasi  
- **Last code update**: 2015
- **Last data update**: ??
- **Keywords**: DIAMOnD; disease module identification; network medicine
- **Rights Statement**: ??


### Instructions

1. Download the code, either by downloading the script [code/DIAMOnD.py](https://github.com/Barabasi-Lab/DIAMOnD/blob/master/DIAMOnD.py) or by cloning the repository (`git clone https://github.com/Barabasi-Lab/DIAMOnD.git`).
2. Be sure to make the code executable by running the following command in the terminal: `chmod +x DIAMOnD.py`.
3. Run the code: `./DIAMOnD.py` or `python DIAMOnD.py` in command line. Detailed instructions of how the code can be executed and an example can be found below.


#### Execution

DIAMOnD can be executed using the following commands:

`./DIAMOnD.py <network_file> <seed_file> <n> <alpha>(optional) <outfile_name>(optional)`

Or 

`python DIAMOnD.py <network_file> <seed_file> <n> <alpha>(optional) <outfile_name>(optional)`

Where the parameters are:

- `<network_file>`: Path of the file of the network. The network must have the format of an edgelist: `<node 1><separation><node 2>\n`
- `<seed_file>`:  Path of the file containing the seeds. Each seed must be separated by a new line: `<seed 1>\n<seed 2>\n...<seed n>`
- `<n>`: Desired number of steps. 200 is a reasonable starting point.
- `<alpha>` (optional): An integer representing the weight of the seeds. Default value is 1.
- `<network_file>` (optional): Path of the output file.


#### Requirements

- Python 2
- The following modules installed:
    - networkx
    - numpy
    - scipy.stats


#### Example

We can run the following example, using the input files in `example/inputs`

- `seed_genes.txt`: List of genes associated with a phenotype of interest.
```
2717
175
4669
2998
4125
...
51128
6609
2548
5476
6448
```

- `PPI.txt`: Example of protein-protein interaction network (note that identifiers in both input files should be consistent).
```
3920,5476
113457,4214
113457,7132
113457,1326
113457,1147
...
7316,6233
3423,3425
790,790
9513,9513
6233,6233
```

The following command runs the example:

`./code/DIAMOnD.py example/inputs/PPI.txt example/inputs/seed_genes.txt 100 1 example/outputs/result.txt`

It generates a list of the 100 non-seed nodes that have been ranked the highest by DIAMOnD in each iteration.
The results are saved in the output file `example/outputs/result.txt`, which looks like this:

```
#rank	DIAMOnD_node
1	4758
2	3073
3	3074
4	3938
5	2799
...
96	5597
97	2316
98	4088
99	178
100	5601
```
