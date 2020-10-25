# pyTorch_Lightning_tutorial


This guide will walk you through the core pieces of PyTorch Lightning.

   We’ll accomplish the following:

     Implement an MNIST classifier.

     Use inheritance to implement an AutoEncoder
     
     
## Installing Lightning
  Lightning is trivial to install. We recommend using conda environments

      
      -$ pip install pytorch-lightning
      
## The Model
The LightningModule holds all the core research ingredients:

  The model

    The optimizers

    The train/ val/ test steps
