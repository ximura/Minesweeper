# CMakeList.txt : CMake project for minesweeper, include source and define
# project specific logic here.
#
cmake_minimum_required (VERSION 3.8)

project ("minesweeper")

# Add source to this project's executable.
add_executable (minesweeper
    "src/main.cpp"
    "src/MineField.cpp"
    "src/MineField.h"
    "src/MineElement.cpp"
    "src/MineElement.h"
    "src/EmptyElement.cpp"
    "src/EmptyElement.h"
    "src/ElementStatus.h"
    "src/Element.h")

# TODO: Add tests and install targets if needed.
