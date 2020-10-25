# pyTorch_Lightning_tutorial
      PyTorch Lightning is a lightweight PyTorch wrapper that helps you scale your models and write less boilerplate code. In this Tutorial we learn about this framework and how we can convert our PyTorch code to a Lightning code.
   Organizing your code with PyTorch Lightning makes your code:

      Keep all the flexibility (this is all pure PyTorch), but removes a ton of boilerplate

      More readable by decoupling the research code from the engineering

      Easier to reproduce

      Less error prone by automating most of the training loop and tricky engineering

      Scalable to any hardware without changing your model

Lightning is nothing more than organized PyTorch code, so once you’ve organized it into a LightningModule, it automates most of the training for you.The beauty of Lightning is that it handles the details of when to validate, when to call .eval(), turning off gradients, detaching graphs, making sure you don’t enable shuffle for val, etc…



This guide will walk you through the core pieces of PyTorch Lightning.

   We’ll accomplish the following:

     Implement an MNIST classifier.

     Use inheritance to implement an AutoEncoder
     
     
##  Step 0: Installing Lightning
  Lightning is trivial to install. We recommend using conda environments

      
      -$ pip install pytorch-lightning
## Step 1: Define LightningModule
      FORWARD vs TRAINING_STEP

      In Lightning we separate training from inference. The training_step defines the full training loop. We encourage users to use the forward to define inference actions.
## The Model
The LightningModule holds all the core research ingredients:

  The model

    The optimizers

    The train/ val/ test steps
## Step 2: Fit with Lightning Trainer
   First, define the data however you want. Lightning just needs a DataLoader for the train/val/test splits.
      # init model
      autoencoder = LitAutoEncoder()

      # most basic trainer, uses good defaults (auto-tensorboard, checkpoints, logs, and more)
      # trainer = pl.Trainer(gpus=8) (if you have GPUs)
      trainer = pl.Trainer()
      trainer.fit(autoencoder, train_loader)
      
   The Trainer automates:

      Epoch and batch iteration

      Calling of optimizer.step(), backward, zero_grad()

      Calling of .eval(), enabling/disabling grads

      Saving and loading weights

      Tensorboard (see Loggers options)

      Multi-GPU training support

      TPU support

      16-bit training support
      
 ### Using CPUs/GPUs/TPUs
   It’s trivial to use CPUs, GPUs or TPUs in Lightning. There’s NO NEED to change your code, simply change the Trainer options.

      # train on CPU
      trainer = pl.Trainer()
      # train on 8 CPUs
      trainer = pl.Trainer(num_processes=8)
      # train on 1024 CPUs across 128 machines
      trainer = pl.Trainer(
          num_processes=8,
          num_nodes=128
      )
