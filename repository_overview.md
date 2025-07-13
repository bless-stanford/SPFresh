# Repository Overview: SPFresh

## Project Description

**SPFresh** is a high-performance, storage-optimized approximate nearest neighbor (ANN) search system developed by Microsoft Research. It's designed to handle large-scale vector similarity search with efficient storage management and fast query performance.

## Key Features

### Core Functionality
- **Approximate Nearest Neighbor Search**: Fast similarity search in high-dimensional vector spaces
- **Storage-Optimized**: Built with SPDK (Storage Performance Development Kit) for high-performance storage access
- **Multiple Indexing Algorithms**: Supports BKT (Balanced K-means Tree), KDT (K-D Tree), and SPANN algorithms
- **GPU Support**: Includes GPU-accelerated indexing and search capabilities
- **Multi-threaded**: Optimized for concurrent operations

### Storage Architecture
- **SPDK Integration**: Uses SPDK for direct NVMe access, bypassing kernel overhead
- **RocksDB Integration**: Modified RocksDB as a storage option
- **LIRE Protocol**: Implements a novel protocol for efficient updates (distinguishing SPFresh from SPANN+)

## Technical Architecture

### Core Components

1. **AnnService/**: Main service implementation
   - Core algorithms (BKT, KDT, SPANN)
   - Vector indexing and search functionality
   - Client-server architecture
   - SSD serving capabilities

2. **Storage Layer**:
   - SPDK for high-performance NVMe access
   - Modified RocksDB for persistent storage
   - Custom storage optimization techniques

3. **GPU Support**:
   - GPU-accelerated indexing
   - GPU-based search operations
   - CUDA support via Docker

4. **Wrappers/**: Language bindings and API wrappers
5. **Tools/**: Utilities for index building, searching, and maintenance

### Supported Platforms
- **Primary**: Azure Standard_L16s_v3 instances (recommended)
- **OS**: Linux (tested on Ubuntu)
- **Hardware**: Requires NVMe SSDs, optional GPU acceleration

## Installation & Dependencies

### System Requirements
- CMake, GCC-9+ 
- SPDK (Storage Performance Development Kit)
- Modified RocksDB
- Various libraries: libjemalloc, libsnappy, libgflags, libtbb, etc.
- Optional: CUDA for GPU support

### Build Process
1. Install system dependencies
2. Build SPDK with specific configuration
3. Build modified RocksDB
4. Compile SPFresh using CMake

## Performance Characteristics

### Comparison with Baselines
- **SPFresh**: The main system with LIRE protocol optimization
- **SPANN+**: Base system without LIRE protocol
- **DiskANN**: Baseline system (Microsoft's NIPS'19 paper) showing out-of-place update bottlenecks

### Key Optimizations
- **LIRE Protocol**: Enables efficient in-place updates
- **Storage-Aware Design**: Minimizes I/O overhead
- **Multi-level Indexing**: Hierarchical index structures for scalability

## Research Context

This appears to be a research project (likely associated with an academic paper) that includes:
- **Artifact Evaluation**: Complete experimental scripts in `Script_AE/`
- **Reproducible Results**: Scripts to reproduce all experimental figures
- **Baseline Comparisons**: Fair comparison with existing systems like DiskANN

## Use Cases

1. **Large-Scale Vector Search**: Billion-scale vector similarity search
2. **Real-time Applications**: Fast query response times
3. **Storage-Constrained Environments**: Efficient use of SSD storage
4. **High-Throughput Systems**: Concurrent search operations

## Key Differentiators

1. **Storage Focus**: Unlike memory-based systems, optimized for SSD storage
2. **Update Efficiency**: LIRE protocol enables efficient vector updates
3. **Hardware Optimization**: Direct NVMe access via SPDK
4. **Academic Rigor**: Comprehensive experimental evaluation and reproducibility

## License
MIT License - Copyright (c) Microsoft Corporation

## Documentation
- Comprehensive getting started guide
- Parameter configuration documentation
- Jupyter notebook tutorials
- Installation guides for different platforms

This repository represents a significant advancement in storage-aware approximate nearest neighbor search systems, particularly valuable for large-scale applications requiring efficient storage utilization and fast query performance.