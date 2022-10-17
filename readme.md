### Represented parts (green) in the [ai pipeline](https://github.com/DRAIVE/ai-pipeline-tools-poc)

```mermaid

graph LR
    A[<font color=black>Dataset Management] -->|training data| B[<font color=black>Model Training]
    A -->|validation data| C[<font color=black>Model Validation]
    B --> |model| C[<font color=black>Model Validation]
    C:::covered -->|validated model| D[<font color=black>Model Deployment]
    C --> |parameters| E[<font color=black>Experiment & Performance Tracking]
    B:::covered --> |parameters|E[<font color=black>Experiment & Performance Tracking]
    D --> F(<font color=black>Model)
    E:::covered --> G(<font color=black>Model Description)

    classDef covered fill:#04db48, stroke:#000000;
    classDef default fill:#cfcfcf, stroke:#000000;

```
# ai-pipeline-mlflow-poc

## Context

This is a proof of concept created to verify the MLFLow tool's functionality to handle the experiment tracking and comparison. The YOLOv5 object detection model is used here. Another DVC repo which was parallelly created to handle DVC for dataset management is used for accessing(S3) the versioned dataset for training. Both the YOLOv5 and DVC-dataset repos are embedded as sub-directories to this repo. The training and validation stages are handled using a DVC pipeline and mlflow handles the experiment tracking.

## Usage

Steps:
- Clone the repo to a local machine
- Go to the dvc-dataset submodule under data directory
- Add the s3 credentials using dvc [commands](https://dvc.org/doc/command-reference/remote/modify#--local)
- Do 'dvc pull' to download the dataset. (The version of the dataset corresponds to the commit of the repo)
- Comeback to main directory and run the pipeline using 'dvc repro'.
- Use mlflow [commands](https://mlflow.org/docs/latest/cli.html#mlflow-ui) to visualize different runs.