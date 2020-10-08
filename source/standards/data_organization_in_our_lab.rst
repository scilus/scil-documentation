.. _ref_organization_standards:

Our lab's organization standards
================================

Here are some rules and good habits to follow in our lab.

- Please keep all folders names in lowercase (this is true when coding, but also generally everywhere, like in BrainData for instance), and prefer the use of underscores. Ex: my_project instead of MyProject.

- DO NOT DUPLICATE DATA.

- If you want to start a project with...

    - raw data from...

        - an existing databases: You should find the raw data you are looking for in BrainData/databases. If you can't find your data, don't hesitate to ask in the slack channel #help_me_find_data.

        - open databases: If you find openly available data on Internet and want to save it in our databases, please coordinate with Arnaud to decide the best organization.

        - a new database: If you plan of acquiring your own data, please talk with Arnaud.

    - processed data from an existing database: other lab members may have already processed the data you want exactly the same way as you want. If you can't find your data, don't hesitate to ask in the slack channel #help_me_find_data. There are two main places you should check:

        - Check in BrainData/databases/(your database)/derivatives for data that we have organized officially using the BIDS format (see `:ref:`ref_heavy_storage`) for more information).

        - Check in BrainData/processedData/(your database) for other processed data.

- If you want to save a finished project, you can go in BrainData/processedData and create a folder **with a significative name**. Please add information on how your data was processed. Once your project is officially complete, please coordinate with Arnaud to see how to add it to BrainData/databases/(your database)/derivatives.
