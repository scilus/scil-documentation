
Singularity / Nexflow
=====================

Singularity / docker
####################

    We have prepared most of our tools in a way that users don’t need to install too many dependencies on their computer. It saves you time and energy! The way to do that is to « wrap » the tool into a singularity, which you can see as en environment already all up-to-date and ready to use.


Nextflow
########

    If you want to run many scripts, on many subjects, one way would be to prepare a bash script (.sh) to run your study. Ex:

        .. code-block:: bash

            subjects="S01 S02 etc."
            for subj in $subjects
            do
                inputs=PATH_TO_INPUT
                bvals=PATH_TO_BVALS
                bvecs=PATH_TO_BVECTS
                frf_file=PATH_TO_FRF
                out_name=OUTPUT_NAME
                # etc.

                scil_compute_somestep
                ...
                scil_compute_fodf.py --fodf $out_name $input $bvals $bvecs $frf_file
                scil_compute_someotherstep
                ...
            done

        But analysing data often requires many steps. Preparing your own bash script with all those steps, with all the right options, could be fastidious. Most of our tools are offered as a « Nexflow ». That means that we have already created pipelines (a list of the numerous steps to process your data, for example) that will run easily on your computer in a computationally efficient, robust and reproducible way. The goal is that two users, running the same job on two different computers at two different moments, should obtain the same results!