# GPDOCK  Operations Manual
an effective tool for the docking of metalloproteins


The file contains all instructions for running GPDOCK
These two programs are suitable for the docking of single-metalloproteins and multi-metalloproteins. 

Platform: Linux

=============
Prepare input files:

Protein struture: (.pdb) 
********Three points to note:
1. remove other redundant molecules or metal ions, except the target protein and metal ion in their pocket
2. Please change the atomic type of calcium ion in the PDB file from CA or Ca to C0 in order to distinguish it from the backbone carbon atom of amino acid (CA).
3. Please change the atomic type of cadmium ion in the PDB file from CD or Cd to CAD in order to distinguish it from the sidechain carbon atom of amino acid (CD).

Ligand struture: (.mol2)
Obtaining the 3D structure of small molecules 
or processing 2D structure by other software to obtain 3D structure.
For example：
One of the method to obtain 3D structure through SMILES file by openbabel, the following steps can be implemented
1. To obtain SMILES files, such as aaa.smi
2. To obtain 3D structure of this ligand and the coordinates are writen in aaa.mol2
obabel -i smi aaa.smi -O aaa.mol2 --gen3D -d
3. To obtain more lower energy conformer
obconformer 200 100 aaa.mol2 > ligand.mol2
 Or you can get more low-energy conformation through the confab module of openbabel

NOTE：
If the docking results cannot be obtained by using all-atom of ligand,
 the following procedure can remove the hydrogen atoms in the ligands 
to reduce the screening of docking results by steric hindrance

./gb_heavy -LIG input.mol2

This operation will obtain the file named heavy_lig.mol2, which contains the heavy atom information of  input.mol2.
=========================

=========================
Command-line:
if only one metal ion in the docking pocket:

./gpdock -PRO input.pdb  -LIG input.mol2 -ION MMM -HOH NNN

MMM is a number between 1 and 10, each of which represents a metal ion:
1: Zn2+; 2: C02+ (calcium); 3: Mg2+; 4: Mn2+; 5: Fe2+; 6: Fe3+; 7: Cu2+; 8: Co2+; 9: CAD2+ (cadmium); 10: Ni2+.

NNN is a number between 0 and 2, each of which represents the number of water molecules:

If out.pdb is empty which means there is no proper docking pose,
then the hydrogen atom in the ligand can be removed by gb_heavy
and  repeat the docking process by heavy_lig.mol2

./gb_heavy -LIG input.mol2

For examples: 
 for Zinc metalloproteins:
        If you don't have to dock water molecules, you can do it in one of two forms:
       ./gpdock -PRO input.pdb  -LIG input.mol2 -ION 1 -HOH 0
        or
       ./gpdock -PRO input.pdb  -LIG input.mol2 -ION 1 

       if you want to dock the heavy atoms of the ligand:
       ./gb_heavy -LIG input.mol2
       ./gpdock -PRO input.pdb  -LIG heavy_lig.mol2 -ION 1 

        If you want to dock 1 water molecule:
       ./gpdock -PRO input.pdb  -LIG input.mol2 -ION 1 -HOH 1
      please note that there are two docking results, a result file with a water molecule involved and a result file with no water molecule involved

        If you want to dock 2 water molecule:
       ./gpdock -PRO input.pdb  -LIG input.mol2 -ION 1 -HOH 2
       Three docking results will be obtained, including no water docking result file, 1 water docking result file and 2 water docking result file.

if more than 1 metal ions in the docking pocket:
 Please use the gpdock_multi_metal execution file:
 ./gpdock_multi_metal -PRO input.pdb  -LIG input.mol2 -ION MMM

MMM is a number between 1 and 10, each of which represents a metal ion: 
1: Zn2+; 2: C02+ (calcium); 3: Mg2+; 4: Mn2+; 5: Fe2+; 6: Fe3+; 7: Cu2+; 8: Co2+; 9: CAD2+ (cadmium); 10: Ni2+.

At this time, water molecular docking can only be connected to a certain metal ion, and it is impossible to realize water molecular docking of multiple metal ions at the same time.

Introduction of results files:
out.pdb： Summary file of all docking results
out_wat_1.pdb： Summary file of all docking results with 1 water molecules if "-HOH 1" is used.
out_wat_2.pdb:    Summary file of all docking results with 2 water molecules if "-HOH 2" is used.

This program outputs two temporary files:
temp.pdb: The point set corresponding to the docking area calculated by the grid point algorithm
temp1.pdb: The set of protein atoms in contact with the docking region

=======

examples：
Some docking structure files include 4 folders，
and each folder contains the original metalloprotein file,
the initial structure of the ligand and the output file obtained docked by GPDOCK.

1. PART_MM：
The examples of multi-metalloproteins.

2.PART_SM：
The examples of single-metalloproteins.

3.PART_SW：
The examples of single-metalloproteins which contains water molecules engaged in the coordination of metal ions.

4. SMILE-DOCK：
The examples of ligand which structure converted by SMILES.


The format and docking results of the document are available for reference and testing.
All  original files and docking results  can be obtained through the mailbox: wangkai@zhku.edu.cn.
=======

License
=======

Contact
=======
wangkai@zhku.edu.cn