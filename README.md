# Distributed GPU multi-node TensorFlow model training in RHODS

This is a simple example that demonstrates how to train a neural network model on MNIST dataset in Red Hat OpenShift Data Science (RHODS) using several GPU nodes.

The example is intended for Data Scientists or so that would like to take advantage of several GPU nodes on RHODS while training their model with TensorFlow. [RHODS](https://www.redhat.com/en/blog/introducing-red-hat-openshift-data-science) is an add-on service to Red Hat OpenShift managed cloud services that provides a sandbox environment for data scientists to develop, train and test machine learning models and deploy them for use in intelligent applications.

PyTorch version of this example is in the works.

Part of the instructions and Dockerfiles were adopted from a Red Hat [blog](https://www.openshift.com/blog/using-the-nvidia-gpu-operator-to-run-distributed-tensorflow-2.4-gpu-benchmarks-in-openshift-4) with modifications.

## Prerequisites
**OpenShift cluster and OpenShift 4.x**

This example was tested and developed on Red Hat OpenShift Dedicated cluster with OpenShift 4.7.19 running in AWS. An OpenShift cluster with at least OpenShift 4.5 is recommended.

**Red Hat OpenShift Data Science (RHODS)**

RHODS Operator needs to be installed. RHODS Operator 1.0.14 was used for this example.

**NVIDIA GPU Operator and Kubeflow**

NVIDIA GPU Operator allows running of pods of NVIDIA GPUs, while Kubeflow provides TFJob custom resource definition (CRD) that allows distribution of ML data via TensorFlow across multiple nodes. Instructions on installation of NVIDIA GPU Operator are [here](https://docs.nvidia.com/datacenter/kubernetes/openshift-on-gpu-install-guide/index.html#openshift-gpu-support-install-via-operatorhub). Kubeflow can be installed [manually](https://www.kubeflow.org/docs/distributions/openshift/install-kubeflow/) or via installation of [Open Data Hub operator](https://opendatahub.io/docs/kubeflow/installation.html).

## Run
**Navigate to RHODS and initiate a JupyterLab notebook**

**1.** In the Cluster Overview dashboard, select `Red Hat OpenShift Data Science` under `OpenShift Managed Services`:

![Screenshot from 2021-07-23 15-59-14](https://user-images.githubusercontent.com/43946617/126835242-650c12a5-8d88-497b-a1a9-270da17ef6a5.png)


**2.** Launch JupyterHub notebook server:

![Screenshot from 2021-07-23 16-03-54](https://user-images.githubusercontent.com/43946617/126835550-76bbc280-8a13-4477-aa86-46ff49a953a5.png)


**3.** Start server with `TensorFlow` notebook image, `default` container size and `0` number of GPUs. Zero GPUs are selected since the training itself will run directly on the cluster (ie. outside of JupyterLab notebook), while the JupyterLab notebook server can run on any node blind to its CPU or GPU hardware.

![Screenshot from 2021-07-23 16-13-18](https://user-images.githubusercontent.com/43946617/126837225-b6381087-c99c-4321-b876-1792914c41f8.png)


**4.** Clone this repository (https://github.com/heyselbi/rhods-tf-multi-node.git) and open `tf-distributed.ipynb`:

![Screenshot from 2021-07-23 16-22-17](https://user-images.githubusercontent.com/43946617/126837650-b28920ff-ebc6-4c45-a870-5306317a195f.png)



**Update the parameters and run the training on JupyterLab notebook**

**1.** Return to Cluster Overview dashboard, under question mark logo on top right, click on `Command Line Tools` --> `Copy Login Command` --> (might need to login before this) `Display Token` --> copy what's under the login token that starts with `oc login --token=sha...`. Replace the cell 1 of `tf-distributed.ipynb` with your login token.

![Screenshot from 2021-07-23 16-35-02](https://user-images.githubusercontent.com/43946617/126839128-b7dddfa3-0324-4a7b-a8ea-c6c03d9c4d46.png)


**2.** Follow the instructions in `tf-distributed.ipynb`.


## Advanced topic
**How to check available NVIDIA GPUs on the OpenShift cluster and monitor their usage**

TBD
