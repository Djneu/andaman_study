Parameters files for all runs used in the study: 
Flexural strike-slip basins
Derek Neuharth, Sascha Brune, Anne Glerum, Chris K. Morley, Xiaoping Yuan, Jean Braun

Model runs in the study used dealii 9.2.0.
The aspect version used for this study is found at: 
https://github.com/Djneu/aspect/tree/andaman_study

An additional plugin, written by Anne Glerum, is used for the LAB perturbation and included in the plugin_files folder.


To install ASPECT with FastScape.

1. Clone the ASPECT branch and a fastscape version.
	git clone -b andaman_study https://github.com/Djneu/aspect
	git clone https://github.com/fastscape-lem/fastscapelib-fortran

2. Copy the Named_VTK.f90 file from the ASPECT directory into the FastScape source directory
	cp aspect/Named_VTK.f90 fastscapelib-fortran/src/

3. In the fastscape folder, add the following line to CMakeLists.
	set(FASTSCAPELIB_SRC_FILES
           ${FASTSCAPELIB_SRC_DIR}/Named_VTK.f90
	   )

4. Create a build directory for fastscape and compile it with an added flag for creating a shared library.
	cmake -DBUILD_FASTSCAPELIB_SHARED=ON /path/to/fastscapemake
	make


5. Compile ASPECT with a flag FASTSCAPE_DIR pointing to the fastscape build folder with the shared library
	cmake -DFASTSCAPE_DIR=/path/to/fastscape/build -DDEAL_II_DIR=/path/to/dealii -DCMAKE_BUILD_TYPE=Release /path/to/aspect
	make

	*note* ASPECT will still compile and install even if a FastScape version is not found. During cmake, it should state whether or not
	       FastScape was found, if it was not you'll need to rerun cmake.




