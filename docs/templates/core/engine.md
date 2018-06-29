# SHAC Engine
----

The core algorithm from the paper [Parallel Architecture and Hyperparameter Search via Successive Halving and Classification](https://arxiv.org/abs/1805.10255).

This engine provides an interface similar to Scikit-Learn, with two methods - `fit` and `predict` which training and parameter sampling respectively.

The data for the classifiers is generated via rejection sampling, using Joblib for parallel batch generation and evaluation.
It even allows for halted training - such that training can resume from the previous stage without any issue.

Two important user inputs to this class are :

- Evaluation function
- Hyper Parameter list

----

## **Note**

The engine will generate samples at each epoch of training, and supply them to the evaluation function which will also be
executed in parallel. Therefore, all stages of sample generation, training, evaluation must be thread safe.

While the training algorithm can manage thread safety of the generator and training modules, the evaluation module is
for the user to write.

Therefore, we provide wrappers such as `TensorflowSHAC`, `KerasSHAC` and `TorchSHAC` to allow safer evaluation. However, this comes
at significant cost of execution, as a new Tensorflow Graph and likewise, a new Keras Session must be built for each evaluator thread.

!!!info "Serial Evaluation"
    If parallel evaluation is not preferred, please refer the [Serial Evaluation](../serial-execution.md) page.

## Class Information
----

{{autogenerated}}