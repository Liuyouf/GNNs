# Paper: HMM-GDAN: Hybrid Multi-View and Multi-Scale Graph Duplex-Attention Networks for Drug Response Prediction in Cancer

## 1. Experiment Environment

Please install the environment using anaconda3;

conda create -n HMM-GDAN python=3.6

Install the necessary packages.

conda install -c rdkit rdkit

pip install fitlog

pip install torch (1.6.0)

pip install torch-cluster (1.5.9) (https://pytorch-geometric.com/whl/)

pip install torch-scatter (2.0.6) (https://pytorch-geometric.com/whl/)

pip install torch-sparse (0.6.9) (https://pytorch-geometric.com/whl/)

pip install torch-spline-conv (1.2.1) (https://pytorch-geometric.com/whl/)

pip install torch-geometric (1.6.1)

## 2. Implementation

[Data can be download from the "/data" fold at https://github.com/violet-sto/TGSA]
   
### Step1: Data Preprocessing
data/CellLines_DepMap/CCLE_580_18281/census_706/ - Raw genetic profiles from CCLE and the processed features. You can also preprocess your own data with preprocess_gene.py.

data/similarity_augment/ - Directory edge contains edges of heterogeneous graphs; directory dict contains necessary data and dictionaries for mapping between drug data or cell line data.

data/Drugs/drug_smiles.csv - SMILES for 170 drugs. You can generate pyg graph object with smiles2graph.py

data/PANCANCER_IC_82833_580_170.csv - There are 82833 ln(IC50) values across 580 cel lines and 170 drugs.

data/9606.protein.links.detailed.v11.0.txt and data/9606.protein.info.v11.0.txt - Extracted from https://stringdb-static.org/download/protein.links.detailed.v11.0/9606.protein.links.detailed.v11.0.txt.gz

### Step2 : Model Training/Testing
You can run python main.py --mode "train" to train our method HMM-GDAN or run python main.py --mode "test" to test trained our method HMM-GDAN.

### Step3 (Optional): Similarity Augment
First, you can run heterogeneous_graph.py to generate edges of heterogeneous graphs.

Then, you can run main_SA.py to generate node features of heterogeneous graphs using two GNNs from HMM_GDAN/HMM_GDAN_pre and to fine-tune sequentially the remained parameters from HMM_GDANM/HMM_GDAN_pre. To be specific, you can use the instruction python main_SA.py --mode "train"/"test" --pretrain 0/1 to fine-tune HMM_GDAN/HMM_GDAN_pre or to test fine-tuned SA/SA_pre.
