# IS2020_results

Datasets and results obtained for a submitted article on Information Sciences.

## Structure of the repository

The repository is separated into four different directories: datasets, folds, results_exp1, results_exp2. Next, we describe how to access their content.

## Datasets

The **datasets** directory contains all datasets used on the experiments on arff format. They are all binary classification datasets. To read the **Australian.arff** dataset in an R environment, for example, you can use the following code:

```r
library(foreign)
dataset = read.arff("datasets/Australian.arff")
```

## Folds

The directory **folds** contains all folds of each dataset, considering a 30 x 5-fold cross-validation. The files are a list in R, and the first indice represents the iteration, while the second indice represents one fold. In an R environment, you can use the following code to read a fold file and build the first train and test set of the first iteration.

```r
# Reading the folds for Australian dataset
folds = dget("folds/Australian.arff.folds")

# Getting the indices of the test set for the first fold of the first iteration 
test_indices = folds[[1]][[1]]

# Getting the indices of the train set for the first fold of the first iteration 
train_indices = base::c(folds[[1]][[2]], folds[[1]][[3]], folds[[1]][[4]], folds[[1]][[5]])

testset = dataset[test_indices,]
trainset = dataset[train_indices,]
```

## Results of the experiment 1

The **results_exp1** directory contains all results on the arff format for each dataset, considering the first experiment in the paper. Each line represents a fold and iteration, and each column represents a data complexity on the training set or a predictive performance of a classification algorithm.

```r
# Reading the results of the first experiment for the Australian dataset
result = read.arff("results_exp1/Australian.arff")

# Getting the value of N3 measure for the minority class for all folds and iterations
result$neighborhood.N3_partial.minority

# Getting the gmean performance of SVM classifier with radial kernel, cost 1, and gamma 1 on all folds and iterations 
result$SVM_radial_1_1.gmean
```

For a summary of these results, please check this [table](summary_results_exp1.csv)

## Results of the experiment 2

The **results_exp2** directory contains all results on the arff format for each dataset, considering the second experiment in the paper. Each line represents a fold and iteration, and each column represents a data complexity on the training set or a predictive performance of a classification algorithm after applying a preprocessing technique.

```r
# Reading the results of the first experiment for the acute-inflammations dataset
result = read.arff("results_exp2/analcatdata_apnea2.arff")

# Getting the value of N3 measure for the minority class for all folds and iterations after applying SMOTE
result$SMOTE.neighborhood.N3_partial.minority

# Getting the gmean performance of SVM classifier on all folds and iterations after applying SMOTE
result$SMOTE.SVM.gmean
```
For a summary of these results, please check this [table](summary_results_exp2.csv)
