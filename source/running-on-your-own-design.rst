Running On Your Own Design
===========================

Design files (verilog) are stored in a Git repository. In order to prepare your design to be run on OpenROAD flow,
follow the below steps:

1. Fork the `template repository`_ to your own GitHub account.
2. Rename the repo to the name of your design
3. Upload your design files in the design folder.
4. Edit the `openroad-flow.yml`. Comments in the file will help you follow the steps.
5. Go to https://flow.theopenroadproject.org. After logging in (or creating an account for the first time), click on the *My Designs* tab on the left. Then, click `Import Design` and enter the name of the design and the GitHub repository link.
6. Run the flow by clicking on `Run on latest version`.


What is openroad-flow.yml file?
-------------------------------

The `openroad-flow.yml` file tells OpenROAD cloud runners what configurations and parameters to use,
given the input design. For example, what software packages to use and what libraries to build for.


Example
-------

To see an example of a pre-configured repository, have a look at the `RISCV design`_ repository (which is the example we used in the Getting Started section).


.. _`template repository`: https://github.com/The-OpenROAD-Project/openroad-template-design
.. _`RISCV design`: https://github.com/The-OpenROAD-Project/cloud-flow-example-riscv