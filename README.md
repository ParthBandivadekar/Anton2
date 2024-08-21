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
2. ```viparr -f aa.amber.ff19SB -f water.opc system.dms system.ff.dms``` will add the forcefield and water model you have selected
3. ```viparr-build-constraints system.ff.dms -o system.final.dms``` will constrain the hydrogens
4. ```dms-validate system.final.dms``` will make sure everything was done correctly
5. ```dms-info system.final.dms``` to confirm the structure, bonds, ff and topology

<b> Starting the simulation </b>
1. Following the guide on making the correct DMS file we are following [this guide](https://wiki.psc.edu/twiki/view/Anton/a2docs/proj/desres/doc/build/html/walkthrough.html#assumptions)
2. We use [base.ark](https://github.com/ParthBandivadekar/Anton2/blob/48eddec211454fdb06920cccace2ac9ece4f739e/base.ark) to set up the simulation parameters.
3. The default settings are set for a NPT simulation with 2400 picoseconds of simulation time. 

