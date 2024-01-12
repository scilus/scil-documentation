.. _ref_anat:

Discover the brain anatomy
==========================

Most of us did not study in biology or anatomy. We come from physics, computer science, mathematics. But you'll probably learn many bundles' names and position, just by seeing pictures. Here are some pictures of the bundles most commonly used in the lab.


Lobes, sulcus, gyri and more
****************************

Consult the introduction to anatomy given by our anatomist collaborator Laurent Petit here:

(COPIER LE LIEN SUR BRAIN DATA. PAS DISPO LÀ...)

A few famous bundles
********************

Here are pictures of reference bundles. Here, we took the bundles used as reference when using Recobundles. They are in MNI space. To see an example of bundles recovered in a real subject, see the :ref:`ref_recobundles` page. The bundles used in the pictures below are the ones that were used when processing the `Tractoinferno <https://www.nature.com/articles/s41597-022-01833-1>`_ database. You can also discover similar bundles associated with the phantom from the `ISMRM 2015 Tractography Challenge <https://tractometer.org/ismrm2015/home/>`_. The differences between these simulated bundles and real anatomical ones were discussed in `Renauld et al, 2023 <https://www.nature.com/articles/s41598-023-28560-w>`_.


- AC:
- AF: Arcuate fasciculus.
- CC: Corpus callosum.
- CG: Cingulum.
- FAT:
- FPT:
- FX: Fornix
- ICP:
- IFOF:
- ILF:
- MCP:
- MdLF:
- OR, or OR_ML: Optic radiation (with Meyer's loop)
- PC
- POPT:
- PYT:
- SCP:
- SLF:
- UF:

The corpus callosum is probably the easiest bundle to recognize from a raw diffusion / tensor / fODF image because of its strong anisotropy. It is a good choice of bundle to assess that the data was read correctly during processing.

It is often divided into sub-sections during automatic segmentation, because it is a very large bundle covering most of the brain. Below, we can see that when zooming in the frontal section of the CC, near the mid-hemisphere, the FA is a bright white (strong anisotropy), and the tensors' main peak show a clear shape of "U".

|picCC1| |picCC2|

.. |picCC1| image:: /images/bundles/CC.png
   :width: 55%

.. |picCC2| image:: /images/bundles/CC_peaks.png
   :width: 40%

Other bundles are shown below:

|pic1| |pic2|

|pic3| |pic4|

|pic5| |pic6|

.. image:: /images/bundles/FAT_CC2.png
   :width: 45%
   :align: center


.. |pic1| image:: /images/bundles/UF_ILF_Fornix_PC_AC.png
   :width: 45%

.. |pic2| image:: /images/bundles/OR_IFOF_Cg.png
   :width: 48%

.. |pic3| image:: /images/bundles/MdLF_ILF.png
   :width: 45%

.. |pic4| image:: /images/bundles/MdLF_OR_MCP.png
   :width: 45%

.. |pic5| image:: /images/bundles/AF_SLF_SCP.png
   :width: 45%

.. |pic6| image:: /images/bundles/POPT_PYT_FPT_ICP.png
   :width: 45%
