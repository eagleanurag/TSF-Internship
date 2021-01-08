Requirements
============

- OpenCV
- CMake

Compilation
===========

    mkdir build
    cd build
    cmake ../basicOCR
    make

Running demo
============

./OCR

Paint over window a number
To classify press "c" key and in console you can see result,  precission and Accuracy
For create other image you can clean image with "r"
You can increase or decrease cursor radio with "+" and "-" keys

Keys control
============

    "r" - reset image
    "+" - cursor radio increment
    "-" - cursor radio decrement
    "s" - Save image as out.png
    "c" - Classify image,  the result in console
    ESC - quit the program
