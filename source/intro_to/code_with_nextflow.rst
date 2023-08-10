Intro to Nextflow: coding your own flow
=======================================

.. role:: bash(code)
   :language: bash

This page provides an overview of the organization of a Nextflow structure, without covering every aspect. `Nextflow's Read the doc <https://www.nextflow.io/docs/latest/index.html>`_ details all the elements. See also a very good tutorial from Evan Floden `here <https://www.youtube.com/watch?v=wbtMbJTo1xo&list=PLPZ8WHdZGxmUVZRUfua8CsjuhjZ96t62R&ab_channel=Nextflow>`_.

The best way to get an example is to refer to the flows available from SCIL, in particular :ref:`ref_tractoflow` (or see their `web page <https://github.com/scilus/tractoflow/blob/master/main.nf>`_), which covers most of the aspects you'll need. See also `Rbx_flow <https://github.com/scilus/rbx_flow/blob/master/main.nf>`_ for a simpler version of Nextflow.



Overview of nextflow files
--------------------------

In general, a Nextflow pipe consists of 3 different files:

- USAGE

    | It provides information on how to use Nextflow regarding inputs and options.
    | It corresponds somewhat to the argparser arguments in scilpy scripts (help).

- nextflow.config

    It provides all the configurations required to run main.nf. In most cases, all options used in main.nf must be present in nextflow.config. You may refer to tractoflow or rbxflow for an overview of its structure (quite similar from one pipe to another).

- main.nf

    It contains all the processes in your pipeline.


Organization of the main.nf file
--------------------------------

The main.nf file has three main elements, each detailed more in sections below.

1. Setup parameters

    They provide parameters or links to nextflow.config parameters required by processes. Also provide a certain amount of information (i.e. script duration, start, end, pipe name, …).

2. Channels

    They are used to define inputs. They can take several forms.

3. Processes

    They are parts of the flow, they execute a script (command).


1. Setup parameters
********************

These are general flow directives. They can be used to import parameters defined in nextflow.config, to define global cpu or memory usage parameters, or to provide pipeline information (pipe name, start, end, duration, etc.).

Exemple :

.. code-block:: bash

    params.input = false
    params.help = false

    if(params.help) {
        usage = file("$baseDir/USAGE")
        cpu_count = Runtime.runtime.availableProcessors()
        bindings = ["param1":"$params.param1",  #param is set in nextflow.config
                          "param2":"$params.param2",
                          "param3":"$params.param3", …
              "paramN":"$params.paramN"]
        engine = new groovy.text.SimpleTemplateEngine()
        template = engine.createTemplate(usage.text).make(bindings)

        print template.toString()
        return
    }

    log.info "Name of pipeline"
    log.info "Start time: $workflow.start"

    workflow.onComplete {
        log.info "Pipeline completed at: $workflow.complete"
        log.info "Execution status: ${ workflow.success ? 'OK' : 'failed' }"
        log.info "Execution duration: $workflow.duration"
    }


2. Channels
************

For more information, see `Nextflows' doc <https://www.nextflow.io/docs/latest/channel.html>`_.

There are several ways of giving inputs to the Channel, depending on requirements.

The 2 most commonly used are (similar to glob function):

.. code-block:: bash

    #a single file
    Channel.fromPath("path/to/one/file")

    #several files
    Channel.fromFilePairs("path/to/file1", "path/to/file2","path/to/*))


There are also `operators <https://www.nextflow.io/docs/latest/operator.html>`_ to define how inputs are stored. Channel inputs can be stored in specific variables via operators. The operators map, set and into are most often used, .

Example :

.. code-block:: bash

    Channel.fromPath("path/to/fa.nii.gz", maxDepth:1)
        .map{[it.parent.name, it]}
        .set{fa_for_process1} OR
        .into{fa_for_process1;fa_for_process2}    #The dots must be aligned

It is advisable to name variables according to the processes in which they will be used.

Note that .set: is used when input(s) are stored in a single variable. When you only need a variable once, you can also write (more often used for a directory) without using .set:

.. code-block:: bash

    fa_for_process1 = Channel.fromPath("path/to/fa.nii.gz")

WARNING! An input variable cannot be used several times, i.e. each process has its own input variable. If you want to use an input in several processes, it must be stored in a number of variables corresponding to the number of processes. This is the usage of .into: is used when the input(s) are stored into several variables. These are the same inputs, so it doesn't divide them, but duplicates them. For example, above with .into fa.nii.gz is stored in fa_for_process1 and in fa_for_process2, because nextflow will use fa in process 1 and process 2.


3. Processes
************

A `process <https://www.nextflow.io/docs/latest/process.html>`_ consists of 4 parts: directives, input, output and the script. Each process is independent of the others and can be run in parallel.

Example of a process structure :

.. code-block:: bash

    inputs_variables

    process < process name > {

      directives <memory usage, cpu, …>

      input:
        <input(s) qualifier> <input(s) name>

      output:
        <output(s) qualifier> <output(s) name> [, <option>: <option value>]

      when:
        <condition>

      script:
      ”””
        < script to be executed >
      ”””
    }

The script part can also be replaced by:

.. code-block:: bash

      shell:
      ’’’
        < script to be executed >
      ’’’


**Directives:**

Directives are settings that affect the execution of the process and affect only the current process. They must be defined for each process (if necessary). Directives can be memory usage, cpu count, a directory (publishDir) or the echo function (or debug for version 22.*), https://www.nextflow.io/docs/latest/process.html#directives.

**Inputs:**

Similar to function arguments (scilpy script), the `inputs <https://www.nextflow.io/docs/latest/process.html#inputs>`_ section allows you to define the input channels of a process. A process may have at most one input block, and it must contain at least one input. All files or directories used by the script must be supplied in the input block.

There are several qualifiers: file, Path, val, …

**Outputs:**

Like function outputs in script, the `outputs <https://www.nextflow.io/docs/latest/process.html#outputs>`_ section is used to define the outputs of a process. A process can have at most one output block and must contain at least one output. Similarly as for input, there are several qualifiers : file, Path, val, tuple, ...

To save the output, it must be explicitly written to the output block. The names of the output variables must correspond to the outputs in the script block. If you don't want to save an output, simply leave it out of the output variables.

If a script block output is to be used in one or more future processes:

.. code-block:: bash

      output:
      set sid, "${sid}__output1" into output1_for_process2
      set sid, "${sid}__output2" into output2_for_process2, output2_for_process3

As with inputs, you need to create as many variables as there are processes in which the output will be used.

**script|shell:**

Part of the script executed as a Bash script. This can be any command or script available in the host environment. The difference between `script <https://www.nextflow.io/docs/latest/process.html#script>`_ (uses """) and shell (uses ''') is the way Nextflow and Bash variables are read. In the case of SCIL Nextflow, script is generally used.

**when:**

Similar to an ‘if’, `when <https://www.nextflow.io/docs/latest/process.html#when>`_ defines a condition that must be satisfied to execute the process. The condition can be any Boolean expression (true/false).


**inputs_variables:**

It's a variable containing all the inputs required by the process and supplied in the process inputs. Similar to Channel, the input variable can be constructed using operators. The operators "combine", "merge" or "join" are often used.

.. code-block:: bash

    input1
         .join/combine{input2}
         .set{ inputs_variable }  #The dots must be aligned

Several inputs can be added to the first one (using join, combine, merge, ..., depending on your input type). Please note that the order in which inputs are added must correspond to the order of the process input:

.. code-block:: bash

     input:
        set sid, file(name_input1), file(name_input2) from inputs_variable

The name_input1 can be different from the name of input1; ‘file’ here indicates that the input between () is a file. Path, val, ... can also be used as required.


Example from Rbx_flow:

.. code-block:: bash

    #inputs_variables:
    anat_for_reference_centroids
        .join(transformation_for_centroids)
        .set{anat_and_transformation}

    process Transform_Centroids {

        input:
        set sid, file(anat), file(transfo) from anat_and_transformation
        each file(centroid) from atlas_centroids

        # here each == for, the process is executed for each centroid in atlas_centroids

        output:
        file "${sid}__${centroid.baseName}.trk"

        script:

        """
        scil_apply_transform_to_tractogram.py ${centroid} ${anat} ${transfo} tmp.trk --inverse --keep_invalid

        scil_remove_invalid_streamlines.py tmp.trk ${sid}__${centroid.baseName}.trk --cut_invalid --remove_single_point --remove_overlapping_points --no_empty
        """
    }


If you have this in your process setting (nextflow.config):

.. code-block:: bash

    publishDir={"./results/$sid/$task.process"}

Nextflow will create a folder for each process with the corresponding output files.



Debugging Nextflow
------------------

There are several ways to debug a Nextflow pipeline.

- To check inputs or channels: add .view()

    .. code-block:: bash

        Channel.fromPath("path/to/one/file")
               .view() 	#The dots must be aligned

- To check processes: add ‘echo true’ or ‘debug true’ (v22) into process directives with echo commands in the script block.

    .. code-block:: bash

        process sayHello {
            echo/debug true
            script:
             "echo Hello world!"
        }

- command run: when running nextflow, add -process.echo to display echoes in processes.

    .. code-block:: bash

        nextflow run path/to/main.nf -process.echo

- Use .command.* files generated by Nextflow.

    | - Go to the work folder corresponding to the current process: cd /work/*/*
    | - Execute chmod +x * to make the nextflow .command files executable.
    | - Modify the .command.sh file as required, then run the .command.run file to run the command.sh file. Once you've found and solved the problem, modify the corresponding process main.nf.

    Please note that since Nextflow manages files in its own way, you can't run the .command.sh directly.

    You may get an error message because of logs in the .nextflow folder or other log files. If you follow the instructions given by Nextflow (delete the file or other) and rerun, it should work.


