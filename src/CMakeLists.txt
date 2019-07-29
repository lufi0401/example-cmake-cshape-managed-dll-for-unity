cmake_minimum_required(VERSION 3.8.2)
project("VSTest1" VERSION 0.1.0 LANGUAGES CSharp)

# Add library
add_library(VSTest1 SHARED VSTest1.cs)

# Set .NET libraries
set_property(TARGET VSTest1 PROPERTY VS_DOTNET_REFERENCES
    "Microsoft.CSharp"
    "System"
)

# Set external library
set_property(TARGET VSTest1 PROPERTY VS_DOTNET_REFERENCE_UnityEngine
    ${UnityEngineLibraries}
)
set_property(TARGET VSTest1 PROPERTY VS_DOTNET_REFERENCES_COPY_LOCAL false)
set_property(TARGET VSTest1 PROPERTY VS_DOTNET_REFERENCEPROP_UnityEngine_TAG_CopyLocalSatelliteAssemblies False)


    
# Install dll
install(TARGETS VSTest1)

# Add pdb2mdb bat
if (CMAKE_BUILD_TYPE MATCHES Deb)
    message (STATUS "Will build using Pdb2mdbBat")
    add_custom_command(
        TARGET VSTest1 POST_BUILD
        COMMAND ${Pdb2mdbBat} ARGS "$<TARGET_FILE:VSTest1>"
    )
    install(FILES $<TARGET_FILE:VSTest1>.mdb TYPE BIN)
endif()

# May copy install of install
#add_custom_command(
#    TARGET myBinary 
#    POST_BUILD
#        COMMAND ${CMAKE_COMMAND} -E copy  
#                     "${CMAKE_CURRENT_SOURCE_DIR}/myTest.txt" 
#                     "$<TARGET_FILE_DIR:myBinary>/myTest.txt"
#)