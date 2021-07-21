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

NVIDIA GPU Operator allows running of pods of NVIDIA GPUs, while Kubeflow provides TFJob custom resource definition (CRD) that allows distribution of ML data via TensorFlow across multiple nodes. Instructions on installation of NVIDIA GPU Operator are [here](https://docs.nvidia.com/datacenter/kubernetes/openshift-on-gpu-install-guide/index.html#openshift-gpu-support-install-via-operatorhub). Kubeflow can be installed [manually](https://www.kubeflow.org/docs/distributions/openshift/install-kubeflow/) or via installation of Open Data Hub operator.

**Quay repository account and robot access**

Create an account in [quay.io](quay.io). Once account is setup, on the top right click "Create New Repository" and create a "Container Image Repository" with a name of "matmul", set it to public, choose empty repository and click "Create Public Repository".

Now let's set up the robot that will allow access to repositories. On top right, click on username, then "Account Settings". On the left, click on the image of a robot, then on the right "Create Robot Account". Then, fill in "build" for a name and provide description if desired and click "Create Robot Account". Choose all repositories that need to be accessed. In this case, it is only "matmul", whose permissions need to be set "Write" and click "Add permissions". This robot now will facilitate push, pull access to your repository.
