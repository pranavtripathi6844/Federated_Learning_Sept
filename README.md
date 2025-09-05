# Federated Learning Project - Local Implementation

A clean, production-ready implementation of federated learning with model editing capabilities, designed to run locally without Google Colab dependencies.

## 🚀 Features

- **Vision Transformer (ViT) Models**: Support for tiny, small, base, and large model sizes
- **Federated Learning**: FedAvg implementation with configurable client selection
- **Model Editing**: TaLoS (Task-Aware Layer-wise Sparsity) implementation
- **Iterative Mask Refinement**: Progressive pruning with Fisher Information Matrix
- **Soft-Zeroing**: Stable mask generation during Fisher computation
- **Local Execution**: No Google Colab dependencies required
- **Comprehensive Logging**: Integration with Weights & Biases
- **Modular Architecture**: Clean, maintainable code structure

## 📁 Project Structure


## 🛠️ Installation

1. **Clone or create the project folder**:
   ```bash
   cd ~/Desktop/Federated_Learning_Sept
   ```

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Download CIFAR-100 dataset** (automatic on first run)

## 🍎 Apple Silicon (M3/M2/M1) Support

This project now supports **Apple Silicon GPUs** using **Metal Performance Shaders (MPS)** for accelerated training on Mac M1, M2, and M3 series.

### **Requirements for Apple Silicon:**
- **macOS 12.3+** (Monterey or later)
- **PyTorch 1.12+** with MPS support
- **Apple Silicon Mac** (M1, M1 Pro, M1 Max, M2, M2 Pro, M2 Max, M3, M3 Pro, M3 Max)

### **Installation for Apple Silicon:**
```bash
# Install PyTorch with MPS support
pip install torch torchvision torchaudio

# Verify MPS availability
python -c "import torch; print(f'MPS available: {torch.backends.mps.is_available()}')"
```

### **Using Apple Silicon GPU:**
```bash
# Automatic device selection (recommended)
python main.py centralized --model_size small

# Explicit MPS usage
python main.py centralized --device mps

# Force CPU (for debugging)
python main.py centralized --device cpu
```

### **Performance on Apple Silicon:**
- **M3 Pro**: Excellent performance, can handle larger models
- **M2 Pro**: Good performance, suitable for most experiments
- **M1 Pro**: Good performance, may need smaller batch sizes

### **MPS-Specific Considerations:**
- **Unified Memory**: GPU and CPU share memory, allowing larger models
- **Batch Sizes**: Can use larger batch sizes compared to CPU
- **Compatibility**: Most PyTorch operations work with MPS
- **Fallback**: Automatically falls back to CPU if MPS unavailable

## 🚀 Quick Start

### Run Centralized Training
```bash
python main.py centralized --model_size small --num_epochs 100
```

### Run Federated Learning
```bash
python main.py federated --num_clients 100 --num_rounds 100
```

### Run Model Editing
```bash
python main.py editing --target_sparsity 0.9 --num_iterations 10
```

## 📊 Available Experiments

### 1. Centralized Training
- Baseline training for comparison
- Support for different model sizes
- Configurable hyperparameters

### 2. Federated Learning
- FedAvg algorithm implementation
- Configurable client selection
- IID and non-IID data distributions
- Client participation control

### 3. Model Editing (TaLoS)
- Fisher Information Matrix computation
- Iterative mask refinement
- Configurable sparsity targets
- Soft-zeroing for stability

## ⚙️ Configuration

Configuration files are located in `configs/`:
- `default_config.yaml`: Default settings
- `experiment_configs.yaml`: Predefined experiment configurations

## 🔧 Key Components

### SparseSGDWithMomentum
Custom optimizer that supports parameter masking for model editing.

### IterativeMaskGenerator
Generates pruning masks iteratively using Fisher Information scores.

### FederatedTrainer
Handles federated learning training with model editing capabilities.

### CIFAR100DataManager
Manages dataset loading, preprocessing, and federated data splitting.

## 📈 Monitoring

- **Weights & Biases**: Automatic experiment tracking
- **Checkpoints**: Regular model state saving
- **Visualization**: Training curves and mask analysis
- **Logging**: Comprehensive training metrics

## 🎯 Model Editing Process

1. **Fisher Computation**: Calculate parameter importance scores
2. **Iterative Pruning**: Progressive mask refinement over multiple rounds
3. **Soft-Zeroing**: Stable computation during mask generation
4. **Sparse Training**: Train with generated masks using SparseSGDWithMomentum

## 🔬 Advanced Usage

### Custom Configurations
```bash
python main.py federated --config configs/custom_config.yaml
```

### Hyperparameter Tuning
```bash
python main.py editing --target_sparsity 0.8 --num_iterations 8
```

### Model Size Comparison
```bash
python main.py centralized --model_size base --num_epochs 100
```

## 📝 Logging and Checkpoints

- **Checkpoints**: Saved every 5 epochs/rounds
- **Best Models**: Automatically saved based on validation performance
- **Training History**: JSON files with complete metrics
- **Wandb Integration**: Real-time experiment tracking

## 🐛 Troubleshooting

### Common Issues
1. **CUDA out of memory**: Reduce batch size or model size
2. **Dataset download issues**: Check internet connection and disk space
3. **Import errors**: Ensure you're in the correct directory

### Debug Mode
Enable debug output in experiment scripts for detailed logging.

## 📚 References

- **TaLoS**: Task-Aware Layer-wise Sparsity for Model Editing
- **FedAvg**: Federated Averaging for Federated Learning
- **Vision Transformer**: Attention-based image classification

## �� Contributing

This is a clean implementation of the original federated learning project, designed for local execution and easy modification.

## 📄 License

This project is for research and educational purposes.

---

**Ready to run locally!** 🎉
