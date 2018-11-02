## SageMaker Notes

### Overview

* https://aws.amazon.com/sagemaker/
* https://aws.amazon.com/sagemaker/features/

Intent:  Improve the process of ML modeling, by providing Build, Train, and Deploy modules:


* Build:
  * hosted Jupyter notebooks
  * allow connecting directly to data in S3
  * set of "built-in", performance optimized ML algorithms
  * pre-configured to run TensorFlow, Apache MXNet, and Chainer
     * allow local mode script testing via Python SDK
  * allow using custom ML framework

* Train
  * simplify training proces by managing infrastructure and scaling
  * automatic model tuning

* Deploy
  * real-time or batch prediction support
  * auto-scaling
  * A/B testing support


### Developer Guide

* https://docs.aws.amazon.com/sagemaker/

#### How It Works

#### Getting Started

Walkthrough Steps

* create an S3 bucket to store model training data and model artifacts
    * include `sagemaker` in the name of the bucket
* create a notebook instance
    * Services -> SageMaker -> Notebook Instances -> Create notebook instance.
    * Set the following properties:
        * Notebook instance name: ""
        * Instance Type: ml.t2.medium
    * Create an associated IAM role:
        * IAM role -> Create a new role
        * S3 buckets you specify: "None"
        * Create role
    * Create notebook instance

#### Using Notebook Instances

Steps taken by SageMaker when a noteook instance create request is received:

* Creates a network interface
* Launches an ML compute instance
* Installs Anaconda packages and libraries for common deep learning platforms
  * Anaconda installer
  * TensorFlow
  * Apache MXNet
* Attaches an ML storage volume
  * 5 GB ML storage volume (persistent)
  * 20 GB instance storage (ephemeral)
* Copies example Jupyter notebooks

Access to notebooks can be limited to specific IP addresses

Notebook can be accessed via:

* Console -> Open action
* API -> CreatePresignedNotebookInstanceURL

Using Example Notebooks

* they use the `nbexamples` Jupyter extensions
* https://github.com/danielballan/nbexamples


Set Notebook Kernel

* Options
  * Python 2
  * Python 3
  * MXNet
  * TensorFlow
  * PySpark
  
Installing External Libraries and Kernels in Notebook Instances

* Provides ability to install custom environments, packages, and kernels
* e.g. R, Scala
* Scala : note that instructions don't work -- they don't match the structure of the downloaded scalal kernel repo


Resume @ "Using Built-in Algorithms with Amazon SageMaker"
