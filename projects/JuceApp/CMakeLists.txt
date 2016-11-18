cmake_minimum_required(VERSION 3.6)

project(JuceApp)

collect_juce_files(${CMAKE_CURRENT_SOURCE_DIR} JUCE_FILES)
source_group("JUCE Files" FILES ${JUCE_FILES})

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/Source)

set(HEADER_FILES 
	"Source/MainComponent.h")
source_group("Header Files" FILES ${HEADER_FILES})

set(SOURCE_FILES
	"Source/Main.cpp"
	"Source/MainComponent.cpp")
source_group("Source Files" FILES ${SOURCE_FILES})

if(APPLE)
	add_executable(JuceApp MACOSX_BUNDLE ${JUCE_FILES} ${HEADER_FILES} ${SOURCE_FILES})
	set_target_properties(JuceApp PROPERTIES MACOSX_BUNDLE_INFO_PLIST 
		${CMAKE_CURRENT_SOURCE_DIR}/Builds/MacOSX/Info-App.plist)

	find_library(APPKIT_LIBRARY AppKit)
	target_link_libraries(JuceApp ${APPKIT_LIBRARY})
	
elseif(MSVC)

	add_executable(JuceApp ${JUCE_FILES} ${HEADER_FILES} ${SOURCE_FILES})
	
else()

	message(FATAL_ERROR "Unsupported compiler")
	
endif()

target_link_libraries(JuceApp JUCE)
target_link_libraries(JuceApp JuceLib)

