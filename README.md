# IP-Sat model

This code (self-contained) calculate DGLAP-evolved IP-Sat dipole amplitude. Please cite the following paper if you use the code: 
A. H. Rezaeian, M. Siddikov, M. Van de Klundert, R. Venugopalan, Phys.Rev.D87:034002,2013 [arXiv:1212.2974]. 
The details of the computation can be found here: https://arxiv.org/abs/1212.2974
 

The package is self-contained and incorporates QCDNUM code (without quarks in evolution) for the DGLAP evolution. 
______________________________________
How to generate library (Brief instructions what you need to do): 
______________________________________

1) unpack IP-Sat.tar.gz 

tar -xvzf  IP-Sat.tar.gz
 
 Or just fork libColorDipole. 
 
2) cd to main directory "libColorDipole" and then do the following "make TEST_DIPOLE FC=gfortran", 
Note if you have f77 or g77 instead of gfortran, then in the above command replace FC=gfortran with FC=f77 or FC=g77. 

3) After the above step, you will generate all the libraries. Grab the files src/Test_Dipole.f and libraries/libColorDipole.a and copy them in any directory that you like, and compile them:
 
gfortran Test_Dipole.f libColorDipole.a -o run.exe

4) Now you can run: 
./run.exe
---------------------------------------
Note that in directory libraries/, files libColorDipole.so [dynamic] and libColorDipole.a [static].
If you do not know the difference, do not worry, most probably it means that you will need only static one: libColorDipole.a


In the test code in "src/Test_Dipole.f", you can see how to call dipole amplitude.  Instead of Test_dipole.f you can put your own code where you call subroutine dipole_amplitude(xBj, r, b). So in practice after steps 1-2, you are done, you will need only one file libraries/libColorDipole.a. Note also that you can run the code  with C++ or any other compiler. The only file that you need is libraries/libColorDipole.a 

------------------------------------
How to call the subroutine:
____________________________________
You need only to call the subroutine: dipole_amplitude(xBj, r, b, parameterSet). It gives 2*N(xBj,r,b) where N is the imaginary part of the dipole-proton scattering amplitude. The dipole cross-section is defined by integrating over b in 2-dimension, namely \int d2b  dipole_amplitude(xBj, r, b, parameterSet)=\int d2b 2*N(xBj,r,b) where 
xBj is Bjorken x;
r dipole size [1/GeV];
b impact-parameter[1/GeV];
parameterSet=1 corresponds to parameter-set with m_c=1.27 GeV; 
parameterSet=2 corresponds to parameter-set with m_c=1.4 GeV.
Note that for both sets the light quark masses are approximately equal to zero. We used the parameters given in table I of arXiv:1212.2974. 

Important note: In the code we generated the grid for 0.01<xBj<10^-14, if you use the code outside of this kinematics of xBj, you should get problem in your cross-section since dipole amplitude outside of this kinematic region is taken ZERO. Note also that the dipole amplitude parameters was obtained from a fit to combined HERA data in 0.01<xBj<10-7 and  0.75<Q^2(GeV)<650.  
-------------------------------------- 
