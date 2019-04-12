# powersl
How to build the shared library:
```
1. install ccmake:
	sudo apt-get install cmake-curses-gui
2. install g++ if it does not exist:
	sudo apt-get install g++
3. install gfortran if it does not exist:
	sudo apt-get install gfortran
4. Install mpi using apt-get
	sudo apt-get install mpich
5. Install fblaslapack:
	sudo apt-get install libblas-dev
	sudo apt-get install liblapack-dev
4. Get petsc 3.10.3 from 
	https://github.com/petsc/petsc/releases/tag/v3.10.3
5. Untar or unzip it into a location available for the user which will be executing the GO competition scripts:
	tar -xvf petsc-3.10.3.tar.gz
	cp -r petsc-3.10.3 <target location available to the user>
5. Configure petsc for building it. This will take some time.
	cd petsc-3.10.3;
	./configure PETSC_ARCH=linux-gnu-c-debug --with-cc=mpicc --with-cxx=mpicxx --with-fc=0
6. For the next step you need to setup 2 environment variables PETSC_DIR and PETSC_ARCH that you need to setup in your ~/.bashrc but we are only going to import them for this session.
	export PETSC_DIR=<the cloned petsc directory eg /home/nishith/petsc_3_10_3_goparots>
	export PETSC_ARCH=linux-gnu-c-debug
If you are in the correct directory you can also run
	PETSC_DIR=$PWD
Note that you might have to use the setenv command depending upon the shell you are using. My instructions are for bash.
Note that these two environment variables are required for building the shared library.
7. This step might take a little bit of time. Make petsc:
	make PETSC_DIR=<the full cloned petsc dir path> PETSC_ARCH=linux-gnu-c-debug all
This will also run some test examples to verify the correct installation.
8. Check if the libraries are working:
	make PETSC_DIR=<the full cloned petsc dir path> PETSC_ARCH=linux-gnu-c-debug check
If this step runs successfully PETSc is ready for use.
```

Building the shared library:
```
1. Clone the shared library project from git into a location available for the user executing the GO competition scripts:
	git clone https://github.com/ntirpankar/powersl.git
2. Create a build directory in the clone and navigate to the build directoty:
	mkdir build;
	cd build
3. Generate a makefile:
	cmake ..
4. Make the project to generate the shared library files:
	make
5. Ensure that the shared library libpowersl.so.1 and the symlink libpowersl.so are created in the directory.
6. Make sure that the newly generated libraries are available on the LD_LIBRARY_PATH for the application to use
	export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:$PWD
Note that this shared library path will be required by the user running the GO competition scripts.
```
