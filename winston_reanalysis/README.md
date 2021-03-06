<!-- m_matschiner Thu Jan 5 23:30:10 CET 2017-->

# winston\_reanalysis

#### Summary

The code in directory `src` performs a reanalysis of the SNP data generated by Winston et al. (2016), using divergence-time estimation with SNAPP and BEAST.

#### Input

The data set of Winston et al. (2016) will be automatically downloaded to the `data` directory using `wget`. In addition, files are provided in the `data` directory that specify the assignment of specimens to species (files `species.txt` and `species1.txt` in `data/tables`), the constraints used for divergence-time estimation (files `constraints.txt` and `constraints.xml` in `data/constraints`), and a starting tree that does not violate these constraints (file `starting.tre` in `data/trees`).

#### How to run

To conduct this reanalysis, navigate into the `src` directory and run `bash run_all.sh`. Note however, that this script will quit after generating XML format input files and preparing three replicate analysis directories for SNAPP (in `res/snapp/replicates`). SNAPP analyses will need to be conducted separately using the generated XML input files. How to run these analyses most efficiently will depend on the available computer resources, but the `start.slurm` and `resume.slurm` scripts in the three replicate analysis directories may be helpful as templates to execute SNAPP. A single analysis will sample 200000 MCMC iterations, but at least 400000 iterations per replicate will be required for convergence, thus each analysis will need to be resumed at least once. For each replicate, around 2-4 weeks of run time will be required. Once the SNAPP analyses have finished, the remaining steps listed in file `run_all.sh` can be executed by copy-pasting the commands one by one to the command line. The steps to summarize SNAPP results and to prepare BEAST analyses should require only a few seconds, however, BEAST analyses (of concatenated data sets) will then also need to be conducted separately, and how these should be run will depend on the available computer resources. BEAST analyses will require around 600000 MCMC iterations per replicate for convergence.

#### Results

Final results can then be found in directory `res/snapp/combined`. The MCC species tree will be in file `eciton.tre` and a posterior sample of 6000 trees will be in file `eciton.trees`. The same number of sampled parameter estimates will be in file `eciton.log`, which can be opened for a visual assessment of convergence in the software Tracer ([http://tree.bio.ed.ac.uk/software/tracer/](http://tree.bio.ed.ac.uk/software/tracer/)).

#### Requirements

The following software must be installed in order to run all scripts of directory `src`:

* `python3` (version 3.0 or later; [https://www.python.org/downloads/](https://www.python.org/downloads/))
* `ruby` (version 2.0 or later; [https://www.ruby-lang.org/en/](https://www.ruby-lang.org/en/))
* `java` (Java SE Development Kit 8; [http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html))
*  `wget`

#### References

Winston ME, Kronauer DJC, Moreau CS (2016) Early and dynamic colonization of Central America drives speciation in Neotropical army ants. Molecular Ecology. Advance access, doi:10.1111/mec.13846.