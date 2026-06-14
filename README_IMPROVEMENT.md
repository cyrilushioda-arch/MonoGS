# MonoGS Improvement: Adaptive Isotropic Regularization + Appearance-Based Loop Closure

## Improvements Overview
- **Improvement A** (Section 6.1 in report): Per-Gaussian adaptive isotropic regularization based on local image gradient (`utils/slam_backend.py`)
- **Improvement B** (Section 6.2 in report): Appearance-based historical keyframe retrieval for soft loop closure (`utils/slam_frontend.py`)

## Environment
- Ubuntu 20.04
- Python 3.10
- PyTorch 2.0.1+cu118
- CUDA 11.8 (conda)
- GPU: NVIDIA RTX 4090

## Installation
```bash
conda create -n MonoGS python=3.10 -y
conda activate MonoGS
pip install torch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 --index-url https://download.pytorch.org/whl/cu118
pip install opencv-python==4.8.1.78 munch trimesh evo==1.11.0 open3d==0.17.0 torchmetrics imgviz PyOpenGL glfw PyGLM wandb lpips rich ruff plyfile tqdm
cd submodules/diff-gaussian-rasterization && pip install -e . --no-build-isolation && cd ../..
cd submodules/simple-knn && python setup.py install && cd ../..
```

## Run Commands

### Baseline (original MonoGS)
```bash
# TUM RGB-D
python slam.py --config configs/rgbd/tum/fr1_desk.yaml --eval
python slam.py --config configs/rgbd/tum/fr2_xyz.yaml --eval
# Replica
python slam.py --config configs/rgbd/replica/room0.yaml --eval
python slam.py --config configs/rgbd/replica/office0.yaml --eval
```

### Improved Version (A+B)
```bash
# Same commands - improvements are active by default in improvement branch
python slam.py --config configs/rgbd/tum/fr1_desk.yaml --eval
python slam.py --config configs/rgbd/tum/fr2_xyz.yaml --eval
python slam.py --config configs/rgbd/replica/room0.yaml --eval
python slam.py --config configs/rgbd/replica/office0.yaml --eval
```

## Experiment Logs
Results saved in `results/` directory per run.
