# SALoM: Structure Aware Temporal Graph Networks with Long-Short Memory Updater
This is the code repository of paper **SALoM**: Structure Aware Temporal Graph Networks with Long-Short Memory Updater, built on [DyGLib](https://github.com/yule-BUAA/DyGLib).
## Data preprocess
As we built our work upon DyGLib, most of the used original dynamic graph datasets come from [Towards Better Evaluation for Dynamic Link Prediction](https://openreview.net/forum?id=1GVpwr2Tfdg), 
which can be downloaded [here](https://zenodo.org/record/7213796#.Y1cO6y8r30o). 
Please download them and put them in ```DG_data``` folder. 
The Myket dataset comes from [Effect of Choosing Loss Function when Using T-batching for Representation Learning on Dynamic Networks](https://arxiv.org/abs/2308.06862) and can be accessed from [here](https://github.com/erfanloghmani/myket-android-application-market-dataset). 
The original and preprocessed files for Myket dataset are included in this repository.
We can run ```preprocess_data/preprocess_data.py``` for pre-processing the datasets.
For example, to preprocess the *Wikipedia* dataset, we can run the following commands:
```{bash}
cd preprocess_data/
python preprocess_data.py  --dataset_name wikipedia
```
We can also run the following commands to preprocess all the original datasets at once:
```{bash}
cd preprocess_data/
python preprocess_all_data.py
```
## Executing Scripts

### Scripts for Dynamic Link Prediction
Dynamic link prediction could be performed on all the thirteen datasets. 
If you want to load the best model configurations determined by the grid search, please set the *load_best_configs* argument to True.
#### Model Training
* Example of training *SALoM* on *USLegis* dataset:
```{bash}
python train_link_prediction.py --dataset_name USLegis --model_name Liquid --num_neighbors 10 --batch_size 10 --num_layers 1 --num_runs 5 --gpu 0
```
#### Model Evaluation
Three (i.e., random, historical, and inductive) negative sampling strategies can be used for model evaluation.
* Example of evaluating *SALoM* with *random* negative sampling strategy on *USLegis* dataset:
```{bash}
python evaluate_link_prediction.py --dataset_name USLegis --model_name Liquid --num_neighbors 10 --batch_size 10 --num_layers 1 --negative_sample_strategy random --num_runs 5 --gpu 0
```

### Scripts for Dynamic Node Classification
Dynamic node classification could be performed on Wikipedia and Reddit (the only two datasets with dynamic labels).
#### Model Training
* Example of training *SALoM* on *USLegis* dataset:
```{bash}
python train_node_classification.py --dataset_name USLegis --model_name Liquid --num_neighbors 10 --batch_size 10 --num_layers 1 --num_runs 5 --gpu 0
```
#### Model Evaluation
* Example of evaluating *SALoM* on *USLegis* dataset:
```{bash}
python evaluate_node_classification.py --dataset_name USLegis --model_name Liquid --num_neighbors 10 --batch_size 10 --num_layers 1 --num_runs 5 --gpu 0
```
