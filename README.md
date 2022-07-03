# Interpretable Deep Learning for Improving Cancer Patient Survival Based on Personal Transcriptomes

![Im](https://i.imgur.com/XWjDUTW.jpg)



[Bo Sun](bsun0802.github.io), [Liang Chen](https://lianglab.usc.edu/people.html)

Codebase for our paper under review "Interpretable Deep Learning for Improving Cancer Patient Survival Based on Personal Transcriptomes".

Feel free to reach out to bos@usc.edu or liang.chen@usc.edu if you have questions.

## Usage

### Python Environment

Our code is built upon the code released from the [drugcell paper](https://www.cell.com/cancer-cell/pdf/S1535-6108(20)30488-8.pdf). The pytorch environment used was the same. Please refer to the [DrugCell github repo](https://github.com/idekerlab/DrugCell) for environment setup. Use conda for pain-free setup:

` conda env create -f environment.yml`



After setting up the environment, activate to run the training and testing code. 

`conda activate drugcell`# On my machine, the conda env was named "drugcell" 



### Training

Regression:

```bash
python -u /home1/bos/repo/DrugCell/code/train_drugcell.py \
                            -onto /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/drugcell_ont.txt \
                            -drug2id /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/drug2ind.txt \
                            -fingerprint /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/drug2fingerprint.txt \
                            -gene2id /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/gene2ind.txt \
                            -cell2id /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/cell2ind.txt \
                            -genotype /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/cell2expr_zscore.txt \
                            -train /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/drugcell_train_log_v2.txt  \
                            -test /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/drugcell_val_log_v2.txt  \
                            -modeldir /scratch1/bos/bos/DepMap-models/dead_interp \
                            -genotype_hiddens 4 \
                            -drug_hiddens "64,32,4" \
                            -final_hiddens 4 \
                            -epoch 1500 \
                            -batchsize 1000 \
                            -lr 0.0003 \
                            -activation relu 
                            
```

Classification:

```bash
python -u /home1/bos/repo/DrugCell/code/train_drugcell_binary.py \
                            -onto /scratch1/bos/bos/DepMap-data/drugcell-GDC-alive-patient/drugcell_ont.txt \
                            -drug2id /scratch1/bos/bos/DepMap-data/drugcell-GDC-alive-patient/drug2ind.txt \
                            -fingerprint /scratch1/bos/bos/DepMap-data/drugcell-GDC-alive-patient/drug2fingerprint.txt \
                            -gene2id /scratch1/bos/bos/DepMap-data/drugcell-GDC-alive-patient/gene2ind.txt \
                            -cell2id /scratch1/bos/bos/DepMap-data/drugcell-GDC-alive-patient/cell2ind.txt \
                            -genotype /scratch1/bos/bos/DepMap-data/drugcell-GDC-alive-patient/cell2expr_zscore.txt \
                            -train /scratch1/bos/bos/DepMap-data/drugcell-GDC-alive-patient/drugcell_train_v2.txt  \
                            -test /scratch1/bos/bos/DepMap-data/drugcell-GDC-alive-patient/drugcell_val_v2.txt  \
                            -modeldir /scratch1/bos/bos/DepMap-models/alive_zscore_v2 \
                            -genotype_hiddens 6 \
                            -drug_hiddens "64,32,6" \
                            -final_hiddens 6 \
                            -epoch 1500 \
                            -batchsize 2000 \
                            -lr 0.0002
```

### Inference

Regression:

```bash
python -u /home1/bos/repo/DrugCell/code/predict_drugcell.py \
                            -predict /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/drugcell_test_log_v2.txt \
                            -drug2id /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/drug2ind.txt \
                            -gene2id /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/gene2ind.txt \
                            -cell2id /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/cell2ind.txt \
                            -fingerprint /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/drug2fingerprint.txt \
                            -genotype /scratch1/bos/bos/DepMap-data/drugcell-GDC-dead-patient/cell2expr_zscore.txt \
                            -load /scratch1/bos/bos/DepMap-models/dead_interp/model_1440.pt \
                            -hidden /scratch1/bos/bos/DepMap-output/test_dead/hidden \
                            -result /scratch1/bos/bos/DepMap-output/test_dead/result 
```



Classification:

```bash
python -u /home1/bos/repo/DrugCell/code/predict_drugcell_binary.py \
                            -predict /scratch/bos/DepMap-data/drugcell-GDC-alive-patient/drugcell_test_v2.txt \
                            -drug2id /scratch/bos/DepMap-data/drugcell-GDC-alive-patient/drug2ind.txt \
                            -gene2id /scratch/bos/DepMap-data/drugcell-GDC-alive-patient/gene2ind.txt \
                            -cell2id /scratch/bos/DepMap-data/drugcell-GDC-alive-patient/cell2ind.txt \
                            -fingerprint /scratch/bos/DepMap-data/drugcell-GDC-alive-patient/drug2fingerprint.txt \
                            -genotype /scratch/bos/DepMap-data/drugcell-GDC-alive-patient/cell2expr_zscore.txt \
                            -load /scratch/bos/DepMap-models/alive_zscore_v2/model_1180.pt \
                            -hidden /scratch/bos/DepMap-output/alive_patient_livability_pred_v2/hidden \
                            -result /scratch/bos/DepMap-output/alive_patient_livability_pred_v2/result

```

> Those are the command line examples I used. Please read `.py` files to understand arguments details and adapt the absolute path to your computer. 

## Data

The processed data that we used in our work are donwloadble from google drive. 

[Data](https://drive.google.com/file/d/10_oMfrG4dmg1eZCZQnn4V7g2lHdxfY82/view?usp=sharing) of deceased patients for the regression part.

[Data](https://drive.google.com/file/d/1W7wn1RiqrIsigqnrLneYe46Gtu42J5YM/view?usp=sharing) for the classification part.



Some important files are:

- `cell2expr_zscore.txt` expression values z-scrore for each gene, calculated across patients
- `drug2fingerprint.txt` prepared drug fingerprint
- `drugcell_ont.txt` the ontology DAG used to guide the network structure



The notebook here `TCGA.ipynb` outlines the data preparation we performed, you can reproduce the work base on it. The code in this notebook are not clean enough for a "execute all cells" for two reasons, (i) the paths are hard coded local paths on my own labptop. (ii) some cells are not ordered, e.g., insert a cell above/below and I executed them in different orders. 

> But it should be clean enough to provide clear clue on each of steps we took, including drug to fingerprint and other steps.





## Citation

To be filled. 