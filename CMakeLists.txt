cmake_minimum_required(VERSION 3.16)
project(main)

# Set the OpenCV package flags obtained from pkg-config
set(CMAKE_CXX_STANDARD 17)
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})
set(OpenCV_LIBS
    opencv_stitching
    opencv_alphamat
    opencv_aruco
    opencv_barcode
    opencv_bgsegm
    opencv_bioinspired
    opencv_ccalib
    opencv_dnn_objdetect
    opencv_dnn_superres
    opencv_dpm
    opencv_face
    opencv_freetype
    opencv_fuzzy
    opencv_hdf
    opencv_hfs
    opencv_img_hash
    opencv_intensity_transform
    opencv_line_descriptor
    opencv_mcc
    opencv_quality
    opencv_rapid
    opencv_reg
    opencv_rgbd
    opencv_saliency
    opencv_shape
    opencv_stereo
    opencv_structured_light
    opencv_phase_unwrapping
    opencv_superres
    opencv_optflow
    opencv_surface_matching
    opencv_tracking
    opencv_highgui
    opencv_datasets
    opencv_text
    opencv_plot
    opencv_ml
    opencv_videostab
    opencv_videoio
    opencv_viz
    opencv_wechat_qrcode
    opencv_ximgproc
    opencv_video
    opencv_xobjdetect
    opencv_objdetect
    opencv_calib3d
    opencv_imgcodecs
    opencv_features2d
    opencv_dnn
    opencv_flann
    opencv_xphoto
    opencv_photo
    opencv_imgproc
    opencv_core
)

# Find the OpenCV package (not needed since we've manually set the flags)
# find_package(OpenCV 4 REQUIRED)

# include has 2 subdirectories: tensorflow and flatbuffers
# get the folder form https://github.com/muhammedakyuzlu/tensorflow_lite_libs_cpp.git
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/include)

# lib has 1 file: libtensorflowlite.so
ADD_LIBRARY(tensorflowlite SHARED IMPORTED)
set_property(TARGET tensorflowlite PROPERTY IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/libs/libtensorflowlite.so)

file(GLOB SOURCE_FILES src/*.cpp)
add_executable(${CMAKE_PROJECT_NAME} ${SOURCE_FILES})

target_link_libraries(
    ${CMAKE_PROJECT_NAME}
    ${OpenCV_LIBS}
    tensorflowlite
    pthread
)
