
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
