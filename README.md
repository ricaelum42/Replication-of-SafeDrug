<!---
Code (10 Points)
x Citation to the original paper
x Link to the original paper’s repo (if applicable)
x Dependencies
x Data download instruction
x Preprocessing code + command (if applicable)
x Training code + command (if applicable)
x Evaluation code + command (if applicable)
x Pretrained model (if applicable)
x Table of results (no need to include additional experiments, but main reproducibility result should be included)
-->

# Replication of [SafeDrug: Dual Molecular Graph Encoders for Safe Drug Recommendations](https://arxiv.org/pdf/2105.02711.pdf)

## Citation
```bibtex
@inproceedings{yang2021safedrug,
    title = {SafeDrug: Dual Molecular Graph Encoders for Safe Drug Recommendations},
    author = {Yang, Chaoqi and Xiao, Cao and Ma, Fenglong and Glass, Lucas and Sun, Jimeng},
    booktitle = {Proceedings of the Thirtieth International Joint Conference on
               Artificial Intelligence, {IJCAI} 2021},
    year = {2021}
}
```

This repo is a replication of user `ycq091044`'s repo: [Data and Code for IJCAI'21 paper - **SafeDrug**](https://github.com/ycq091044/SafeDrug)

## Package Dependency
- rdkit conda environment
```python
conda create -c conda-forge -n SafeDrug  rdkit
conda activate SafeDrug
```

- in SafeDrug environment
```python
pip install scikit-learn
pip install dill
pip install dnc

pip install torch
```

## Data
The following data are used in the replication work. Note that due to data privacy issue we are not able to share the MIMIC-III dataset in Github. If needed please request for access via https://physionet.org/content/mimiciii/1.4/
To run the code, the ```data/input``` folder should contain the following files:
- MIMIC-III datasets for patient information
    - PRESCRIPTIONS.csv: Consists of medications ordered for each research subject
    - DIAGNOSES\_ICD.csv: Consists of ICD9 diagnosis codes for each research subject
    - ROCEDURES\_ICD.csv: Consists of ICD9 procedure codes for each research subject
- Other datasets for drug information can be directly obtained from the author's repository
    - RXCUI2atc4.csv: A mapping file that maps from RSCUI code to ATC 4th level code
    - drug-atc.csv: A mapping file that maps from CID code to ATC code
    - rxnorm2RXCUI.txt: A mapping file that maps from RxNorm code to RXCUI code
    - drugbank_drugs_info.csv: A mapping file that maps from drug names to drug SMILES string.
    - drug-DDI.csv: Contains DDI information for each pair of CID

We used the existing data preprocessing code provided by the author to obtain preprocessed data.
Download the processing.py file from the author's repository [SafeDrug/data](https://github.com/ycq091044/SafeDrug/tree/main/data).
Run the processing code to get preprocessed data
```
python processing.py
```
Our preprocessed data is available for use at [data/output](https://github.com/ricaelum42/Replication-of-SafeDrug/tree/main/data/output)

## Replicated Code
[Replication-of-SafeDrug](https://github.com/ricaelum42/Replication-of-SafeDrug/blob/main/code/SafeDrug.ipynb) can be ran as `ipynb` on `Google Colab`
- Select `Open in Colab` in the `ipynb` file
- Change `Hardware accelerator` to `GPU` in `Runtime` -> `Change runtime type`
- Select `Runtime`->`Restart and run all`

## Baseline Model
### Launch Models
Each of the baseline models are available as `ipynb` files and can be accessed through `Google Colab`.
\
Please note that the baseline `ipynb` files will require access to `models.py` and `util.py` in [Replication-of-SafeDrug/code/](https://github.com/ricaelum42/Replication-of-SafeDrug/tree/main/code). `ipynb` files should be edited accordingly to reflect any changes in path changes.
- To run **GAMENet**, **LEAP**, **RETAIN**
\
Select `Open in Colab` in the `ipynb` file
\
Change `Hardware accelerator` to `GPU` in `Runtime` -> `Change runtime type`
\
Select `Runtime`->`Restart and run all`

- To run **LR**
\
Select `Open in Colab` in the `ipynb` file
\
Select `Runtime`->`Restart and run all`

## Results
### Replicated Model Performance

| Model | DDI | Jaccard |
| :---: | :---: | :---: |
| SafeDrug | 0.0619 | 0.5111 |
| LR | 0.0777 | 0.4903 |
| RETAIN |0.0800 | 0.4857 |
| LEAP | 0.0729 | 0.4496 |
| GAMENet | 0.0751 | 0.5145 |

### Replicated Model Efficiency

| Model | # of Param. | Train Time | Test Time |
| :---: | :---: | :---: | :---: |
| SafeDrug | 366,122 | 239.16s /Epoch | 11.77s |
| RETAIN | 285,489 | 37.41 /Epoch | 7.73s |
| LEAP | 428,403 | 278.32s /Epoch | 29.21s |
| GAMENet | 444,209 | 114.25s /Epoch | 15.07s |

### Replicated Model Output Files
- **SafeDrug**: [code/saved/SafeDrug](https://github.com/ricaelum42/Replication-of-SafeDrug/tree/main/code/saved/SafeDrug)
- **LR**: [baseline/lr/output_files](https://github.com/ricaelum42/Replication-of-SafeDrug/tree/main/baseline/lr/output_files)
- **RETAIN**: [baseline/retain/output_files](https://github.com/ricaelum42/Replication-of-SafeDrug/tree/main/baseline/retain/output_files)
- **LEAP**: [baseline/leap/output_files](https://github.com/ricaelum42/Replication-of-SafeDrug/tree/main/baseline/leap/output_files)
- **GAMENet**: [baseline/gamenet/output_files](https://github.com/ricaelum42/Replication-of-SafeDrug/tree/main/baseline/gamenet/output_files)
