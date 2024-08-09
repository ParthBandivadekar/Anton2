# Anton2
Documentation to run MD simulations on Anton2
login: name@anton2.psc.edu

<b> #Converting files from Amber to Anton </b>
1. Prepare and run minimization, heating and relaxation steps for your system of interest. This guide will use Chignolin as an example protein.
2. Once the relaxation step is done we need to convert the file from cdf format to ascii format. Even thought rst7 starts as a Ascii format file the above steps save it as cdf.
3. Here's the cpptraj script to convert the files to the right format. [Link](Amb2Ant.cpptraj)
4. Using viparr on Anton 2 we now need to convert the files to the dms format.
5. First load the viparr and msys module using
6.  ``` 
    garden load msys/1.7.345c7/bin
    garden load viparr/4.7.49c7/lib
    garden load viparr/4.7.49c7/bin
    garden load viparr/4.7.49c7/lib-python37
    garden load viparr-ffpublic/1.0.10c7/data```
7. Then use the command `viparr-convert-prmtop -c Eq.rst7 -o system.dms Chg.prmtop`

<b> #Setting up the forcefields and dms file </b>
1. viparr --help will give you all the information related to the forcefields present in viparr
2. ```viparr -s water -f water.opc system.dms system.opc.dms``` will add the water model you have selected
3. ```viparr-build-constraints system.opc.dms -o system.final.dms``` will constrain the hydrogens
4. ```dms-validate system.final.dms``` will make sure everything was done correctly
5. ```dms-info system.final.dms``` to confirm the structure, bonds, ff and topology

<b> #Randomizing velocities for multiple simulations </b>
1. dms-thermalize
2. 

