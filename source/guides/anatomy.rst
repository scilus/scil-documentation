.. _ref_anat:

Brain anatomy
=============

Lobes, sulcus, gyri and more
****************************

Consult the introduction to anatomy given by our anatomist collaborator Laurent Petit here: `BrainData/references/NeuroAnatomy/Petit_NeuroAnatomy_SCIL_2019_01.pptx`


A few famous bundles
********************

The anatomical description of bundles (or tract, fasciculus, tractus, etc.) is a subject of study that is still evolving, and that is even sometimes source of debates. Experts in computer science, biology, histology, medicine, etc., all have a different approach to discovering the brain organization. Still, in our field, the most common names come back repeatedly. Most of us did not study in biology or anatomy. We come from physics, computer science, mathematics. But you'll probably learn many bundles' names and position, just by seeing pictures. Here are some pictures of the bundles most commonly used in the lab.

    - *Anatomical description*: It is possible to find in the literature the "true" definition of each bundle (ex: starting point, ending point, division into sub-bundles, and so no). At this level, the word "bundle" does not exist, as it refers to the action of putting together a group of **streamlines**, on the computer. Rather, tracts (or fasciculi) refer to the trajectory of **nerve fibers** through the brain. You may read for instance `Schahmann et al, 2008 <https://nyaspubs.onlinelibrary.wiley.com/doi/pdf/10.1196/annals.1444.017>`_ for a description of many fiber pathways.

    - *Atlas bundles as reference*: After the theoretical description, the next best thing is to consult atlases. They are bundles that you can download and see, generally in a template space such as MNI. They are often created by using tractography in a population of subjects. The streamlines present in most subjects and that are consistant with the definition of the bundle in the literature are kept. You may find an example `here, Radwan et al (2022) <https://www.sciencedirect.com/science/article/pii/S1053811922001586>`_. These reference files, however, represent an average result and could be a little different than the "real" anatomical description.

    - *Bundles recovered through tractography in one subject*: You will discover that anatomy varies a lot throughout subjects. Combined to the fact that tractography is far from perfect, the bundles resulting from tractography in one single subject could be very different from the expected result (see for instance Figure 7 in `Bürgel et al 2006 <https://www.sciencedirect.com/science/article/pii/S105381190500649X>`_ on the inter-subject variability). To see an example of bundles recovered in a real subject, see the :ref:`ref_recobundles` page.

    - *Simulated bundles*: Finally, you can also explore the bundles associated with the phantom from the `ISMRM 2015 Tractography Challenge <https://tractometer.org/ismrm2015/home/>`_. The differences between these simulated bundles and real anatomical ones were discussed in `Renauld et al, 2023 <https://www.nature.com/articles/s41598-023-28560-w>`_. In this case, the bundles are not entirely simulated; they were created by tracking from real subjects with deterministic, bundle-wise parameters. However, the dwi accompanying the data is entirely simulated.

**Commissural fibers**: They connect the two hemispheres of the brain. They are mostly in a left-right orientation.

    - AC: Anterior commissure
    - CC: Corpus callosum
    - PC: Posterior commissure

**Projection fibers**: They connect the cortex with lower parts of the brain, such as the brainstem or cerebellum, or with the spinal cord. They are mostly in a z orientation (top-bottom).

    - FPT: Frontopontine Tract
    - OR, or OR_ML: Optic radiation (with Meyer's loop)
    - POPT: Parieto-occipital pontine tract
    - PYT: Pyramidal tract
    - FX: Fornix (it also contains commissural fibers)
    - SCP: Superior cerebellar peduncle
    - MCP: Middle cerebellar peduncle
    - ICP: Inferior cerebellar peduncle

**Association fibers**: They connect two cortex regions in a same hemisphere.
    - AF: Arcuate fasciculus.
    - CG: Cingulum.
    - FAT: Frontal aslant tract
    - IFOF: Inferior fronto-occipital fasciculus
    - ILF: Inferior longitudinal fasciculus
    - MdLF: Middle longitudinal fascicle
    - SLF: Superior longitudinal fasciculus
    - UF: Uncinate fasciculus


The corpus callosum is probably the easiest bundle to recognize from a raw diffusion / tensor / fODF image because of its strong anisotropy. It is a good choice of bundle to assess that the data was read correctly during processing.

It is often divided into sub-sections during automatic segmentation, because it is a very large bundle covering most of the brain. Below, we can see that when zooming in the frontal section of the CC, near the mid-hemisphere, the FA is a bright white (strong anisotropy), and the tensors' main peaks show a clear shape of "U".

|picCC1| |picCC2|

.. |picCC1| image:: /images/bundles/CC.png
   :width: 55%

.. |picCC2| image:: /images/bundles/CC_peaks.png
   :width: 40%

Below, we show pictures of the reference bundles used with Recobundles (here, the ones that were used when processing the `Tractoinferno <https://www.nature.com/articles/s41597-022-01833-1>`_ database). They are in MNI space.


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
