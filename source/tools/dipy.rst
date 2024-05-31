.. _ref_dipy:

.. role:: bash(code)
   :language: bash

Dipy
====

`Dipy <https://dipy.org/index.html>`_ is a diffusion MRI data analysis. It is similar to :ref:`ref_mrtrix`. One of Dipy's main authors and contributors, Eleftherios Garyfallidis, was a post-doc in our lab in 2014-2015. It offers many functions coded in python/cython that you can import as a library when analysing your data. It doesn't offer complete end-to-end scripts, but you can check their `official website <https://dipy.org/>`_'s tutorials for scripts examples. You can also check our videos tab in the Teams' General channel for a tutorial.

Dipy will be installed automatically when installing Scilpy. However, you might have to modify Dipy at some point in your research. If so, you will need to fork the Dipy `repository <https://github.com/dipy/dipy>`__ and clone it somewhere on your computer. If you want your modification to become a part of the official Dipy, you will have to set up your upstream remote (see :ref:`ref_git`) and do a pull request in Dipy.