# Model-PredictionAPI

The goal is to test the use of Google Prediction API for indoor location systems.
In order to achieve this:
- Generate a given number of datasets to train the models. These datasets simulate a 3 receivers and 1 transmitter. Each entry of a dataset consist on  ```[postion of transmisor, distance to receiver 1,distance to receiver 2, distance to receiver 3, power received 1, power received 2, power received 3]```
- Train Google Prediction model using the previous datasets
- Test the accurancy of the generated model. The information use to test the model is ```[distance to receiver 1,distance to receiver 2, distance to receiver 3, power received 1, power received 2, power received 3]```

## Requirements

- Node v4.0 or greater
- Google Cloud Platform account
    - Create a project
    - Download connection key file (.json)
- Activate Google Prediction API


## Workflow

### Generate datasets

The first step of the process is generate dataset of calculated values, **using the path loss formula**.  The models should be trained with samples generated using de path loss model. The input is an array wich contains the number of samples for each dataset.

```javascript
//Number of samples for each dataset
var samplesToTrain = [150,200,300,500,1000,1500,2000,2500];
```
In order to test with other number of samples there is only need to modify the ```samplesToTrain``` variable.

### Train Google Prediction Model

The program connects with the Google API server and uploads the generated models to an Existing Project.
It also checks the status of the upload. Once the Status is changed "Done" a trigger is executed to start the testing process.


### Test Accurancy

Using the ```predict``` API method each model is test a determined number of times (the number is specified in the configuration variables).
Once all the test are done the progam generates a *.json* file for each model, containing the difference between the formula and the Prediction API.

