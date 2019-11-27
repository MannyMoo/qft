################################################################################
# Package: QFT
################################################################################
gaudi_subdir(QFT v0r1)

gaudi_depends_on_subdirs(
	GaudiConfUtils
	AnalysisUtils)

find_package(PythonLibs)
find_package(Boost COMPONENTS program_options REQUIRED)
find_package(ROOT COMPONENTS Core RIO Hist Graf Graf3d Postscript Gpad
                             RooFit RooFitCore Tree MathCore Foam Physics
                             Proof ProofBench ProofDraw ProofPlayer)

gaudi_install_python_modules()

#gaudi_add_test(QMTest QMTEST)

# If you want to build and link C++ libraries, uncomment the below.
# Make sure the dict/*.h and dict/*.xml files exist.

# override the genreflex call to wrap it in the right environment
# set(ROOT_genreflex_CMD ${env_cmd} --xml ${env_xml} ${ROOT_genreflex_CMD})

include_directories(SYSTEM ${Boost_INCLUDE_DIRS} ${ROOT_INCLUDE_DIRS})
# gaudi_add_dictionary(QFT
#                      dict/QFTDict.h dict/QFTDict.xml
#                      SPLIT_CLASSDEF)

# Uncomment whichever source files you have.
gaudi_add_library(QFTLib
                  src/*/*.C
                  src/*/*.tcc
                  PUBLIC_HEADERS QFT
                  INCLUDE_DIRS Boost ROOT
                  LINK_LIBRARIES Boost ROOT)

# # ensure that genreflex is not called twice (in parallel builds)
# add_dependencies(QFTLib QFTGen)


# This can be used to build a C++ executable and add it to PATH
#gaudi_add_executable(MyExecutable src/MyExecutable.cpp LINK_LIBRARIES Boost ROOT DaVinciKernelLib QFTLib)
