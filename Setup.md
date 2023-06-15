
#  Setup

This guide provides instructions on the order in which our project must be set up if you wish to reproduce results or build upon our work, with references to the appropriate documentation in the relevant repositories.

1. Set up a QuestDB database and perform the data import: [QuestDB Setup](https://github.com/Sensor-Based-Activity-Recognition/docs/blob/main/Datenbank.md)
   1. In case you want to add additional data, you can use `blam` to import from .json/.csv export of the [Sensor Logger](https://www.tszheichoi.com/sensorlogger) app: [Data Preprocessing](https://github.com/Sensor-Based-Activity-Recognition/blam)
2. You can now clone the `pipeline` repo. This allows you to run and change the ML pipeline to perform experiments and train new models using `dvc` locally: [Pipeline](https://github.com/Sensor-Based-Activity-Recognition/pipelines)
   1. In case you want to set up MLOps to automatically execute the pipeline and start new experiments from `https://studio.iterative.ai/`, you can follow the instructions here to set up a GitHub Runner & Workflow [Workflow](https://github.com/Sensor-Based-Activity-Recognition/pipelines/blob/main/.github/workflows/README.md).
   2. In case you want to use dvc remote storage, you can use `dvc remote` to set up a remote storage and share it with your team [Remote Storage](https://dvc.org/doc/command-reference/remote). We self-hosted an S3 storage bucket for this project.
   3. In case you want to use Iterative Studio, create a new account on `https://studio.iterative.ai/` and link your repo.
3. For deploying a model and using our mobile app to perform activity recognition with it's classification results, deploy the [API](https://github.com/Sensor-Based-Activity-Recognition/api). Then, you can proceed to install the [Mobile App](https://github.com/Sensor-Based-Activity-Recognition/mobile-app).

Happy Activity Recognition!
