# immediate_submit
Immediate_submit script used in many of our snakemake HPC pipelines

Example for use with a slurm cluster:

```
snakemake all --use-singularity --singularity-args "-B /tmp:/usertmp" --jobs 1001 --cluster-config data/cluster_config-slurm.yaml --cluster "$(pwd)/bin/immediate-submit/immediate_submit.py {dependencies} slurm" --immediate-submit -pr --notemp --latency-wait 600
```

The cluster config file needs to have this structure:

```
__default__: # default rule name
   job-name: DEF
   time: "00:10:00"
   ntasks: 1
   cpus-per-task: 1
   mem: 16G
   output: $(pwd)/log/cluster-logs/slurm-%j.out #the directories here need to exist
   error: $(pwd)/log/cluster-logs/slurm-%j.err
tiberius: #rule name
   job-name: tiberius
   mem: 64G
   cpus-per-task: 20
   time: "01:00:00"
```


