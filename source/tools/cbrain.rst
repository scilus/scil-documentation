.. _ref_cbrain:

CBRAIN
======

.. role:: bash(code)
   :language: bash


CBRAIN is a collaborative, web-enabled grid platform built to facilitate research on large, distributed datasets by managing user access, transfer, caching and provenance for distributed data, as well as mediating interactions with high-performance computing centres (HPCs). Here is the documentation: https://github.com/aces/cbrain/wiki. Also check our videos tab in the Teams' General channel for an introduction to CBRAIN.

You can ask for an account by following this link https://portal.cbrain.mcgill.ca/. Indicate that you are from Maxime Descoteaux's SCIL lab. Once you've got an account please send a message on the Teams channel `ComputeCanada` to be added to the SCIL group and get access to the data provider on beluga.

Tutorial
--------

In short, CBrain regroups your files into projects. You can then select as many files as you want and launch a set of predefined tasks such as FreeSurfer or Civet.

Uploading your data
*******************

In both cases, transfer your files on the "mainstore". Cbrain can store files in various servers. You will also see below that you can launch tasks on various servers. "Mainstore" allows your files to be accessible on any server, no mather where you launch your task.

If you only have a few files, you can upload them directly through the portal (once connected: click on MyAccount and follow instructions.)

This technique is not super efficient, so you might prefer transferring for many files by sftp (host: ace-cbrain-1.cbrain.mcgill.ca) with your username and password. Do not create sub-folders on cbrain, just transfer your nifti files, for instance. Then, in the portal, under resources, select data_providers. You should see your sftp connection. Select the data and click on "register files, move to mainstore".

Launching tasks
***************

Select your files (either by viewing them in the project tab or in your home tab) and select launch. You can see, amongst others, recon-all (i.e. FreeSurfer) and civet. You have to choose the server to use. Anyone can work (as long as your data is in the "mainstore"), just take the ones that shows the less delay (a good delay is usually ~5 minutes max. But delay of many hours sometimes happen). Other options depend on the task you are running, see the respective tool's page.

At first, you might see that the task will be pending, and then setting up. If it fails, you can try to click on the task to see if an error message was sent. Sometimes, the issue is on CBrain's side, and just launching the same task again can solve the problem.

Downloading processed data
**************************

You can again download files directly from the portal or send them by sftp or to our beluga server. Note that we suggest that when launching your tasks, you send the output to the mainstore and then, transfer your files, rather than saving directly the results on sftp. It can reduce the chance of encountering an unexpectedd error.