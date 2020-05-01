# Sudoku and Elaborations of Sudoku
Consider the task of solving a Sudoku puzzle given as an image. In NeurASP, we could use a neural network to recognize the digits in the given puzzle and use an ASP solver to compute the solution instead of having a single network that accounts for both perception and solving.

One great benefit is that we can use the same trained perception neural network to solve some elaborations of Sudoku problems, such as Anti-Knight Sudoku, Sudoku-X, and even Offset Sudoku if it does not use colored image.

## File Description
* data: a folder containing 2 pickle files storing the Sudoku images and their labels, 6 PyTorch models trained with different number of training data, and an example sudoku image that is used to show how NeurASP inference can be done on a Sudoku image.
* train.py: a Python file that defines the NeurASP program and calls learn method in neurasp package.
* test.py: a Python file that defines the NeurASP program and calls testNN method in neurasp package.
* dataGen.py: a Python file that load the train/test data and generate dataList, obsList (for training), and train_loader/test_loader (for computing the accuracy on training/testing data)
* network.py: a Python file that defines the network "identify".
* sudoku.ipynb: a Jupyter notebook for this example with detailed explanations to the codes

## Train
To start training, execute the following command under this folder.
```
python train.py [Num]
```
Num is an optional parameter, deciding the number of data used for training. By default, the value of Num is 25.
The trained model will be saved in file "data/model_dataX.pt" where X is replaced with the value of Num. The test accuracy will also be printed out. 

## Test
We provided 6 trained models (trained with 15, 17, ..., 25 data instances) in the data folder. You can directly check the accuracy of them on the testing data by executing the following command under this folder.
```
python test.py
```
You can also use this script to test your own trained models.

## Inference on Single Sudoku Image
We provided 6 trained models and the best model is "data/model_data25.pt", which is trained with only 25 normal Sudoku puzzles but already achieves 100% accuracy on identifying the values (empty or 1, 2, ..., 9) of a given Sudoku image. 

Given any Sudoku image generated by OpenSky Sudoku Generator, and the type of this Sudoku problem, you can use the following command to infer its solution
```
python infer.py SudokuType IMAGE
```
where SudokuType must be one of {normal, anti-knight, Sudoku-X, offset}, IMAGE must be the path to a Sudoku image. For example, you can try the following command to infer the solution of our example normal Sudoku problem in "data/sudoku.png".
```
python infer.py normal data/sudoku.png
```