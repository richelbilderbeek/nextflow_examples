# nextflow_examples

My own Nextflow examples

 * [Example 1](https://github.com/richelbilderbeek/nextflow_example_1): 
   Nextflow tutorial examples
 * [Example 2](https://github.com/richelbilderbeek/nextflow_example_2): 
   A first process creates a file that is used by the second process,
   using a container
 * [Example 3](https://github.com/richelbilderbeek/nextflow_example_3): 
   Use Nextflow Tower
 * [Example 4](https://github.com/richelbilderbeek/nextflow_example_4): 
   Reproduce an error
 * [Example 5](https://github.com/richelbilderbeek/nextflow_example_5): 
   A first process creates a file that is used by the second process,
   without using a container

## Troubleshooting

### Cannot find Java or it's a wrong version

```
ERROR: Cannot find Java or it's a wrong version -- please make sure that Java 8 or later (up to 18) is installed
NOTE: Nextflow is trying to use the Java VM defined by the following environment variables:
 JAVA_CMD: /usr/bin/java
 JAVA_HOME: 
```

Do:

```
export JAVA_HOME=$(readlink -f `which javac` | sed "s:/bin/javac::") ; export JAVA_CMD="${JAVA_HOME}/bin/java"
```

Or run [scripts/fix_java_error.sh](scripts/fix_java_error.sh):

```
. ./fix_java_error.sh
source fix_java_error.sh
```

See [here](https://stackoverflow.com/a/16619261) for an explanation of the `.`/`source` in front of calling the script.

### Cannot run program "sbatch"

This is a line that should always work:

```
nextflow run nf-core/nanoseq -profile test,singularity --outdir nanoseq_results 
```

However, this error can pop up:

```
java.io.IOException: Cannot run program "sbatch" (in directory "/your_folder/work/ac/8ce701d7678f94c2c6ea5c60d2fd39"): error=2, No such file or directory
```

This can happen when there is a config file in 
[the place where Nextflow searches](https://www.nextflow.io/docs/latest/config.html).
 * `nextflow.config` in the current directory
 * `nextflow.config` in the workflow project directory
 * The config file `$HOME/.nextflow/config`

Remove/move that config file. 

## Links

 * [Nextflow cheat sheet](https://github.com/danrlu/Nextflow_cheatsheet)
 * [Nextflow and Docker course](https://github.com/nextflow-io/crg-course-nov16)
