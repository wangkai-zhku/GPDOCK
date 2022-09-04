# GPDOCK
an effective tool for the docking of metalloproteins


The file contains all instructions for running GPDOCK
These two programs are suitable for the docking of single-metalloproteins and multi-metalloproteins. 

Platform: Linux
=======

Prepare input files:

Protein struture: (.pdb) 
********Three points to note:
1. remove other redundant molecules or metal ions, except the target protein and metal ion in their pocket
2. Please change the atomic type of calcium ion in the PDB file from CA or Ca to C0 in order to distinguish it from the backbone carbon atom of amino acid (CA).
3. Please change the atomic type of cadmium ion in the PDB file from CD or Cd to CAD in order to distinguish it from the sidechain carbon atom of amino acid (CD).

Ligand struture: (.mol2)
Obtaining the 3D structure of small molecules 
or processing 2D structure by other software to obtain 3D structure.

=======

Command-line:
if only one metal ion in the docking pocket:

./gpdock -PRO input.pdb  -LIG input.mol2 -ION MMM -HOH NNN

MMM stands for different metal ions.  1: Zn2+; 2: C02+ (calcium); 3: Mg2+; 4: Mn2+; 5: Fe2+; 6: Fe3+; 7: Cu2+; 8: Co2+; 9: CAD2+ (cadmium); 10: Ni2+.
NNN represents whether to dock water molecules.

        If you don't have to dock water molecules, you can do it in one of two forms:
       ./gpdock -PRO input.pdb  -LIG input.mol2 -ION MMM -HOH 0
        or
       ./gpdock -PRO input.pdb  -LIG input.mol2 -ION MMM 

        If you want to dock 1 water molecule:
       ./gpdock -PRO input.pdb  -LIG input.mol2 -ION MMM -HOH 1
      please note that there are two docking results, a result file with a water molecule involved and a result file with no water molecule involved

        If you want to dock 2 water molecule:
       ./gpdock -PRO input.pdb  -LIG input.mol2 -ION MMM -HOH 2
       Three docking results will be obtained, including no water docking result file, 1 water docking result file and 2 water docking result file.

if more than 1 metal ions in the docking pocket:
 Please use the gpdock_multi_metal execution file:
 ./gpdock_multi_metal -PRO input.pdb  -LIG input.mol2 -ION MMM
MMM stands for different metal ions.  1: Zn2+; 2: C02+ (calcium); 3: Mg2+; 4: Mn2+; 5: Fe2+; 6: Fe3+; 7: Cu2+; 8: Co2+; 9: CAD2+ (cadmium); 10: Ni2+.
At this time, water molecular docking can only be connected to a certain metal ion, and it is impossible to realize water molecular docking of multiple metal ions at the same time.

Introduction of results files:
out.pdb： Summary file of all docking results
out_wat_1.pdb： Summary file of all docking results with 1 water molecules if "-HOH 1" is used.
out_wat_2.pdb:    Summary file of all docking results with 2 water molecules if "-HOH 2" is used.

This program outputs two temporary files:
temp.pdb: The point set corresponding to the docking area calculated by the grid point algorithm
temp1.pdb: The set of protein atoms in contact with the docking region

=======
=======

License
=======

Contact
=======
wangkai@zhku.edu.cn
