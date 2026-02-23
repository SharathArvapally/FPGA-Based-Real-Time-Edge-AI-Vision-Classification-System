
# FPGA-Based Real-Time Edge AI Vision Classification System

## 📌 Project Overview

This project implements a hardware-accelerated Convolutional Neural Network (CNN) for real-time image classification using FPGA.  

The CNN model is trained in PyTorch, quantized to fixed-point format, and implemented in Verilog RTL for FPGA synthesis and timing analysis using Vivado.

The system demonstrates hardware-software co-design by mapping a trained neural network into a synthesizable FPGA architecture.

---

## 🎯 Objectives

- Train a CNN model in PyTorch
- Convert floating-point weights to fixed-point (Q8.8 format)
- Export quantized weights for hardware usage
- Implement convolution, ReLU, and fully connected layers in Verilog
- Load trained weights into FPGA using on-chip ROM
- Perform functional simulation in Vivado
- Analyze timing closure and resource utilization
- Compute latency and throughput metrics

---

## 🧠 CNN Architecture

### Software Model (PyTorch)

Conv2D (3x3, 1 filter)  
→ ReLU  
→ Flatten  
→ Fully Connected  
→ Classification Output  

### Hardware Architecture (FPGA RTL)

3×3 Convolution (9 DSP multipliers)  
→ ReLU (Comparator logic)  
→ Sequential MAC-based Fully Connected Layer  
→ Final Output Score  

All modules are fully synchronous (clocked) and reset-controlled.

---

## ⚙️ Implementation Details

### 1️⃣ Model Training (Kaggle – PyTorch)

- Dataset: MNIST
- Framework: PyTorch
- Quantization: 16-bit Fixed-Point (Q8.8)
- Weights exported to `.mem` format for FPGA

### 2️⃣ Fixed-Point Representation

- Data width: 16-bit signed
- Scale factor: 2^8 = 256
- Arithmetic implemented using signed multipliers

---

## 🧱 FPGA Modules

- `conv3x3.v` → Registered 3×3 convolution engine
- `relu.v` → Clocked ReLU activation
- `fc_layer.v` → Sequential MAC-based fully connected layer
- `top_module.v` → Complete CNN pipeline
- `testbench.v` → Functional verification
- `constraints.xdc` → Clock constraint (100 MHz)

Weights are stored in ROM and loaded via `$readmemh`.

---

## 🧪 Functional Verification

Vivado Behavioral Simulation verifies:

- Correct convolution output
- Correct ReLU behavior
- Correct FC accumulation
- RTL output matches PyTorch fixed-point inference

---

## 📊 Synthesis & Timing Analysis

Target Device: Xilinx Artix-7  

Measured Metrics:
- LUT utilization
- Flip-flop usage
- DSP slice usage
- Timing closure (WNS)
- Maximum operating frequency (Fmax)

---
Clock Constraint:
create_clock -period 10.000 -name clk [get_ports clk]


---

## 🚀 Performance Evaluation

Latency = (Pipeline cycles + FC cycles) / Fmax  

Example (100 MHz clock):
- Total cycles ≈ 678
- Latency ≈ 6–7 µs
- Throughput ≈ 100M operations/sec

---

## 🏗 Design Characteristics

✔ Fully synchronous design  
✔ Clock + Reset controlled  
✔ Fixed-point arithmetic  
✔ DSP-based multiplication  
✔ Synthesizable RTL  
✔ Timing-closure verified  
✔ Hardware-software co-design  

---

## 📁 Project Structure

---

## 🚀 Performance Evaluation

Latency = (Pipeline cycles + FC cycles) / Fmax  

Example (100 MHz clock):
- Total cycles ≈ 678
- Latency ≈ 6–7 µs
- Throughput ≈ 100M operations/sec

---

## 🏗 Design Characteristics

✔ Fully synchronous design  
✔ Clock + Reset controlled  
✔ Fixed-point arithmetic  
✔ DSP-based multiplication  
✔ Synthesizable RTL  
✔ Timing-closure verified  
✔ Hardware-software co-design  

---

## 📁 Project Structure
├── conv3x3.v
├── relu.v
├── fc_layer.v
├── top_module.v
├── testbench.v
├── constraints.xdc
├── conv_weights.mem
├── fc_weights.mem
└── README.md


---

## 💡 Key Learnings

- Mapping neural networks to hardware
- Fixed-point quantization tradeoffs
- DSP slice utilization in FPGA
- Timing constraint management
- Resource-performance tradeoff analysis
- Hardware validation of ML models

---
## Hardware Results

- Maximum Frequency: ~126 MHz
- Slice LUTs Used: 129 (0.39%)
- Registers Used: 81 (0.12%)
- DSP48 Used: 11 (9%)
- Timing Constraints: Met
- Inference Latency: ~87 ns (for demo input size)

---  

## 🔮 Future Improvements

- Multi-filter convolution support
- Parallel fully connected units
- BRAM-based weight storage
- Streaming line-buffer architecture
- AXI interface integration
- Real-time camera input support

---

## 📌 Conclusion

This project demonstrates the end-to-end deployment of a trained CNN model onto FPGA hardware using fixed-point arithmetic and RTL design.  

It highlights performance analysis, timing closure, and hardware acceleration techniques relevant for edge AI and FPGA-based ML systems.

---

## 👨‍💻 Author

Sharath Chandra  
FPGA & AI/ML Enthusiast  
