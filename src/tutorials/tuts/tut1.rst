############################################################## 
Tutorial 1: Molecular geometry optimization at the DFT level
############################################################## 

This is a very simple  tutorial  to get acquainted with electronic structure calculations using FLOSIC. This tutorial will explain how to run 
FLOSIC for molecular geometry optimizations using DFT. 

************************************
Setting Up Input Structure
************************************

The **CLUSTER** file is the main input file of FLOSIC. It contains the minimal information to set up a calculation. For this tutorial, we will use 
a CH4 molecule, which uses a **CLUSTER** file like the one shown below:

.. literalinclude:: input_data/CLUSTER.CH4
    :linenos:

We will now describe the input structure of this file.


The first line is :code:`GGA-PBE*GGA-PBE`. It means that the exchange-correlation interactions in the systems are modeled within the generalized 
gradient approximation (GGA) using the Perdew-Burke-Ernzerhof (PBE) parametrization. This is the default functional used in NRLMOL. A few other 
:ref:`functionals<Exchange correlation functionals>` are also available.

The second line is :code:`NONE`. It refers to point group symmetry of the molecule. For the purposes of the tutorial, we will not enforce symmetry. 
If you would like to use symmetry, a symmetry (TD,OH, etc.) can be selected in place of :code:`NONE`. In these cases, the code will create a **GRPMAT**
file containing the appropriate symmetry operations (each represented by a 3x3 matrix).  If you would like to use symmetry operations 
directly from an existing **GRPMAT** file, replace :code:`NONE` with :code:`GRP`. 

The third line contains :code:`5`. It specifies the number of inequivalent atoms in the calculation. We're running a CH4 calculation, so the number 
of atoms is 5 (1 C and 4 H). The following lines contain the cartesian positions of the atoms in atomic units (A.U.), followed by number of 
electrons of each  atom (e.g. 6 for Carbon). The string :code:`ALL` means include all (i.e. 6 in this case) electrons into the calculation.
The next 4 lines are the hydrogen atoms, which follow the same format.

The ninth line in the example file has two fields: net charge and net spin. The first field is :code:`0.0` which means to perform the calculation for
the neutral molecule. If the first field was  :code:`1`,  then the calculations would be performed for a cation of CH4. The next field which is also 
:code:`0.0` in this example corresponds to the number of unpaired electrons in the system, or the net spin in multiples of :math:`\frac{\hbar}{2}`. CH4 
is a closed shell system, so it has no unpaired electrons. Lines after the Charge and Spin fields are ignored.

************************************
Running the Calculation
************************************

Now, create an empty directory and run the :code:`nrlmol_exe` executable inside of it. Multiple default files will be 
created:

- AVRGDAT
- CLUSTER
- GEOCNVRG
- NRLMOL_INPUT.DAT
- PARASAV
- :ref:`RUNS`
- SPNORB

Copy the input from this example into the **CLUSTER**, replacing the default input. Run the calculation for CH4 and redirect output into some log file: 

.. code-block:: bash

    ${PATH_TO_FLOSIC}/nrlmol_exe &>> log &

.. note::
    You can call your log file whatever you want. The final ampersand (&) is to run the program in the background.

Open the **GEOCNVRG** file, you should see the following:

.. literalinclude:: input_data/GEOCONVRG.CH4

A new atomic geometry will be appended to the **SYMBOL** file; this file is created from the data in **CLUSTER**. The new geometry is created by 
a gradient optimization routine (either LBFGS or CONJUGATE-GRADIENT). The file **FRCOUT.G0** contains the atomic forces and coordiantes of the previous 
atomic geometry. Running the code again will carry out a calculation at the updated molecular geometry and a new total energy and new atomic forces will 
be computed. A new update of the atomic coordinates will also be written into SYMBOL. Repeating this process several times will result in a local minimum energy 
geometry to be reached. This happens when the maximum force falls below the criterion set in **GEOCNVRG**.
