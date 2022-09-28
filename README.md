# MOLI_standalone

## Purpose
First of all, I appreciate the author of MOLI for making the codes public. And I would like to contribute something for fellow researchers who are working on drug response prediction.

This is a refactored version of MOLI gene expression code. The purpose of refactoring is to run MOLI gene expression code on any dataset and specify various hyperparameters for each experiment without modifying source code.

### Highlights of this version:

1. Split training code and test code
2. Specify dataset and hyperparameters as command arguments
3. Save several charts

## Usage

For help
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

## Training

```
python MOLI_train.py -if Docetaxel_training.csv -mf Docetaxel.pth -dc 0.0125 -mb 36 -id 32 -lr 0.1 -dr 0.5 -wd 0.0001 -gm 0.5 -ep 10 -tm 3
```

## Test

```
python MOLI_test.py -if combat_GDSC_2014_Docetaxel_test.csv -mf combat_GDSC_2014_Docetaxel.pth
```
Thank you very much,


Brian
