.. _ref_glassbrain:

Making a glass brain
====================

This example shows how to create a glass brain image using a brain mask
to visualize and contextualize fiber bundles. Best viewed in mrview but can
work in MI-Brain.

The series of commands is inspired from `this <https://community.mrtrix.org/t/fiber-tract-visualised-on-a-glass-brain/4932/2>`__ but adapted to use scilpy instead. Adjust the variable ``RES`` to change the voxel size of the output image. A lower value will give a smoother result but will take longer to compute and be heavier on memory.


.. code-block:: bash

    IN=brainmask.nii.gz
    OUT=glass_brain.nii.gz
    RES=0.2

    scil_volume_resample.py ${IN} resampled.nii.gz --voxel_size ${RES} --interp cubic -f
    scil_volume_math.py blur resampled.nii.gz 2 smooth.nii.gz -f --data_type float32
    scil_volume_math.py lower_threshold smooth.nii.gz 0.3 threshold.nii.gz -f --data_type uint8
    scil_volume_math.py dilation threshold.nii.gz 2 dilated.nii.gz -f
    scil_volume_math.py subtraction dilated.nii.gz threshold.nii.gz ${OUT} -f

To view the output in mrview, first open a subject's image you want to visualize other than the glass brain. Then, add the glass brain as an overlay. Go to "View" and select "Volume render" (or press F3). At the bottom of the overlay window: deactivate interpolation, change the color scheme to "Gray" and reduce opacity.

To view the output in MI-Brain, load the output. Right-click the image and select "Create a polygon model". Reduce the opacity of the polygon model to something low and change the color to something gray-ish.

Here are some examples of the output images:

.. image:: /images/glass_brain_mibrain.png
   :alt: Glass brain image
   :width: 45%
   :align: left 

.. image:: /images/glass_brain_mrview.png
   :alt: Glass brain image
   :width: 45%
   :align: right 

