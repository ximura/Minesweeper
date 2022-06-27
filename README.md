To build you would need to install *cmake*

```bash
mkdir bin
cd bin
cmake ..
make
./minesweeper
```
Program run example
```
$ ./minesweeper 
Enter fied size:
10
Enter bomb count:
10
0 0 0 0 1 2 2 1 0 0 
1 1 1 0 1 M M 1 1 1 
1 M 1 0 1 2 2 1 1 M 
1 1 1 0 0 0 1 1 2 1 
0 0 0 0 0 0 1 M 1 0 
0 0 0 0 0 0 1 1 1 0 
1 1 0 0 0 0 0 1 1 1 
M 2 1 1 1 1 0 1 M 1 
3 M 1 1 M 1 0 1 1 1 
M 2 1 1 1 1 0 0 0 0 

------------------------------------------
Enter coordinate to open from (0-9):
9 9
0 0 0 0 1 ? ? ? ? ? 
1 1 1 0 1 ? ? ? ? ? 
? ? 1 0 1 2 2 ? ? ? 
1 1 1 0 0 0 1 ? ? ? 
0 0 0 0 0 0 1 ? ? ? 
0 0 0 0 0 0 1 1 ? ? 
1 1 0 0 0 0 0 1 ? ? 
? 2 1 1 1 1 0 1 ? ? 
? ? ? ? ? 1 0 1 1 1 
? ? ? ? ? 1 0 0 0 0 
Enter coordinate to open from (0-9):
0 0
0 0 0 0 1 ? ? ? ? ? 
1 1 1 0 1 ? ? ? ? ? 
? ? 1 0 1 2 2 ? ? ? 
1 1 1 0 0 0 1 ? ? ? 
0 0 0 0 0 0 1 ? ? ? 
0 0 0 0 0 0 1 1 ? ? 
1 1 0 0 0 0 0 1 ? ? 
? 2 1 1 1 1 0 1 ? ? 
? ? ? ? ? 1 0 1 1 1 
? ? ? ? ? 1 0 0 0 0 
Enter coordinate to open from (0-9):
0 9
BOOM!!!
```

## Part 1:
Choose a data structure(s) to represent the game state. You need to keep track of the following:
- NxN board
- Location of bombs
- Counts of # of adjacent bombs
- Whether a cell is open

MineField.cpp - represent game field, with list of elements (cells).
All elements stored in std::vector, as we need to have quick read access.
Element.h - board element interface with 2 implementations:
* EmptyElement - represents empty field, has counter for adjusted mines
* MineElement - represents mine

## Part 2:
Populate your data structure with K bombs placed in random locations. Note that should place
exactly K bombs and their location should be random with a uniform distribution.

We use [std::uniform_int_distribution](https://en.cppreference.com/w/cpp/numeric/random/uniform_int_distribution) as standart implementation of uniform distribution.

## Part 3
For each cell without a bomb, compute and store the number of adjancent bombs. Note that
diagonals also count. E.g.

This step is done on initialization phase, so that game update loop had to do less on each frame.

## Part 4
Write the logic that updates which cells become visible when a cell is clicked. Note that if a cell
has zero adjacent bombs the game needs to automatically make the surrounding cells visible.

This logic implemented in MineField::Check(int x, int y)
We need to check every adjusted field, so it's 8 checkes per field element. In worst case if there are 0 mines we would need to check every element and complexity gonna be O(N*N)
