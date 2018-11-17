To compile Pixel Blender disassembler to write assembler code:

Replace `#include <malloc.h>` by `#include <stdlib.h>`

	g++ apbj.cpp -o apbj
	g++ dpbj.cpp -o dpbj
