cmake_minimum_required(VERSION 3.15)

project(PERSISTENT_PROPERTY_CHECK VERSION 0.0.1)

add_subdirectory(dependencies)

juce_add_plugin(PersistentPropertyCheck
    PLUGIN_MANUFACTURER_CODE Juce               # A four-character manufacturer id with at least one upper-case character
    PLUGIN_CODE Dem0                            # A unique four-character plugin id with exactly one upper-case character
                                                # GarageBand 10.3 requires the first letter to be upper-case, and the remaining letters to be lower-case
    FORMATS AU VST3 Standalone                  # The formats to build. Other valid formats are: AAX Unity VST AU AUv3
    PRODUCT_NAME "Persistent Property Check")        # The name of the final executable, which can differ from the target name

# juce_generate_juce_header(AudioPluginExample)

target_sources(PersistentPropertyCheck
    PRIVATE
        source/PluginEditor.cpp
        source/PluginProcessor.cpp)

target_include_directories(PersistentPropertyCheck PRIVATE include)

target_compile_definitions(PersistentPropertyCheck
    PUBLIC
        # JUCE_WEB_BROWSER and JUCE_USE_CURL would be on by default, but you might not need them.
        JUCE_WEB_BROWSER=0  # If you remove this, add `NEEDS_WEB_BROWSER TRUE` to the `juce_add_plugin` call
        JUCE_USE_CURL=0     # If you remove this, add `NEEDS_CURL TRUE` to the `juce_add_plugin` call
        JUCE_VST3_CAN_REPLACE_VST2=0)

target_link_libraries(PersistentPropertyCheck
    PRIVATE
        # AudioPluginData           # If we'd created a binary data target, we'd link to it here
        juce::juce_audio_utils
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_lto_flags
        juce::juce_recommended_warning_flags)
