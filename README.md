# JUCE CMake Base
Starter repo for a [JUCE](https://github.com/julianstorer/JUCE) library project built with CMake. 

## Justification

Whilst the Projucer provided with JUCE is useful, it makes it impossible to do multi-project builds. CMake provides a lot of flexibility in this area, however in order to maintain the advantages of the Projucer (JUCE module management, JUCE configuration, resource file binary data conversion, etc.), a method to integrate the generated output into the CMake build system is required. The CMake scripts in this repo provide this, and are designed around the idea of building JUCE as a static library and linking statically to multiple targets.

## Features
- Builds JUCE from submodule as static library. 
- Automatically re-saves .jucer projects at CMake configure time and links in generated files.
- Autoconfigures .jucer projects with CMake project name, and versioning information derived from git repo tags.

## Support
- Microsoft Visual Studio 2015
- XCode (macOS apps only)

## Contents

The repo contains 3 projects
- JUCE static library.
- Example static library linking to JUCE.
- Example application linking to both JUCE and the example static library.

## Requirements
- CMake 3.6+
- Git and the JUCE Projucer must be in the system path.
