General python coding tricks
============================

Here are tricks on how we like to use code in our lab. One possible text editor that works well is PyCharm.

**Basic principle**

    - Follow PEP8 as closely as possible. If you work in PyCharm, you can have PEP8 indications directly. Else, you can try in the terminal (see below) and check the comments. NOTE. This will be updated soon considering following message when using Pep8: *pep8 has been renamed to pycodestyle (GitHub issue #466) Use of the pep8 tool will be removed in a future release. Please install and use `pycodestyle` instead.*

        .. code-block:: bash

            pep8 my_script.py

    - The main point where we can deviate from PEP8 is on the line length: if breaking up the line to have 80 chars or less would make everything really unreadable, we can be flexible.

**Shebang lines**

    - Scripts should start with

        .. code-block:: python

            #!/usr/bin/env python
            # -*- coding: utf-8 -*-

**Imports**

    - Always use full imports, even if they come from a file in the same subdirectory.
    - For more information on imports, see here: https://www.python.org/dev/peps/pep-0008/#imports
    - Note that we usually rename numpy as np, nibabel as nib.

**Args in functions**

    - ARNAUD, JC, GUILLAUME? DO WE LIKE type hints?  (example below)

        .. code-block:: python

             def my_function(first_number: int):
             def my_function(first_number)

**Classes**

    - SOMETHING TO SAY?

