# Project Title

Use blender to generate systhesized omnnidirectional images

## Prerequisites
1. Clone the blender repo:

    git clone https://github.com/blender/blender.git
    cd blender
    git checkout v2.75

2. Modify the source code    

    cp path/to/compile.patch .
    git apply compile.patch

3. Install the dependencies(gcc>=9):
    
    ./build_files/build_environment/install_deps.sh

4. Run the following commnd to compile and install blender(gcc==7)

    Change the gcc version before make.

    make -j12 BUILD_CMAKE_ARGS=" -D PYTHON_ROOT_DIR=/opt/lib/python-3.4 -D OPENCOLORIO_ROOT_DIR=/opt/lib/ocio -D WITH_CYCLES_OSL=OFF -D WITH_LLVM=OFF -D WITH_CODEC_FFMPEG=ON -D FFMPEG_LIBRARIES='avformat;avcodec;avutil;avdevice;swscale;rt;theora;theoradec;theoraenc;vorbis;vorbisenc;vorbisfile;ogg;x264;openjp2' -D FFMPEG=/opt/lib/ffmpeg"

5. Compile complete

    All output files are stored under the build_linux in the parent directory

## How to run 
To start the blender
    ../build_linux/bin/blender



## Using the Omnidirectional camera model

* Make sure you're using the [Cycles render engine](http://www.blender.org/manual/render/cycles/introduction.html)
* Select your camera, and go to the camera panel
* Switch the Lens type to "Panoramic" and select the "Omnidirectional" lens subtype
* Render your image normally (both CPU and GPU rendering are supported)

## Omnidirectional camera parameters

<img src="screenshot.png" width="800">

* *Polynomial*: a0, a1, a2, a3, a4, a5 correspond to the polynomial backward projection function parameters (in increasing degree order)
* *Shift*: projection center shift from the image center, in pixels
* *Affine*: correspond to the affine parameters in the omnidirectional camera model
* *Radius*: scale factor used to compute the radius of the crop circle (radius = scale * image_height / 2.0). If zero, no crop circle is added.
