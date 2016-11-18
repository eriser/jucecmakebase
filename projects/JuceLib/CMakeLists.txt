cmake_minimum_required(VERSION 3.6)

collect_juce_files(${CMAKE_CURRENT_SOURCE_DIR} JUCE_FILES)
source_group("JUCE Files" FILES ${JUCE_FILES})

set(HEADER_FILES
	"Source/Example.h")
source_group("Header Files" FILES ${HEADER_FILES})
	
set(SOURCE_FILES
	"Source/Example.cpp")
source_group("Source Files" FILES ${SOURCE_FILES})
	
add_library(JuceLib ${JUCE_FILES} ${HEADER_FILES} ${SOURCE_FILES})
target_link_libraries(JuceLib JUCE)

target_include_directories(JuceLib PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/Source)

