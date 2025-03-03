---
description: Documentation on how to export a Python model to the model registry
---

# How To Export a Python Model

## Introduction

In this guide you will learn how to export a generic Python model and register it in the Model Registry.

## Code

### Step 1: Connect to Hopsworks

=== "Python"
    ```python
    import hopsworks

    project = hopsworks.login()

    # get Hopsworks Model Registry handle
    mr = project.get_model_registry()
    ```

### Step 2: Train

Define your XGBoost model and run the training loop.

=== "Python"
    ```python
    # Define a model
    model = XGBClassifier()

    # Train model
    model.fit(X_train, y_train)
    ```

### Step 3: Export to local path

Export the XGBoost model to a directory on the local filesystem.

=== "Python"
    ```python
    model_file = "model.json"

    model.save_model(model_file)
    ```

### Step 4: Register model in registry

Use the `ModelRegistry.python.create_model(..)` function to register a model as a Python model. Define a name, and attach optional metrics for your model, then invoke the `save()` function with the parameter being the path to the local directory where the model was exported to.

=== "Python"
    ```python
    # Model evaluation metrics
    metrics = {'accuracy': 0.92}

    py_model = mr.python.create_model("py_model", metrics=metrics)

    py_model.save(model_dir)
    ```

## Going Further

You can attach an [Input Example](../input_example.md) and a [Model Schema](../model_schema.md) to your model to document the shape and type of the data the model was trained on.
