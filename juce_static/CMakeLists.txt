cmake_minimum_required(VERSION 3.6)

collect_juce_files(${CMAKE_CURRENT_SOURCE_DIR} JUCE_FILES)

if (APPLE)
	file(GLOB SOURCE_FILES "${PROJUCER_FILES_DIR}/JuceLibraryCode/*.mm")
else()
	file(GLOB SOURCE_FILES "${PROJUCER_FILES_DIR}/JuceLibraryCode/*.cpp")
endif()

add_library(JUCE ${JUCE_FILES} ${SOURCE_FILES})

if (APPLE)

	find_library(ACCELERATE_LIBRARY Accelerate)
	find_library(AUDIOTOOLBOX_LIBRARY AudioToolbox)
	find_library(CARBON_LIBRARY Carbon)
	find_library(COREAUDIO_LIBRARY CoreAudio)
	find_library(COREMIDI_LIBRARY CoreMIDI)
	find_library(DISCRECORDING_LIBRARY DiscRecording)
	find_library(IOKIT_LIBRARY IOKit)
	find_library(OPENGL_LIBRARY OpenGL)
	find_library(QTKIT_LIBRARY QTKit)
	find_library(QUARTZCORE_LIBRARY QuartzCore)
	find_library(QUICKTIME_LIBRARY QuickTime)
	find_library(WEBKIT_LIBRARY WebKit)

	target_link_libraries(JUCE 
		${ACCELERATE_LIBRARY}
		${AUDIOTOOLBOX_LIBRARY}
		${CARBON_LIBRARY}
		${COREAUDIO_LIBRARY}
		${COREMIDI_LIBRARY}
		${DISCRECORDING_LIBRARY}
		${IOKIT_LIBRARY}
		${OPENGL_LIBRARY}
		${QTKIT_LIBRARY}
		${QUARTZCORE_LIBRARY}
		${QUICKTIME_LIBRARY}
		${WEBKIT_LIBRARY})

endif()

target_include_directories(JUCE PUBLIC ${CMAKE_SOURCE_DIR}/lib/juce/modules)