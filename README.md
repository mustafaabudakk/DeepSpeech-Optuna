# Speech to Text with DeepSpeech

We intervened this project for hyperparameter tuning and for now, only <b>train_batch_size</b>, <b>dropout_rate</b>, <b>learning_rate</b> and <b>n_hidden</b> are used. So as not to spoil the original code, we created a new <b>optuna_hp.py</b> on the same code and we had to change some methods and add the necessary code pieces for optuna optimization.

You can change the range of values within the method as you wish.

Some changes had to be made on checkpoint_dir in order to eliminate the errors encountered with the Optuna integration. In order to resolve these, you must enter the appropriate value for your machine in the <b>checkpoint_root_dir</b> variable in the <b>setup_dirs</b> method.

<h3> <b>Note:</b> </h3> In this study, the <b>distributed Optuna - multi GPU</b> relationship was used and the codes were updated for this purpose but suitable for single and multiple. For this non-purpose use, <b>create_study</b> may be modified as needed.

## How to Run

### Without Optuna Hyperparameter Optimization
```
CUDA_VISIBLE_DEVICES=0       # gpu/device id: for specific GPUs
nohup python DeepSpeech.py   # to run in the background
--scorer_path ~/name.scorer
--checkpoint_dir ~/checkpoints/
--epochs 20     
--train_batch_size 64   
--dev_batch_size 128   
--learning_rate 0.01   
--n_hidden 2056 
--dropout 0.05
--train_files ~/train.csv 
--dev_files ~/validation.csv
--test_files ~/test.csv
--export_dir ~/output_models/
--summary_dir ~/summaries/ 
--use_allow_growth true
--alphabet_config_path ~/alphabet.txt > ~/nohup_out.txt 2>&1 &
```

### With Optuna Hyperparameter Optimization
#### Which model parameters?
- train_batch_size
- dropout
- learning_rate
- n_hidden
```
CUDA_VISIBLE_DEVICES=0      # gpu/device id: for specific GPUs
nohup python DeepSpeech.py  # to run in the background
--scorer_path ~/name.scorer
--checkpoint_dir ~/checkpoints/
--epochs 20  
--dev_batch_size 128
--train_files ~/train.csv 
--dev_files ~/validation.csv
--test_files ~/test.csv
--export_dir ~/output_models/
--summary_dir ~/summaries/ 
--use_allow_growth true
--alphabet_config_path ~/alphabet.txt > ~/nohup_out.txt 2>&1 &
```

It is open for improvements and please let me know what new things can be added :)
