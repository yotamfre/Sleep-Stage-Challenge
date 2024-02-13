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

#### Data Visualization:
[^1]The first step was to better understand the data. After loading the files onto dataframes using Pandas, the tables looked like this:

![image](https://github.com/yotamfre/Sleep-Stage-Challenge/assets/66326758/d4569511-239e-48d8-8972-7a51d022a101)

![image](https://github.com/yotamfre/Sleep-Stage-Challenge/assets/66326758/97b9b2d6-98b4-436d-8d2a-f17eec4e7278)

The first table is containing the features while the the second table contains the labels. The first step was to merge the 2 tables over step, timestamp and series_ID using a left merge. For development purposes, `sample_data` can be set to True which would perform the merge for only 10 different people's data.

[^1]: To understand the structure of the dataset, click [here](https://www.kaggle.com/competitions/child-mind-institute-detect-sleep-states/data/).
