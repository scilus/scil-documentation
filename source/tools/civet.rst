.. _ref_civet:

Civet
=====

`Civet <http://www.bic.mni.mcgill.ca/ServicesSoftware/CIVET>`_ is a tool created by the McConnel BBrain Imaging Center (McGill) to extract cortical surfaces (see also :ref:`ref_fsl_freesurfer`).

The easiest way to use it is through :ref:`ref_cbrain`.

    1. Convert your data into the .mnc format (to convert from nifti, see `here <http://www.bic.mni.mcgill.ca/ServicesSoftware/ConvertingOtherFileTypesToMINC>`_.

    2. On brain, the options you should choose are:

        - N3: 100
        - Select "ANIMAL" by clicking on the box.
        - Example of prefix pattern that fits tractoflow: {1} (i.e. sub)
        - Example of id pattern that fits tractoflow: {2}__{3} (i.e. ID__t1 for instance).
