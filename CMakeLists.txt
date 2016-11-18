cmake_minimum_required(VERSION 3.6)

# Import functions
include(cmakemodules/GetGitRevisionDescription.cmake)
include(cmakemodules/CollectJuceFiles.cmake)

# Get version information
git_describe(VERSION --tags --dirty=-dirty GITVERSION_SUCCESS)

if (GITVERSION_SUCCESS)

	message("Git Tag Version: ${VERSION}")

	string(REGEX REPLACE "^v([0-9]+)\\..*" "\\1" VERSION_MAJOR "${VERSION}")
	string(REGEX REPLACE "^v[0-9]+\\.([0-9]+).*" "\\1" VERSION_MINOR "${VERSION}")
	string(REGEX REPLACE "^v[0-9]+\\.[0-9]+\\.([0-9]+).*" "\\1" VERSION_BUGFIX "${VERSION}")
	string(REGEX REPLACE "^v[0-9]+\\.[0-9]+\\.[0-9]+(.*)" "\\1" VERSION_SHA1 "${VERSION}")

else()

	message("Failed to get version from Git")
	
	set(VERSION_MAJOR 0)
	set(VERSION_MINOR 0)
	set(VERSION_BUGFIX 0)
	set(VERSION_SHA1 0)

endif()

set(VERSION_SHORT "${VERSION_MAJOR}.${VERSION_MINOR}.${VERSION_BUGFIX}")

project(JuceCMakeBase)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -D_NDEBUG")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -D_DEBUG")

if(MSVC)
	set(CMAKE_SHARED_LINKER_FLAGS_DEBUG ${CMAKE_SHARED_LINKER_FLAGS_DEBUG} " /NODEFAULTLIB:\"libcmt.lib\" /NODEFAULTLIB:\"msvcrt.lib\"")
	set(CMAKE_EXE_LINKER_FLAGS_DEBUG ${CMAKE_EXE_LINKER_FLAGS_DEBUG} " /NODEFAULTLIB:\"libcmt.lib\" /NODEFAULTLIB:\"msvcrt.lib\"")
	set(CMAKE_EXE_LINKER_FLAGS ${CMAKE_EXE_LINKER_FLAGS} " /SUBSYSTEM:WINDOWS")
endif()

# Add JUCE to build
add_subdirectory(juce_static)

# Add projects
add_subdirectory(projects)

