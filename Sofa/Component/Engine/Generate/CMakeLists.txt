cmake_minimum_required(VERSION 3.22)
project(Sofa.Component.Engine.Generate LANGUAGES CXX)

set(SOFACOMPONENTENGINEGENERATE_SOURCE_DIR "src/sofa/component/engine/generate")

set(HEADER_FILES
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/config.h.in
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/init.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/ExtrudeEdgesAndGenerateQuads.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/ExtrudeEdgesAndGenerateQuads.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/ExtrudeQuadsAndGenerateHexas.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/ExtrudeQuadsAndGenerateHexas.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/ExtrudeSurface.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/ExtrudeSurface.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GenerateCylinder.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GenerateCylinder.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GenerateGrid.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GenerateGrid.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GenerateRigidMass.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GenerateRigidMass.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GenerateSphere.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GenerateSphere.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GroupFilterYoungModulus.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GroupFilterYoungModulus.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/JoinPoints.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/JoinPoints.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MergeMeshes.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MergeMeshes.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MergePoints.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MergePoints.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MergeSets.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MergeSets.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MergeVectors.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MergeVectors.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MeshBarycentricMapperEngine.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MeshBarycentricMapperEngine.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MeshClosingEngine.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MeshClosingEngine.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MeshTetraStuffing.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/NormEngine.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/NormEngine.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/NormalsFromPoints.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/NormalsFromPoints.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/RandomPointDistributionInSurface.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/RandomPointDistributionInSurface.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/VolumeFromTetrahedrons.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/VolumeFromTetrahedrons.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/VolumeFromTriangles.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/VolumeFromTriangles.inl
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/Spiral.h
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/Spiral.inl
)

set(SOURCE_FILES
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/init.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/ExtrudeEdgesAndGenerateQuads.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/ExtrudeQuadsAndGenerateHexas.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/ExtrudeSurface.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GenerateCylinder.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GenerateGrid.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GenerateRigidMass.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GenerateSphere.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/GroupFilterYoungModulus.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/JoinPoints.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MergeMeshes.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MergePoints.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MergeSets.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MergeVectors.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MeshBarycentricMapperEngine.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MeshClosingEngine.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/MeshTetraStuffing.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/NormEngine.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/NormalsFromPoints.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/RandomPointDistributionInSurface.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/VolumeFromTetrahedrons.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/VolumeFromTriangles.cpp
    ${SOFACOMPONENTENGINEGENERATE_SOURCE_DIR}/Spiral.cpp
)

sofa_find_package(Sofa.Simulation.Core REQUIRED)

add_library(${PROJECT_NAME} SHARED ${HEADER_FILES} ${SOURCE_FILES})
target_link_libraries(${PROJECT_NAME} PUBLIC Sofa.Simulation.Core)

sofa_create_package_with_targets(
    PACKAGE_NAME ${PROJECT_NAME}
    PACKAGE_VERSION ${Sofa_VERSION}
    TARGETS ${PROJECT_NAME} AUTO_SET_TARGET_PROPERTIES
    INCLUDE_SOURCE_DIR "src"
    INCLUDE_INSTALL_DIR "${PROJECT_NAME}"
)

# Tests
# If SOFA_BUILD_TESTS exists and is OFF, then these tests will be auto-disabled
cmake_dependent_option(SOFA_COMPONENT_ENGINE_GENERATE_BUILD_TESTS "Compile the automatic tests" ON "SOFA_BUILD_TESTS OR NOT DEFINED SOFA_BUILD_TESTS" OFF)
if(SOFA_COMPONENT_ENGINE_GENERATE_BUILD_TESTS)
    enable_testing()
    add_subdirectory(tests)
endif()
