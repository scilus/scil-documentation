Scilpy coding standards
============================

Thanks to JC for the coding tricks.

Here are the scilpy standards in python. See the General python coding tricks page for more tricks on how we use python. For C++, use the following link: https://github.com/scilus/fibernavigator/wiki/Coding-standard. Note that some scripts are coded in cython (.pyx) but if you're using it, you're probably already an experienced user of scilpy so we won't describe cython here.

**Main scilpy library**

    - We separate our library into these categories: image, io,	preprocessing, reconst, segment, tracking, tractanalysis, utils, viz. In each folder, we generally place the smaller functions (a few lines) in utils.py and the main functions in separate files. The most complicated functions are generally encapsulated in a class for easier management (ex: RecobundlesX, VotingScheme, TrackOrientationDensityImaging).

**Scripts**

    - Our scripts usually contain the following functions:

        .. code-block:: python

            #!/usr/bin/env python
            # -*- coding: utf-8 -*-

            """
            Description of this script.
            The description of the script should be almost at the beginning, between triple quotes.
            It can be referred in the ArgumentParser constructor as __doc__.
            """

            def _build_arg_parser():
                p = argparse.ArgumentParser(
                    description=__doc__, formatter_class=argparse.RawTextHelpFormatter)
                ...

            def main():
                ...

            if __name__ == "__main__":
                main()


    - More information on how to code _build_arg_parser:

        .. code-block:: python

            # GOOD:
            p.add_argument('input_path',
                help='Explanation')                       # try to have the “help” section on a separate line.

            # NOT GOOD:
            p.add_argument('input_path', action="store",  # store is already the action by default. Not needed.
                help='The path to the dMRI input.')
            p.add_argument('input_path', type="str",      # str is already the type by default. Not needed.
                help='The path to the dMRI input.')

        .. code-block:: python

            # GOOD:
            p.add_argument(
                '--use_some_option', action='store_true', # optional arguments with more than one letter should use the “--” syntax.
                help='If set, we will do some option.')

            # NOT GOOD:
            p.add_argument(
                '--use_some_option', action='store_true', default=False,  # False is already the default with action "store_true". Not needed.
                help='If set, we will do some option.')


        - Some args are very common and have been defined in scilpy.io.utils to make sure that we all take the same explanation text. You may import these functions and call them directly in _build_arg_parser. Ex:

        .. code-block:: python


            add_verbose_arg(p)    # The -v arg.
            add_overwrite_arg(p)  # The -f arg.


**UX and usability**

We aim to provide scripts that are relatively clear and easy to use for non technical users. With this goal in mind:

    - Add basic file existence checks for paths and directories specified as arguments to a script. Telling the user with a “parser.error” is clearer than a nibabel file not found error.
    - When possible, use the following methods scilpy.io.utils assert_inputs_exist, assert_outputs_exists
    - Use try / catch blocks for blocks that are possible to handle and may be created by realistic use cases. Else, let the exception bubble up, and then deal with it when it happens.


**Printing and logging**

    - Instead of using naked prints in the scripts, use Python’s logging facilities. Helps when running lots of scripts, to direct outputs to various logging mechanisms.