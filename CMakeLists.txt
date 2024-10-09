cmake_minimum_required(VERSION 3.21)

# Support new ``if()`` IN_LIST operator.
cmake_policy(SET CMP0057 NEW)

project (
  mvmf6-reader
#   VERSION 1.1.0
  LANGUAGES CXX C
)

set(CMAKE_CXX_STANDARD 11)

# set standard directory locations
include(GNUInstallDirs)

if(APPLE)
  set(CMAKE_INSTALL_BINDIR .)
endif()

# check for vtk
find_package(VTK REQUIRED)

# find_package(VTK
#   COMPONENTS
#     CommonColor
#     CommonComputationalGeometry
#     CommonCore
#     CommonDataModel
#     CommonExecutionModel
#     CommonMath
#     CommonMisc
#     CommonSystem
#     CommonTransforms
#     DICOMParser
#     doubleconversion
#     expat
#     FiltersCore
#     FiltersExtraction
#     FiltersGeneral
#     FiltersGeometry
#     FiltersHybrid
#     FiltersModeling
#     FiltersSources
#     FiltersStatistics
#     fmt
#     freetype
#     glew
#     # GUISupportMFC
#     GUISupportQt
#     ImagingCore
#     ImagingSources
#     InteractionStyle
#     IOCore
#     IOImage
#     IOLegacy
#     IOXML
#     IOXMLParser
#     jpeg
#     kissfft
#     loguru
#     lz4
#     lzma
#     metaio
#     ParallelCore
#     ParallelDIY
#     png
#     pugixml
#     RenderingCore
#     RenderingFreeType
#     RenderingLOD
#     RenderingOpenGL2
#     RenderingUI
#     vtksys
#     tiff
#     zlib
#   REQUIRED
# )


add_library(mvModflow6Reader SHARED
    modelviewer-mf6/mv/Modflow6DataSource.cpp
    modelviewer-mf6/mv/Modflow6DataSource.h
    modelviewer-mf6/mv/mvDataSource.cpp
    modelviewer-mf6/mv/mvDataSource.h
    modelviewer-mf6/mv/mvDefine.h
    modelviewer-mf6/mv/mvLinkList.cpp
    modelviewer-mf6/mv/mvLinkList.h
    modelviewer-mf6/mv/mvModelFeatures.cpp
    modelviewer-mf6/mv/mvModelFeatures.h
    modelviewer-mf6/mv/mvUtil.cpp
    modelviewer-mf6/mv/mvUtil.h
    modelviewer-mf6/mv/mvDisplayObject.cpp
)

# generate mvHeader for dll linkage
include(GenerateExportHeader)
generate_export_header(mvModflow6Reader
  EXPORT_FILE_NAME mvHeader.h
  BASE_NAME MV
)

target_include_directories(mvModflow6Reader PRIVATE ${CMAKE_CURRENT_BINARY_DIR})

target_link_libraries(mvModflow6Reader ${VTK_LIBRARIES})
