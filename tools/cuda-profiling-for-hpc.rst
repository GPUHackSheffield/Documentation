.. _cuda_profiling_for_HPC:

CUDA Profiling for HPC
======================

When using HPC systems it can be difficult to attach profiling GUIs for interactive profiling. Instead it is best to profile remotely capturing as much data as possible and viewing profile information locally.

CUDA profiling tools offer timeline-style tracing of GPU activity, plus detailed kernel level information.

Newer CUDA versions and GPU architectures can use Nsight Systems and Nsight Compute. 
All current CUDA versions and GPU architectures support Nvprof and the Visual Profiler.


Compiler settings for profiling
-------------------------------

Compile with ``-lineinfo`` (or ``--generate-line-info``) to include source-level profile information. 
Do not profile debug builds, it will not be representative.


Nsight Systems and Nsight Compute
---------------------------------

.. note:: 
   Requires CUDA >= 10.0 and Compute Capability > 6.0

Trace application timeline using remote Nsight Systems CLI (``nsys``):

.. code-block:: bash

   nsys profile -o timeline ./myapplication

Import into local Nsight Systems GUI (``nsight-sys``): 

+ ``File > Open``
+ Select ``timeline.dqrep``


Capture Kernel level info using remote Nsight CUDA CLI (``nv-nsight-cu-cli``):

.. code-block:: bash
   
   nv-nsight-cu-cli -o profile ./bin/Release/atomicIncTest 


Import into local Nsight CUDA GUI ``nv-nsight-cu`` via: 

.. code-block:: bash

   nv-nsight-cu profile.nsight-cuprof-report


**Or** Drag ``profile.nsight-cuprof-report`` into the ``nv-nsight-cu`` window.




Documentation
^^^^^^^^^^^^^

+ `Nsight Systems <https://docs.nvidia.com/nsight-systems/>`_
+ `Nsight Compute <https://docs.nvidia.com/nsight-compute/>`_


Visual Profiler (nvprof and nvvp)
---------------------------------

.. note:: 
   Suitable for all current CUDA versions and GPU architectures


Trace application timeline remotely using ``nvprof``:

.. code-block:: bash

   nvprof -o timeline.nvprof ./myapplication


Capture kernel-level metrics remotely using ``nvprof`` (this will take a while):

.. code-block:: bash

   nvprof --analysis-metrics -o analysis.nvprof ./myapplication


Import into the Visual Profiler GUI (``nvvp``)

+ ``File > Import``
+ Select ``Nvprof``
+ Select ``Single process``
+ Select ``timeline.nvvp`` for ``Timeline data file``
+ Add ``analysis.nvprof`` to ``Event/Metric data files``

Documentation
^^^^^^^^^^^^^

+ `Nvprof Documentation <https://docs.nvidia.com/cuda/profiler-users-guide/index.html>`_
