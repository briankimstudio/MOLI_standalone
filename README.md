# MOLI_standalone

## Purpose
First of all, I appreciate the author of MOLI for making the codes public. And I would like to contribute something for fellow researchers who are working on drug response prediction.

This is a refactored version of MOLI gene expression code. The purpose of refactoring is to run MOLI gene expression code on any dataset and specify various hyperparameters for each experiment without modifying source code.

### Highlights of this version:

1. Split training code and test code
2. Specify dataset and hyperparameters as command arguments
3. Save trained model, hyperparameters, scaler
4. Save AUC, strip, confusion matrix plot

## Usage

### Help

```
$ python MOLI_train.py -h

usage: MOLI_train.py [-h] -if IF -mf MF [-id ID] [-dr DR] -dc DC [-ep EP] [-it IT] [-mb MB]
                     [-lr LR] [-wd WD] [-tm TM] [-gm GM]

Train MOLI model

optional arguments:
  -h, --help  show this help message and exit
  -if IF      Input Filename
  -mf MF      Model Filename for storing the model after training
  -id ID      Input Dimension for neural network. 32~1024 (Default: 1024)
  -dr DR      Dropout Rate for neural network. 0.3~0.5 (Default: 0.5)
  -dc DC      Drug Cutoff for converting IC50 to binary class. For example, Docetaxel is 0.0125
  -ep EP      EPoch. 20~100 (Default: 20)
  -it IT      ITeration. 1~50 (Default: 1)
  -mb MB      Mini Batch size. 8~64 (Default: 36)
  -lr LR      Learning Rate for neural network. 0.00001~0.5 (Default: 0.001)
  -wd WD      Weight Decay for neural network. 0.0001~0.1 (Default: 0.001)
  -tm TM      Triplet Margin. 0.5~3 (Default: 3)
  -gm GM      Gamma. 0.005~0.1 (Default: 0.5)

```

### Training

- Filename of input dataset: Docetaxel_training.csv
- Filename of trained model: Docetaxel.pth

```
$ python MOLI_train.py -if Docetaxel_training.csv -mf Docetaxel.pth -dc 0.0125 -mb 36 -id 32 -lr 0.1 -dr 0.5 -wd 0.0001 -gm 0.5 -ep 10 -tm 3
```

### Output

```
--------------------------------------------------------------------------------
Train MOLI only expression model
--------------------------------------------------------------------------------
--------------------------------------------------------------------------------
Experiment configuration
--------------------------------------------------------------------------------
if: Docetaxel_training.csv
mf: Docetaxel.pth
id: 32
dr: 0.5
dc: 0.0125
ep: 10
it: 1
mb: 36
lr: 0.1
wd: 0.0001
tm: 3.0
gm: 0.5
--------------------------------------------------------------------------------
Modified version of MOLI only expression: Training
--------------------------------------------------------------------------------
Date               : 2022-09-28 10:07:41.731896
Input filename     : Docetaxel_training.csv
Model filename     : Docetaxel.pth
Feature dimension  : (850, 7963)
Class distribution : [0:286, 1:564]
Baseline accuracy  : 0.6635
--------------------------------------------------------------------------------
I:1, K:1, Epoch:0/10, Loss:2.0792, Accuracy:0.5312, AUC:0.7295
I:1, K:1, Epoch:1/10, Loss:2.0184, Accuracy:0.5000, AUC:0.7594
I:1, K:1, Epoch:2/10, Loss:1.9222, Accuracy:0.6875, AUC:0.7598
I:1, K:1, Epoch:3/10, Loss:1.8329, Accuracy:0.7500, AUC:0.7601
I:1, K:1, Epoch:4/10, Loss:1.9362, Accuracy:0.7188, AUC:0.7041
I:1, K:1, Epoch:5/10, Loss:1.9004, Accuracy:0.5312, AUC:0.7465
I:1, K:1, Epoch:6/10, Loss:2.2440, Accuracy:0.5625, AUC:0.7864
I:1, K:1, Epoch:7/10, Loss:1.9599, Accuracy:0.5938, AUC:0.7684
I:1, K:1, Epoch:8/10, Loss:2.0142, Accuracy:0.6875, AUC:0.7882
I:1, K:1, Epoch:9/10, Loss:1.6791, Accuracy:0.6875, AUC:0.7788
----------------------------------------
K: 1, Mean AUC:0.7581
----------------------------------------
Model saved: combat_GDSC_2014_Docetaxel.pth
----------------------------------------
..
..
..
----------------------------------------
Best AUC: 0.7732
----------------------------------------
```

### Test

- Filename of input dataset: Docetaxel_test.csv
- Filename of trained model: Docetaxel.pth

```
$ python MOLI_test.py -if Docetaxel_test.csv -mf Docetaxel.pth
```
### Output

```
--------------------------------------------------------------------------------
Experiment configuration
--------------------------------------------------------------------------------
if: Docetaxel_test.csv
mf: Docetaxel.pth
--------------------------------------------------------------------------------
Modified version of MOLI only expression: Testing
--------------------------------------------------------------------------------
Date               : 2022-09-28 10:55:38.921152
Input filename     : Docetaxel_test.csv
Feature dimension  : (24, 7963)
Class distribution : [0:14, 1:10]
Baselne accuracy   : 0.5833
--------------------------------------------------------------------------------
Confusion matrix
[[6 8]
 [7 3]]
--------------------------------------------------------------------------------
Accuracy : 0.3750
AUC      : 0.3571
--------------------------------------------------------------------------------
              precision    recall  f1-score   support

         0.0     0.4615    0.4286    0.4444        14
         1.0     0.2727    0.3000    0.2857        10

    accuracy                         0.3750        24
   macro avg     0.3671    0.3643    0.3651        24
weighted avg     0.3829    0.3750    0.3783        24
```

### Submit to cluster

Use `qsub` command to submit `job` file to cluster.

```
qsub docetaxel.pbs
```

