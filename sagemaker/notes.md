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
* Scala : note that instructions in docs don't work, see the following for updated instructions:

```
git clone https://github.com/jupyter-scala/jupyter-scala.git

cd jupyter-scala

./scripts/coursier.sh bootstrap \
    -i user -I user:sh.almond:scala-kernel-api_$SCALA_VERSION:$ALMOND_VERSION \
    sh.almond:scala-kernel_$SCALA_VERSION:$ALMOND_VERSION \
    -o almond
    
./almond --install
```

#### Using Built-in Algorithms with Amazon SageMaker

* several algorithms provided built-in to SageMaker
* supervised examples:
  * for classification:
    * Linear Learner: `predictor_type = binary_classifier`
    * XGBoost: `objective = reg:logistic`
  * for regression:
    * Linear Learner: `predictor_type = regressor`
    * XGBoost: `objective = reg:linear`
  * discrete recommendations:
    * Factorization Machine
* unsupervised examples:
  * K-Means
  * PCA
* specific use case examples:
  * Image Classification Algorithm
  * Sequence to Sequence
  * Latent Dirichlet Allocation (LDA)
  * Neural Topic Model (NTM)
  
* For each algorithm, there is a Docker Registry path to the image for that algorithm.

#### Common Data Formats

* Many accept CSV for training; in that case, specify `text/csv` for `ContentType`
  * don't include header
  * target variable must be in first column
  * For unsupervised learning: `label_size=0`
* optimized protobuf recordIO format allows using "Pipe mode" to train
  * streaming data during training
  * rather than loading all at once as in "File mode"
  * allows reducing the size of the EBS volume needed
  * Pipe mode: only need enough EBS space to store final model artifacts
  * File mode: needs enough EBS space to store produced artifacts _and_ training data

#### Trained Model Deserialization

* stored as `model.tar.gz` in output S3 bucket
* within that file is a `model_algo-1` containing the serialized model object
* [ ] try reloading an XGBoost serialized model outside of the notebook
