
cmake_minimum_required(VERSION 3.22)

project(SOLAR_TUNE VERSION 1.0.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include(FetchContent)

FetchContent_Declare(
    JUCE
    GIT_REPOSITORY https://github.com/juce-framework/JUCE.git
    GIT_TAG 8.0.10
)

FetchContent_MakeAvailable(JUCE)

juce_add_plugin(SOLAR_TUNE
    COMPANY_NAME "MUU MILL"
    PLUGIN_MANUFACTURER_CODE MuMi
    PLUGIN_CODE SoTu
    FORMATS VST3
    PRODUCT_NAME "SOLAR TUNE"
    IS_SYNTH FALSE
    NEEDS_MIDI_INPUT FALSE
    NEEDS_MIDI_OUTPUT FALSE
    IS_MIDI_EFFECT FALSE
    COPY_PLUGIN_AFTER_BUILD FALSE
)

target_sources(SOLAR_TUNE
    PRIVATE
        Source/PluginProcessor.cpp
        Source/PluginEditor.cpp
)

target_compile_definitions(SOLAR_TUNE
    PUBLIC
        JUCE_WEB_BROWSER=0
        JUCE_USE_CURL=0
)

target_link_libraries(SOLAR_TUNE
    PRIVATE
        juce::juce_audio_utils
        juce::juce_dsp
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_lto_flags
        juce::juce_recommended_warning_flags
)
