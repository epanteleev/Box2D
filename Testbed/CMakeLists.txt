# Some flags for GLEW
add_definitions(-DGLEW_STATIC)

set (TARGET_NAME Testbed)
# Define the framework files.
set(Testbed_Framework_SRCS
	Framework/Main.cpp
	Framework/RenderGL3.cpp
	Framework/RenderGL3.hpp
	Framework/Test.cpp
	Framework/Test.hpp
	Framework/DebugDraw.cpp
	Framework/DebugDraw.hpp
	Framework/imgui.h
	Framework/imgui.cpp
	Framework/stb_truetype.h
)

#define the test files.
set(Testbed_Tests_SRCS
	Tests/TestEntries.cpp
	Tests/AddPair.hpp
	Tests/ApplyForce.hpp
	Tests/BodyTypes.hpp
	Tests/Breakable.hpp
	Tests/Bridge.hpp
	Tests/BulletTest.hpp
	Tests/Cantilever.hpp
	Tests/Car.hpp
	Tests/Chain.hpp
	Tests/CharacterCollision.hpp
	Tests/CollisionFiltering.hpp
	Tests/CollisionProcessing.hpp
	Tests/CompoundShapes.hpp
	Tests/Confined.hpp
	Tests/ContinuousTest.hpp
	Tests/DistanceTest.hpp
	Tests/Dominos.hpp
	Tests/DumpShell.hpp
	Tests/DynamicTreeTest.hpp
	Tests/EdgeShapes.hpp
	Tests/EdgeTest.hpp
	Tests/Gears.hpp
	Tests/OneSidedPlatform.hpp
	Tests/Pinball.hpp
	Tests/PolyCollision.hpp
	Tests/PolyShapes.hpp
	Tests/Prismatic.hpp
	Tests/Pulleys.hpp
	Tests/Pyramid.hpp
	Tests/RayCast.hpp
	Tests/Revolute.hpp
	Tests/Rope.hpp
	Tests/RopeJoint.hpp
	Tests/SensorTest.hpp
	Tests/ShapeEditing.hpp
	Tests/SliderCrank.hpp
	Tests/SphereStack.hpp
	Tests/TheoJansen.hpp
	Tests/Tiles.hpp
	Tests/TimeOfImpact.hpp
	Tests/VaryingFriction.hpp
	Tests/VaryingRestitution.hpp
	Tests/VerticalStack.hpp
	Tests/Web.hpp
)

set(GLAD_RESOURCES glad/glad.h glad/glad.c)
# These are used to create visual studio folders.
source_group(Framework FILES ${Testbed_Framework_SRCS})
source_group(Tests FILES ${Testbed_Tests_SRCS})

include_directories( ${OPENGL_INCLUDE_DIR})

if(UNIX)
    set(LIBRARIES  dl glfw GL GLU X11)
elseif(WIN32)
    set(ADDITIONAL_LIBRARIES winmm)

    if(CMAKE_COMPILER_IS_GNUCXX)

    endif(CMAKE_COMPILER_IS_GNUCXX)
endif(UNIX)

add_executable(Testbed ${Testbed_Framework_SRCS} ${Testbed_Tests_SRCS} ${GLAD_RESOURCES})

file (COPY Data DESTINATION  ${CMAKE_BINARY_DIR}/${TARGET_NAME})

include_directories( glad/ ../box2d/include/)
include_directories(${GLEW_INCLUDE_DIR} ${GLFW_INCLUDE_DIR})

target_link_libraries( ${TARGET_NAME}
    Box2D ${ADDITIONAL_LIBRARIES} ${LIBRARIES}
) 
