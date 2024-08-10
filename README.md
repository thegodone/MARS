# Reference implementation of our paper: A Motif-based Autoregressive Model for Retrosynthesis Prediction

# conda environment
We recommend to new a Conda environment to run the code originally: "We use Python-3.7, PyTorch-1.6.0, PyTorch-Geometric-2.0.2 and rdkit-202003.3.0"

use retrobridge requirement to create conda env. 

```
conda create --name retrobridge python=3.9 rdkit=2023.09.5 -c conda-forge -y
conda activate retrobridge
pip install -r requirements.txt

conda install -c pyg -c conda-forge torch-scatter
pip install tensorboardX
```

# Step-1: Data Processing

Run this command to convert reactions to molecular graphs, generate motif vocabulary and transformation paths:
```
python prepare_mol_graph.py
```

# Step-2: Training

To begin training, run this command:
```
python run_gnn.py
```

You can also setup hyperparameters describe in rnn_gnn.py:
```
python run_gnn.py --epochs 100 --device 0
```

# Step-3: Inference

To generate the predictions, run this command:
```
python run_gnn.py --test_only --input_model_file model_e100.pt
```

you can use multiprocessing to speed up the infernece phase:
```
python run_gnn.py --test_only --input_model_file model_e100.pt --num_process 16
```
