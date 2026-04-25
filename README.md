# CUDA Batch Signal Processor 🚀

**Course:** CUDA at Scale for the Enterprise (Coursera)  
**Project Type:** Independent Project (Peer-Graded Assignment)

## 📖 Project Description

This project fulfills the assignment requirement to process a large amount of data (specifically, hundreds of small inputs) using GPU computation. 

The **CUDA Batch Signal Processor** is a C++/CUDA application that simulates the batch ingestion and parallel processing of 100 individual signal arrays. Instead of relying on slow CPU-bound iterations, this program leverages the immense parallel processing power of a GPU to process the data, demonstrating a highly scalable architecture for signal processing.

## ⚙️ Code Description & Architecture

The program is contained within `batch_signals.cu` and follows a strict Host-to-Device-to-Host workflow:

1. **Initialization:** The host (CPU) loops through 100 batch iterations. For each iteration, it generates a synthetic signal array containing 1,024 data points (floats).
2. **Memory Management:** Memory is allocated on the GPU (`cudaMalloc`), and the raw signal data is transferred from the Host to the Device (`cudaMemcpy`).
3. **GPU Computation (The Kernel):** A custom CUDA kernel named `processSignal` is launched. The grid and block dimensions are calculated dynamically based on the signal size (using 256 threads per block). The kernel applies a mathematical amplification (multiplying each data point by 2.0) across all points in parallel.
4. **Retrieval & Cleanup:** The processed signal is copied back to the Host, verified, and the GPU memory is freed to prevent memory leaks during the 100-iteration batch run.

## 🛠️ How to Build and Run

To compile and execute this code in a CUDA-enabled environment (such as the Coursera Lab Terminal), run the following commands:

**1. Compile the code using the NVIDIA CUDA Compiler:**
```bash
nvcc batch_signals.cu -o batch_signals
