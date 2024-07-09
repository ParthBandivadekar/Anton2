# Anton2
Documentation to run MD simulations on Anton2

<b> #Converting files from Amber to Anton </b>
1. Prepare and run minimization, heating and relaxation steps for your system of interest. This guide will use Chignolin as an example protein.
2. Once the relaxation step is done we need to convert the file from cdf format to ascii format. Even thought rst7 starts as a Ascii format file the above steps save it as cdf.
3. Here's the cpptraj script to convert the files to the right format. [Link](Amb2Ant.cpptraj)
4. Using viparr on Anton 2 we now need to convert the files to the dms format.
5. First load the viparr module using
6.  ``` 
    garden load viparr/4.7.49c7/lib
    garden load viparr/4.7.49c7/bin
    garden load viparr/4.7.49c7/lib-python37```
7. Then use the command `viparr-convert-prmtop -c Eq.rst7 -o system.dms Chg.prmtop`
8. 
