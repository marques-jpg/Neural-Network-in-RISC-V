# Neural Network in RISC-V Assembly

## Overview
This project implements a simple feedforward Artificial Neural Network (ANN) completely in RISC-V Assembly. The network is designed to classify handwritten decimal digits (from raw PGM format images) using pre-trained weight matrices. 

The implementation reads the input image and the necessary weight matrices from binary files, performs the required linear algebra operations and activation functions, and outputs the predicted digit.

## Project Structure and Pipeline
The main execution pipeline is handled by the `classify` function, which performs the following steps:
1. **Data Loading:** Reads the weight matrices (`m0` and `m1`) and the input image (`input`) from binary files.
2. **Data Conversion:** Converts the raw byte data into 32-bit integer arrays for processing.
3. **Hidden Layer Computation:** Computes the hidden layer `h` using Matrix Multiplication and a ReLU activation function: `h = ReLU(matmul(m0, input))`.
4. **Output Layer Computation:** Computes the final output array `o` using Matrix Multiplication: `o = matmul(m1, h)`.
5. **Classification:** Uses the `argmax` function on the output array `o` to determine the highest scoring class, which corresponds to the predicted decimal digit.

## Implemented Functions
The program includes several modular assembly routines to handle specific tasks:
* `abs`: Computes the absolute value of an integer.
* `relu`: Applies the Rectified Linear Unit (ReLU) activation function in-place on an array.
* `argmax`: Returns the index of the largest element in an array.
* `dotproduct`: Computes the dot product of two integer arrays.
* `matmul`: Performs matrix multiplication of two integer matrices.
* `read_file`: Handles system calls to read data from files into memory.
* `turn_int`: Converts an array of bytes (chars) into 32-bit integers, with optional offset and value adjustments.
* `classify`: The main orchestrator that runs the neural network inference.

## Performance Optimizations
The code incorporates several optimizations to improve computational efficiency:
1. **Memory Access Minimization:** Reuses pointers and minimizes memory accesses for faster execution.
2. **Efficient Data Conversion:** Direct conversion of bytes to integers using optimized offsets, reducing redundant instructions.
3. **Optimized Matrix Multiplication:** Explicit register usage and manual index control during matrix operations to speed up the `matmul` routine.
4. **In-place ReLU:** The ReLU activation function modifies the array directly in memory, avoiding unnecessary memory allocation and copying.
5. **Efficient Stack Management:** Optimized use of the stack for context preservation and restoration during function calls.

## License

MIT License © 2025 Guilherme Marques.
