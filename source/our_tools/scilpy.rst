.. _ref_scilpy:

SCILPY
======

.. role:: bash(code)
   :language: bash

Scilpy is closely related to :ref:`ref_dipy`: it follows the same organization. But it also contains work that has been developped by our lab and that is not included yet into Dipy. We have a `public version <https://github.com/scilus/scilpy>`_ of Scilpy on Github, with work that has been tested and that we want to share with the community, and a private version on Bitbucket (you have to ask for access) with our work that is either not tested, still being developped or not converted into python 3.

For each script, you can use the -h option for explanations on how to use it. Ex:

    .. code-block:: bash

        scil_compute_fodf.py -h

If you don't know the name of a script, you may look for all scripts matching some keywords with:

    .. code-block:: bash

        scil_find_script.py keyword


Installing scilpy
    - Users: you can follow the instructions on the Github page. Clone the repository, install the requirements and install through the setup.py as explained.

    - Developpers: instead, you should try :bash:`python setup.py develop`

    .. warning::

        Before installing anything, please read the :ref:`ref_environments_page` page!