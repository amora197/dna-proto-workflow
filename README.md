# dna-proto workflow (Snakemake)

<img src="https://divingintogeneticsandgenomics.rbind.io/img/snakemake.png" alt="Girl in a jacket" width="200" height="150">  

This workflow is for analysing genome re-sequencing experiments. It features 2 modes. The **de-novo** mode is used to confirm sample relationships from the raw sequencing reads with [kwip](https://github.com/kdmurray91/kWIP) and [mash](https://github.com/marbl/Mash). The **varcall** mode performs read alignments to one or several reference genomes followed by variant detection. Alignments can be performed with [bwa](http://bio-bwa.sourceforge.net/bwa.shtml) and/or [NextGenMap](https://github.com/Cibiv/NextGenMap/wiki) and  variant calling with [Freebayes](https://github.com/ekg/freebayes) and/or [bcftools mpileup](https://samtools.github.io/bcftools/howtos/variant-calling.html). If a genome annotation is available, variants are annotated with [snpEff](https://pcingola.github.io/SnpEff/).

## Authors

*   Norman Warthmann
*   Kevin Murray*
*   Marcos Conde

*This repository is based on the [PaneucalyptShortReads](https://github.com/kdmurray91/PaneucalyptShortReads)

## Usage

1.  Create a new github repository in your github account using this workflow [as a template](https://help.github.com/en/articles/creating-a-repository-from-a-template).
2.  [Clone](https://help.github.com/en/articles/cloning-a-repository) your newly created repository to your local system where you want to perform the analysis.
3.  **Setup** the software dependencies
4.  **Configure** the workflow for your needs and input files
5.  **Run** the workflow
6.  [**Archive** your workflow](https://snakemake.readthedocs.io/en/stable/snakefiles/deployment.html#sustainable-and-reproducible-archiving) for documenting your work and easy reproduction.

Some pointers for **setup**, **configuring** and **running** the workflow are below, for details please consult the documentation.

----

## [Setup](https://snakemake.readthedocs.io/en/stable/tutorial/setup.html)

An easy way to setup the dependencies is conda.

**Get the Miniconda Python 3 distribution:**

```
$ wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
$ bash Miniconda3-latest-Linux-x86_64.sh
```

**Create an environment with the required software:**

> NOTE: conda's enviroment name in these examples is `dna-proto`.

```
$ conda env create --name dna-proto --file envs/condaenv.yml
```

**Activate the environment:**

```
$ conda activate dna-proto
```

Check this [conda cheatsheet](https://gist.github.com/mv-lab/62318ff0023bd626f1e05ed9c0155fd5)

<br>

----

## Check config and metadata

We provide scripts to list metadata and configuration parameters in ```utils/```.

```
python utils/check_metadata.py
python utils/check_config.py
```

<br>

## Visualising the workflow
You can check the workflow in graphical form by printing the so-called DAG.

```
snakemake --dag -npr -j -1 | dot -Tsvg > dag.svg
eog dag.svg
```

## Pretending a run of the workflow
Prior to running the workflow, pretend a run and confirm it will do what is intended.

```
snakemake  -npr
```

## Data

Main directory content:

```
.
├── envs
├── genomes_and_annotations
├── metadata
├── output
├── rules
├── scripts
├── utils
├── config.yml
├── Snakefile
├── snpEff.config

```
> NOTE: the ```output``` directory and some files in the ```metadata``` directory are/will be generated by the workflow.

You will need to configure the workflow for your specific project. For details see the documentation. Below files and directories will need editing:

-   **Snakefile**
-   **genomes_and_annotations/**
-   **metadata/**
-   **config.yml**
-   **snpEff.config**

You can download example data for testing the workflow. [click here to download](https://drive.google.com/drive/folders/1kpJsghU-jNTSKC9uEB9khos390lZNROr?usp=sharing)

--

## How to contribute

<img align="right" width="300" src="https://github.com/firstcontributions/first-contributions/raw/master/assets/fork.png" alt="fork this repository" />

### Fork this repository

Fork this repository by clicking on the fork button on the top of this page.
This will create a copy of this repository in your GitHub account (not in your computer).

<br>

### Clone the repository

<img align="right" width="300" src="https://i.ibb.co/yVWsByF/Screenshot-from-2019-12-18-10-38-25.png" alt="clone this repository" />

Now **clone the forked repository** to your machine.
Go to your GitHub account, open the forked repository, click on the clone button and then click the *copy to clipboard* icon. The url is going to be like: ```https://github.com/your-username/dna-proto-workflow.git``` where `your-username` is your GitHub username.

Open a terminal and run the following git command:

```
git clone https://github.com/your-username/dna-proto-workflow.git
```

<img align="right" width="300" src="https://github.com/firstcontributions/first-contributions/raw/master/assets/copy-to-clipboard.png" alt="copy URL to clipboard" />

Once you've cloned your fork, you can edit your local copy. However, if you want to contribute, you'll need to create a new branch.

### Create a branch

Change to the repository directory on your computer (if you are not already there):
> NOTE: you can't change the name of the directory.

```
cd dna-proto-workflow
```

You can check your branches and active branch, using the ```git branch``` command.
```
git branch -a
```

Now create a branch using the `git checkout` command:
```
git checkout -b new-branch-name
```

For example:
```
git checkout -b development
```

From this point, you are in the new branch and edits only affect your branch. If things go wrong, simply remove your branch using
```
git branch -d name-of-the-branch
```

Or revert back to the `master`-branch using
```
git checkout master
```

### Make changes and commit

Once you've modified something, you can confirm that there are changes with `git status` (called from the top-level directory).
Add those changes to your branch with `git add`:

```
git status
git add .
or
git add name_of_the_file_you_modified
```

Commit those changes with `git commit`:
```
git commit -m "write a message"
```

### Push changes to GitHub

Push the changes in your local copy (on your machine) to your remote repository on GitHub with `git push`:
```
git push origin your-branch-name
```
replacing `your-branch-name` with the name of the branch you created earlier (e.g., `development`).


### Contributing to the project: Submit your changes for review

In your repository on GitHub, klick the `Compare & pull request` button.

<img style="float: right;" src="https://i.ibb.co/N7np2Ch/compare-and-pull.png" />

Now submit the pull request and you'll see something like:

<img style="float: right;" src="https://help.github.com/assets/images/help/pull_requests/pull-request-review-edit-branch.png" alt="submit pull request" />

We'll get notified and can check your changes and merge them into this project (in general, into the `master` branch).
