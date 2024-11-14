# AWS cluster information

### Compute nodes

The cluster has two types of compute nodes. The default nodes (`defq`) have
24 cores (48 threads) with 96GB RAM and 900GB of local scratch space.
Tiny nodes (`tiny`) have 2 cores (4 threads) with 32GB RAM and 150GB of local scratch.

The "spot" queues (`defq-spot` and `tiny-spot`) should be used if possible since they are signficantly less expensive than on-demand nodes. With spot instances there is a chance your job will be interruped. We have yet to test spot instances with our snakemake workflows.  (see [Working with spot instances](https://docs.aws.amazon.com/parallelcluster/latest/ug/spot.html))

### Filesystems

Several filesystems are mounted on the head node and compute nodes. 

The `/efs` filesystem is an "elastic file system" that automatically grows and shrinks as files are added, you pay for what you use. User home directories are located in `/efs/users`.

The `/fsx` filesystem is a high performance parallel filesystem, we currently have provisioned 9TB. Due to the performance benefits, it is recommended to have analyses use this filesystem for IO and to move inactive projects to `/efs`. Also (in my experience) lustre filesystems tend to be a bit unstable, so you would not want to keep files here that are difficult to obtain - there is a chance they might get lost. 

Finally, `/local` is a solid-state drive that is attached directly to each compute node and provides the fastest IO of any of the filesystems. This filesystem is not shared among nodes and should be used for temporary files. The environment variable `TMPDIR` is set to `/local`. 

## Initial Setup

### Useful symlinks

I like to create symlinks to frequently used directories in my home directory.
This is especially useful when using programs like cyberduck.

```bash
ln -s /fsx/users/$(whoami) myfsx
```

### Install miniconda

The miniconda installer is located at `/efs/software/Miniconda3-py39_4.10.3-Linux-x86_64.sh`. To install miniconda:

```bash
bash /efs/software/Miniconda3-py39_4.10.3-Linux-x86_64.sh -b -p $HOME/miniconda3
$HOME/miniconda3/bin/conda init
```

Log out and log back in to activate the base environment. Your command prompt will now be prefixed by your current environment, `base`.

```bash
(base) [bendall@ip-10-0-0-65 ~]$
```

Install `mamba` into base environment. `mamba` is a drop-in replacement for `conda` and is much faster.

```bash
conda install -n base -c conda-forge mamba
```

Set up bioconda by setting channel order

```bash
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

### Install snakemake

Create a clean environment with just snakemake and snakedeploy

```bash
mamba create -c conda-forge -c bioconda -n snakemake snakemake snakedeploy mamba
```

### Setup git

```bash
git config --global user.name "[first name] [last name]"
git config --global user.email "[email]"
```

```bash
ssh-keygen -t ed25519 -C "[email]"
```

Copy key at `~/.ssh/id_ed25519.pub` to Github

### Setup SSH within cluster

Copy your new public key to your authorized keys so you can authenticate to different nodes

```bash
cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
```

### Test SLURM

`sinfo` tells you what is the cluster status

```bash
sinfo
```

`squeue` tells you about specific jobs. The alias `qstat` and `allstat` is a more readable version for your jobs and all jobs, respectively.

```bash
squeue
qstat
allstat
```

Submit the following job.

```bash
sbatch -c 2 -p tiny-spot <<EOF
#!/bin/bash
sleep 60
echo "hello world from $(hostname)"
EOF
```

Check the status of the cluster (using `sinfo`) and the job (using `qstat`) and 
notice the different states the job goes through.

Once a node has been allocated and configured, you can SSH into the node. For example, if the
node is called `tiny-spot-dy-r5adxlarge-1`, do this to log in to that node.

```
tiny-spot-dy-r5adxlarge-1
```

This is useful to check on resources being used by a running job or even to run tasks
when the node isn't fully utilized.





