.. _bede_scheduler:

Running and Scheduling Tasks on Bede
####################################

Slurm Workload Manager
======================

Slurm is a highly scalable cluster management and job scheduling system, used in Bessemer. As a cluster workload manager, Slurm has three key functions:

* it allocates exclusive and/or non-exclusive access to resources (compute nodes) to users for some duration of time so they can perform work,
* it provides a framework for starting, executing, and monitoring work on the set of allocated nodes,
* it arbitrates contention for resources by managing a queue of pending work.

Request an Interactive Shell
============================

Launch an interactive session on a worker node using the command:

.. code-block:: sh

    srun --pty bash -i

You can request an interactive node with multiple CPU cores by using the command:

.. code-block:: sh

    srun -c="N" --pty bash -i

The parameter "N" represents the number of CPU cores upto 4 per interactive job. Please note that requesting multiple cores in an interactive node depends on the availability. During peak times, it is unlikely that you can successfully request a large number of cpu cores interactively.  Therefore, it may be a better approach to submit your job non-interactively. 

You can request additional memory (parameter "nn" represents the amount of memory):

.. code-block:: sh

    srun --mem="NN"G --pty bash -i



Submitting Non-Interactive Jobs
===============================

Write a job-submission shell script
-----------------------------------

You can submit your job, using a shell script. A general job-submission shell script contains the "bang-line" in the first row.

.. code-block:: sh

    #!/bin/bash

Next you may specify some additional options, such as memory,CPU or time limit.

.. code-block:: sh

    #SBATCH --"OPTION"="VALUE"

Load the approipate modules if necessery.

.. code-block:: sh

    module use "PATH"
    module use "MODULE NAME"

Finally, run your program by using the Slurm "srun" command.

.. code-block:: sh

    srun "PROGRAM"

The next example script requests 40 CPU cores in total and 64Gb memory. Notifications will be sent to an email address.

.. code-block:: sh

    #!/bin/bash
    #SBATCH --nodes=1
    #SBATCH --ntasks-per-node=40
    #SBATCH --mem=64000
    #SBATCH --mail-user=username@sheffield.ac.uk

    module load OpenMPI/3.1.3-GCC-8.2.0-2.31.1

    srun --export=ALL program

Maximum 40 cores can be requested per node in the general use queues.


Job Submission
--------------

Save the shell script (let's say "submission.sh") and use the command

.. code-block:: sh

    sbatch submission.sh

Note the job submission number. For example:

.. code-block:: sh

    Submitted batch job 1226

Check your output file when the job is finished.  

.. code-block:: sh

    cat "JOB_NAME"-1226.out

Common job options
==================

Optional parameters can be added to both interactive and non-interactive jobs. Options can be appended to the command line or added to the job submission scripts.

* Setting maximum execution time
    * ``--time=hh:mm:ss`` - Specify the total maximum execution time for the job. The default is 48 hours (48:00:00)
* Memory request
    * ``--mem=#``- Request memory (default 4GB), suffixes can be added to signify Megabytes (M) or Gagabytes (G) e.g. ``--mem=16G`` to request 16GB.
    * Alternatively ``--mem-per-cpu=#`` or ``--mem-per-gpu=#`` - Memory can be requested per CPU with ``--mem-per-cpu`` or per GPU ``--mem-per-gpu``, these three options are mutually exclusive.
* GPU request
    * ``--gres:gpu=1`` - Request GPU(s)
* Specify output filename
    * ``--output=output.%j.test.out``
* E-mail notification
    * ``--mail-user=username@sheffield.ac.uk`` - Send notification to the following e-mail
    * ``--mail-type=type`` - Send notification when type is ``BEGIN``, ``END``, ``FAIL``, ``REQUEUE``, or ``ALL``
* Naming a job
    * ``--job-name="my_job_name"``
* Add comments to a job
    * ``--comment="My comments"``

For the full list of the available options please visit the Slurm manual webpage at https://slurm.schedmd.com/pdfs/summary.pdf.

Key SLURM Scheduler Commands
============================

Display the job queue. Jobs typically pass through several states in the course of their execution. The typical states are PENDING, RUNNING, SUSPENDED, COMPLETING, and COMPLETED.

.. code-block:: sh

    squeue

Shows job details:

.. code-block:: sh

    sacct -v

Details the HPC nodes:

.. code-block:: sh

    sinfo

Deletes job from queue:

.. code-block:: sh

    scancel "JOB_ID"
