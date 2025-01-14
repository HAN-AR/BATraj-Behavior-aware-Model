# BAT: Behavior-Aware Human-Like Trajectory Prediction for Autonomous Driving

This repository contains the official implementation of  **BAT: Behavior-Aware Human-Like Trajectory Prediction for Autonomous Driving**, accepted by the Association for the Advancement of Artificial Intelligence (AAAI) 2024.

## Highlights
- Introducing a real-time dynamic geometric graph method for the continuous representation of driving behavior in trajectory prediction for autonomous driving.
- Pioneering a pooling strategy that aligns with human observation instincts by capturing the location of traffic agents using polar coordinates.
- Introducing the MoCAD dataset with its unique right-hand-drive system and mandatory left-hand driving, enriching trajectory prediction studies in complex urban and campus scenarios.
- The proposed model demonstrates exceptional robustness and adaptability in various traffic scenarios, including highways, roundabouts, campuses, and busy urban locales.
  

## Background

The ability to accurately predict the trajectory of surrounding vehicles is a critical hurdle to overcome on the journey to fully autonomous vehicles. To address this challenge, we pioneer a novel behavior-aware trajectory prediction model (BAT) that incorporates insights and findings from traffic psychology, human behavior, and decision-making. Our model consists of behavior-aware, interaction-aware, priority-aware, and position-aware modules that perceive and understand the underlying interactions and account for uncertainty and variability in prediction, enabling higher-level learning and flexibility without rigid categorization of driving behavior. Importantly, this approach eliminates the need for manual labeling in the training process and addresses the challenges of non-continuous behavior labeling and the selection of appropriate time windows. We evaluate BAT's performance across the Next Generation Simulation (NGSIM), Highway Drone (HighD), Roundabout Drone (RounD), and Macao Connected Autonomous Driving (MoCAD) datasets, showcasing its superiority over prevailing state-of-the-art (SOTA) benchmarks in terms of prediction accuracy and efficiency. Remarkably, even when trained on reduced portions of the training data (25%), our model outperforms most of the baselines, demonstrating its robustness and efficiency in predicting vehicle trajectories, and the potential to reduce the amount of data required to train autonomous vehicles, especially in corner cases. In conclusion, the behavior-aware model represents a significant advancement in the development of autonomous vehicles capable of predicting trajectories with the same level of proficiency as human drivers.
[![image](https://github.com/Petrichor625/BATraj-Behavior-aware-Model/blob/main/Figures/hudu2.png)


## Our model
Architecture of behavior-aware trajectory prediction model
![image](https://github.com/Petrichor625/BATraj-Behavior-aware-Model/blob/main/Figures/Framework3.png)

This model comprises of four innovative modules - a behavior-aware module, an interaction-aware module, a priority-aware module, and a position-aware module - each designed to enhance the sophistication and nuance of the model's understanding of driver behavior and vehicle interactions on the road.

**The behavior-aware module**, in particular, is a key component of this model. Instead of resorting to a simplistic classification of behaviors into two or three distinct typologies, it utilizes a continuous representation of behavioral information, rooted in dynamic geometric graph theory, to offer unparalleled flexibility and scalability in dynamic driving contexts. This allows autonomous vehicles to anticipate and respond to the actions of other drivers more intricately and elaborately. 

**The interaction-aware module**, on the other hand, takes into account the interactions between the AV and other vehicles in the environment, utilizing Long Short-Term Memory Networks (LSTMs) encoder to process historical track information for the ego vehicle and surrounding vehicles, thus enabling the ego vehicle to have a better understanding of the potential interactions with other vehicles. 

**The priority-aware module** evaluates the importance of different vehicles and allows the ego vehicle to prioritize its attention and response to certain vehicles over others, based on their relevance to the ego vehicle's trajectory. 

**The position-aware module** encodes and learns the dynamic location of the ego vehicle, providing additional context for the prediction of the ego vehicle's trajectory. Furthermore, we introduce a Polar coordinate system to accommodate the relative distance among various vehicles and scenes, which provides a flexible way to adapt to heterogeneous input data.


## To-do List

###### **Note**

- [x] [2023.5.25] Creating the repository for BAT
- [x] [2023.8.05] Open source BAT code
- [x] [2023.11.28] Update Readme
- [x] [2023.12.09] Update project code
- [x] [2024.3.14] Update visualization code (See more details in our new work HLTP)


## Install

The model install in Ubuntu 20.04, cuda11.7

**1. Clone this repository**: clone our model use the following code 

```
git clone https://github.com/Petrichor625/BATraj-Behavior-aware-Model.git Behavior_aware
cd Behavior_aware
```

**2. Implementation Environment**: The model is implemented by using Pytorch. It is recommended to use a virtual environment or anaconda. The original repo contains instructions for conda to create and install some packages.  
Here the instuctions for Python venv on ubuntu:
1. Install python 3.8 and venv
   ```
   sudo apt install python3.8 -y
   sudo apt install python3.8-venv -y
   ```
2. Create virtual environment with Python 3.8
   ```
   python3.8 -m venv venv
   ```
3. Activate it
   ```
   source venv/bin/activate
   ```
4. Install CUDA/CuDNN
   ```
   sudo apt-get install libcudnn8=8.5.0.*-1+cuda11.7
   sudo apt-get install libcudnn8-dev=8.5.0.*-1+cuda11.7
   ```
5. Install PyTorch
   ```
   pip install torch==1.13.1+cu117 torchvision==0.14.1+cu117 torchaudio==0.13.1 --extra-index-url https://download.pytorch.org/whl/cu117
   ```
5. Install requirements
   ```
   pip install -r requirements.txt
   ```
6. Download NGSIM processed data  
   Pre-processed NGSIM data is expected for training, so download from the [original repo releases](https://github.com/Petrichor625/BATraj-Behavior-aware-Model/releases/tag/NGSIM)



## Download and Pre-processing Datasets

Before starting the training process,   you can choose one of the datasets to train the model,  and you need to prepare the dataset and follow the steps below.



**a. Next Generation Simulation (NGSIM) Dataset**

<u>The esteemed NGSIM dataset is available at the Releases in this repository.</u>

###### **Note**

1. [2023.5.25] Like the baselines, the NGSIM dataset in our work is segmented in the same way as in the most widely used work [Deo and Trivedi, 2018], so that comparisons can be made.

2. [2023.5.25] The maneuver-based test set is only a true subset of the overall test set. We select well-defined maneuvers from the overall test set and divide them into the maneuver-based test set, omitting some unknown maneuvers such as zigzag driving, tentative driving, etc.


**b. Highway Drone (HighD) Dataset**

HighD is a new dataset of naturalistic vehicle trajectories recorded on German highways. Using a drone, typical limitations of established traffic data collection methods such as occlusions are overcome by the aerial perspective. Traffic was recorded at six different locations and included more than 110 500 vehicles. It provides both the full dataset and the sample version of the dataset for testing purposes. We also train and test our models in the highD dataset.

Due to the policy requirements of this dataset, please request and download the **HighD** dataset from the  HighD official [website](https://www.highd-dataset.com/). Normally, applications take 7-14 working days to be approved.

After downloading the dataset,  please put all your dataset files in the directory named `HgihD` (in the folder 'dataset'), and then you then run the following MATLAB script to process the raw data:

```
HighD_preprocess.m
```



###### Node

[2023.5.25] The HighD dataset in our work is segmented in the same way as the work ([stdan](https://ieeexplore.ieee.org/document/9767719))



**c.  Roundabout Drone (RounD) Dataset**

The rounD dataset is a new dataset of naturalistic road user trajectories recorded at German roundabouts. Using a drone, typical limitations of established traffic data collection methods like occlusions are overcome. Traffic was recorded at three different locations. The trajectory for each road user and its type is extracted.

To further evaluate the performance of our model in some complex and non-regularized scenes, such as roundabouts, and irregular intersections, we also train our model in the rounD dataset.



Due to the policy requirements of this dataset, please request and download the **RounD** dataset from the  RounD official [website](https://www.round-dataset.com/). Normally, applications also take 7-14 working days to be approved.

After downloading the dataset,  please put all your dataset files in the directory named `RounD` (in the folder 'dataset'), and then you then run the following MATLAB script to process the raw data:

```
rounD_preprocess.m
```



## Train 

In this section, we will explain how to train the model.

Please keep your model in a file named `models` and change your hyperparameter in models.py

###### Note

You can view or change the network parameters from the `model_args.py` file

##### Begin to Train

```
python3 train.py
```

The training logs will keep in the file name `Train_logs`, you can use tensorboard to check your training process.

```
tensorboard --logdir /YourPath/Train_log/yourmodel
```

**Save trained model**

In addition, the trained model will be stored in the path you set, which can be set from the `model_fname` in the `train.py` file 

```
model_fname = 'path/to/save/model'
```



## Evaluation

This step helps you assess how well the model generalizes to unseen data and allows you to make any necessary adjustments or improvements. If the model does not meet your desired performance criteria, you can iterate on the training process by adjusting hyperparameters, modifying the model architecture, or collecting additional data.

Once the model has been trained, it is important to evaluate its performance on a separate validation or test set. This step helps assess how well the model generalizes to unseen data. You can choose to evaluate the model using either the validation set (val) or the test set (the overall tested set or the maneuver-based dataset) by setting the test_dataset_files and test_cases . 

```
(Here is just a sample NGSIM dataset, you can modify it to suit your needs)
test_dataset_files = ['TestSet', 'TestSet_keep', 'TestSet_merge', 'TestSet_left',  'TestSet_right']
test_cases = ['overall', 'keep', 'merge', 'left', 'right']
```

Please set the path of your trained model in net_fname in evlauate.py

```
net_fname = 'path/to/save/model'
```

To evaluate the model on the validation or test set, run the following command:

```
python evaluate.py 
```

Finally, the evaluation results will be saved as a .csv file and stored in the path you have predefined in eval_fname

```
eval_fname ='path/to/save/results'
```



## Qualitative results

We are preparing a script for generating these visualizations:

 ````
 Code for qualitative results coming soon
 ````
 ![image](https://github.com/Petrichor625/BATraj-Behavior-aware-Model/blob/main/Figures/Qualitative%20results.gif)


## Main contributions

This work aims to introduce a novel **lightweight and map-free model** that eliminates the need for labor-intensive high-definition (HD) maps and costly manual annotation by using only historical trajectory data in the polar coordinate system and a DGG-based method to capture continuous driving behavior. It can be summarized as follows:

1. We present a novel dynamic geometric graph approach that eliminates the need for manual labeling during training. This method addresses the challenges of labeling non-continuous behaviors and selecting appropriate time windows, while effectively capturing continuous driving behavior. Inspired by traffic psychology, decision theory, and driving dynamics, our model incorporates centrality metrics and behavior-aware criteria to provide enhanced flexibility and accuracy in representing driving behavior. To the best of our knowledge, this is the first attempt to incorporate **continuous representation** of behavioral knowledge} in trajectory prediction for AVs.
2. We propose a novel pooling mechanism, aligned with human observational instincts, that extracts vehicle positions in **polar coordinates**. It simplifies the representation of direction and distance in Cartesian coordinates, accounts for road curvature, and allows modeling in complex scenarios such as roundabouts and intersections.
3. We introduce a new Macao Connected Autonomous Driving (MoCAD) dataset, sourced from a L5 autonomous bus with over 300 hours across campus and busy urban routes. Characterized by its unique **right-hand-drive system**, MoCAD, set to be publicly available, is pivotal for research in right-hand-drive dynamics and enhancing trajectory prediction models.
4. Our model significantly outperforms the SOTA baseline models when tested on the NGSIM, HighD, RounD, and MoCAD datasets, respectively. Remarkably, it maintains impressive performance even when trained on only **25.0% of the dataset**, demonstrating exceptional robustness and adaptability in various traffic scenarios, including **highways**, **roundabouts**, and **busy urban locales**.



## Citation
**BAT: Behavior-Aware Human-Like Trajectory Prediction for Autonomous Driving**, proceeding on the Association for the Advancement of Artificial Intelligence (AAAI) 2024. (Camera-ready)

```
@misc{liao2023bat,
      title={BAT: Behavior-Aware Human-Like Trajectory Prediction for Autonomous Driving}, 
      author={Haicheng Liao and Zhenning Li and Huanming Shen and Wenxuan Zeng and Guofa Li and Shengbo Eben Li and Chengzhong Xu},
      year={2023},
      eprint={2312.06371},
      archivePrefix={arXiv},
      primaryClass={cs.RO}
}
```
 


