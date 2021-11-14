# Cifar-10 Experiment

## Environment Settings

This project was set up with random number seeds to ensure reproducible results. The basic experimental environment setup is shown below.

- model: Resnet34
- batch size: 128
- epoch: 100
- criterion: cross entropy
- optimizer: SGD
  - learning rate: [1e-4, 1e-3, 1e-2]
  - momentum: 0.9
- ratio of validation: 0.2

## Transform

- training setting

```python
transforms.RandomCrop(32, padding=4),
transforms.RandomHorizontalFlip(),
transforms.RandomGrayscale(),
transforms.ToTensor(),
transforms.Normalize([0.4914, 0.4822, 0.4465],
                         [0.2023, 0.1994, 0.2010])
```

- test setting

```python
torchvision.transforms.ToTensor(),
torchvision.transforms.Normalize([0.4914, 0.4822, 0.4465],
							   [0.2023, 0.1994, 0.2010])
```

- display

  Let's see what some of the photos look like after pre-processing, they look a bit peculiar.

  ![](https://raw.githubusercontent.com/mrk-lyz/images/master/img/202111142006563.png)

## Results

Let us focus on the effect of the `learning rate` hyperparameter on the training results.

- 1e-4

  - loss

    min training loss : 0.1677, min validation loss: 0.5577 

    ![loss_lr_0.0001](https://raw.githubusercontent.com/mrk-lyz/images/master/img/202111142016314.png)

  - acc

    max training acc : 0.9413, max validation acc: 0.83 

    ![acc_lr_0.0001](https://raw.githubusercontent.com/mrk-lyz/images/master/img/202111142016454.png)

    We can clearly see that there is an **underfitting** in the figure, the loss and accuracy are NOT converged yet.

- 1e-3
  
  loss = 0.46518, acc = 0.89930
  
  - loss
  
    min training loss : 0.0226, min validation loss: 0.4248 
  
    ![loss_lr_0.001](https://raw.githubusercontent.com/mrk-lyz/images/master/img/202111142018834.png)
  
  - acc
  
    max training acc : 0.9929, max validation acc: 0.8956 
  
    ![acc_lr_0.001](https://raw.githubusercontent.com/mrk-lyz/images/master/img/202111142018298.png)
  
    Although the accuracy on the training set keeps improving, it stays the same on the validation set.
  
- 1e-2
  - loss
  
    min training loss : 0.0523, min validation loss: 0.3331
  
    ![loss_lr_0.01](https://raw.githubusercontent.com/mrk-lyz/images/master/img/202111142039256.png)
  
  - acc
  
    max training acc : 0.9826, max validation acc: 0.9113
  
    ![acc_lr_0.01](https://raw.githubusercontent.com/mrk-lyz/images/master/img/202111142040917.png)
  
    The model converges at a very fast speed.

## Results

The model trained using a learning rate of 0.01 has an accuracy of **0.9123** on the test set. More details can be found in `main.ipynb`.

