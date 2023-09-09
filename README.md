# sinteractive

A logical counterpart to `sbatch` to help users submit interactive jobs.


## Gory details

In Slurm pre-20.11, the recommended way of submitting an interactive job
was to type a mouthfull of
```
salloc [allocation options] [--x11] srun --pty --cpu-bind=none $SHELL -l
```
It had some issues with GPUs (and GRES in general), but generally worked...
but it was a mouthful, and this was the *raison-d'etre* of this tool.

Slurm 20.11 has introduced a default behavior change with which the above
command no longer became a recommended way to start interactive jobs (due
to it breaking any subsequent `srun` and `mpirun` calls).  The new
preferred way is to set `LaunchParameters=use_interactive_step` in your
site's `slurm.conf`, and then simply call
```
salloc [allocation options] [--x11]
```
See https://slurm.schedmd.com/faq.html#prompt for more details on this.

`sinteractive` does its best to abstract the underlying complexity from the
user.  It is smart to detect current Slurm version and presence/absence of
the `use_interactive_step` parameter, and invokes the appropriate
underlying command.


## Author:

Lev Gorenstein, Rosen Center for Advanced Computing, Purdue University, 2020-2023.
Please note that as of September 2023 I am no longer affiliated with Purdue University.

Contribute: https://github.com/lgorenstein/sinteractive
