## Sleep Stages Challenge

This project stemmed from a [Kaggle competition](https://www.kaggle.com/competitions/child-mind-institute-detect-sleep-states/) hosted by Child Mind Institute.
The purpose of the project is to create an ML model that is cabale of detecting onset and wakeup time using accelerometer data.

## Installation and Setup Instructions

#### Dependencies:  

Clone down this repository. There are multiple python libraries used throughout the code all of which need to be installed.
The libraries are:
- pytorch
- numpy
- matplotlib
- pandas

#### Data: 
Unfortunately, the data files are too large for a normal repository. Also, I am not sure I am allowed to include them in a public repository. For those reasons, the data must be installed separately. 

You can download the data directly from Kaggle [here](https://www.kaggle.com/competitions/child-mind-institute-detect-sleep-states/data/). You can download the data in any directory.

Once you have the data downloaded, create a new folder and name it `data_path` and inside of it, create a new python file and name it `data_path.py`. Inside of the newly created python file, create a string named `dataPath` and assign to it the data path of the folder containing your data.

#### Other needed directories:
The last step is to create a folder named `batched_data` which is where your tensors of batched data will be downloaded after running the code.

#### Running the code:
The only 2 files that need to be run for the model to work are:
- `batching.ipynb`
- `resize_batched_data.ipynb`
- `training.ipynb`
These are all located in the `essential files` folder. You should run all cells in each file in the order of files shown above.

If you would like to see some of the data visualizations used in the development you are free to run files in the `suplumentary files' folder.

## Development process and scope:

#### Data Manipulation and Visualization:
[^1]The first step was to better understand the data. After loading the files onto dataframes using Pandas, the tables looked like this:

![image](https://github.com/yotamfre/Sleep-Stage-Challenge/assets/66326758/d4569511-239e-48d8-8972-7a51d022a101)

![image](https://github.com/yotamfre/Sleep-Stage-Challenge/assets/66326758/97b9b2d6-98b4-436d-8d2a-f17eec4e7278)

The first table is containing the features while the the second table contains the labels. The first step was to merge the 2 tables over step, timestamp and series_ID using a left merge. For development purposes, `sample_data` can be set to True which would perform the merge for only 10 different people's data.
After that, the following [^2]graphs were created using the 30 minute intervals around an event:

![image](https://github.com/yotamfre/Sleep-Stage-Challenge/assets/66326758/6b13e515-1a1b-41ef-8245-da7060bcd6e2)

![image](https://github.com/yotamfre/Sleep-Stage-Challenge/assets/66326758/171a5628-91dd-4d15-9048-d6c23fdb7e7d)

These figures demonsttarate that there is a significant change during this interval around the event.

In order to fit the data to a model, it had to be cleaned first. First, the begining and end of each different individulas measurments were cut off so that every person had data that divided to a whole number of series'. Then, Labels had to be made. Because the given dataset originated from sleep logs, the exact timestamp of the event is unreliable. Because of this, it would be difficult to constract a model that predicts the exact time when an event occured. Instead, it would be wiser to create a model that predicts weather or not the person is awake for any given timestamp. It was chosen that the labels will have the same dimenstion as the series length with 0's representing an awake state while 1's represented a state of sleep.

####The Model:
The model chosen was an Long Short Term Memory model. This is because LSTM's have a design well suited for timeseries problems like this. However, 24 hours worth of data is too much context for an LSTM to learn on in this case. Because of this it was decided to use a period of 1 hour around a label with the label being at a random spot throughout the series.

![image](https://github.com/yotamfre/Sleep-Stage-Challenge/assets/66326758/daad0cde-deda-43a5-88ca-80454f47e84b)

This approach worked because after training the model the follwing results were achieved:

![image](https://github.com/yotamfre/Sleep-Stage-Challenge/assets/66326758/01531a66-ebe0-4741-ac30-bab7fdd81d41)

![image](https://github.com/yotamfre/Sleep-Stage-Challenge/assets/66326758/cccbf7ec-3a45-4166-83f8-d6f73417bfe7)

![image](https://github.com/yotamfre/Sleep-Stage-Challenge/assets/66326758/8453be11-6b06-4250-b5dc-db19f708927c)

[^1]: To understand the structure of the dataset, click [here](https://www.kaggle.com/competitions/child-mind-institute-detect-sleep-states/data/).
[^2]: These graphs can be seen in graphs.ipynb. 
