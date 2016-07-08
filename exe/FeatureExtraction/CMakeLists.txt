cmake_minimum_required(VERSION 2.8.3)

find_package(catkin REQUIRED COMPONENTS
	roscpp
	rospy
	std_msgs
	openface_msgs
	message_generation
)

catkin_package(
	CATKIN_DEPENDS message_runtime roscpp rospy std_msgs
)

include_directories(
	${catkin_INCLUDE_DIRS}
)

add_executable(FeatureExtraction FeatureExtraction.cpp)

# Local libraries
include_directories(${LandmarkDetector_SOURCE_DIR}/include)

include_directories(../../lib/local/LandmarkDetector/include)
include_directories(../../lib/local/FaceAnalyser/include)		

target_link_libraries(FeatureExtraction LandmarkDetector)
target_link_libraries(FeatureExtraction FaceAnalyser)
target_link_libraries(FeatureExtraction dlib)

target_link_libraries(FeatureExtraction ${OpenCV_LIBS} ${Boost_LIBRARIES} ${TBB_LIBRARIES} ${catkin_LIBRARIES})

install (TARGETS FeatureExtraction DESTINATION ${CMAKE_BINARY_DIR}/bin)