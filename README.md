# ATTENTION BASED ROAD SEGMENTATION

The paper we are trying to implement is based on structure-guided lane detection for autonomous vehicles. The original datasets used by the authors are the **CU Lane** and the **TuSimple** datasets. Both these datasets are very big and computationally expensive to work on. For our purposes we will be using the **KITTI Road dataset** published by Karlsruhe Institute of Technology. The link to the original dataset is: http://www.cvlibs.net/datasets/kitti/eval_road.php

We have used a smaller version of this dataset from the link: https://www.kaggle.com/datasets/sumanyughoshal/kitti-road-dataset.

## DETAILS ABOUT THE DATASET:

The KITTI Road dataset that we are using consists of 289 training images and 290 test images. It contains three different categories of road scenes:
   * uu - urban unmarked (98 training/100 test)
   * um - urban marked (95 training/96 test)
   * umm - urban multiple marked lanes (96 training/94 test)
   
The 289 training examples are accompanied by their labels in the form of ground truth masks. The 290 test examples however, come without labels. In the following section, we would be answering a few questions regarding the dataset.


### Is the dataset balanced?

The dataset is fairly well balanced for an urban scenario. As mentioned above, there are almost a hundred different examples of each of the three types of lanes: unmarked, marked and multiple marked. One example from each of the three scanarios have been displayed below


### Why is the dataset relevant to our chosen paper?
​
The paper chosen by us tries to address three main difficulties of the lane detection task. These difficulties are:
* Characterizing lanes based on different methods of annotations.
* Identification and modelling of relationship between surrounding scene and lanes.
* Supporting more attributes of the scene to come up with better results while detecting lanes.

The paper proposes a novel structure guided framework, **SGNet** to address the above mentioned difficulties. A new lane representation is introduced and a top-down vanishing point guided mechanism is proposed. Hence our chosen dataset is relevant to the paper because:
* This dataset characterizes lanes differently as compared to the CULane and TuSimple datasets. The CULane and TuSimple datasets annotate lane boundaries based on the co-ordinates of the lane markings. This dataset, however, follows a segmentation based annotation approach in which not only the lane boundaries, but the entire lane is shown as a separate entity from other entities of a constituent scene. Hence it uses a different approach for annotation.
* For identification and modelling of the relationship between surrounding scenes and lanes, it is desired for the scenes around the lanes to be very diverse. Our chosen dataset satisfies this condition too as it depicts a variety of urban scenarios and structures surrounding the lanes.
* For supporting more attributes of the scene to come up with a better lane segmentation, it is important for a large number of attributes to be present in the data. The field of view of our chosen dataset is large enough and has captured various attributes like surrounding vehicles, buildings, walls and other obstructions

### What are the limitations of this dataset?

The major limitation of this dataset is its size. With less than 300 number of training images, it is very hard to make a model generalize well based on this data. Besides this, the majority of the data consists of images taken during the daytime. It should also be noted that the dataset consists of picture from an urban scenario only, a rural scenario may or may not be a different story depending on some specific cases.

# OVERCOMING THE LIMITATIONS

To overcome working with only 289 training examples, we have used a library, *Automold*, which has been made specifically for this purpose. The link to the Automold library is: https://github.com/UjjwalSaxena/Automold--Road-Augmentation-Library

We have used functions from Automold to introduce special augmentations like the introduction of fog, snow, shadows, which are specific to the region and time of a particular scenario. Regular augmentation effects like blurring, brightening, darkening of scenes have also been kept. As a result, our training data has expanded to *1734* examples.


# RUNNING THE CODE

The entire code is in the form of a jupyter notebook (.ipynb) file. To run the file, download the notebook and data from this repository to your local system and change the directory names in the notebook accordingly. 

# SOME RESULTS ON UNSEEN TEST IMAGES (ALSO AVAILABLE IN THE JUPYTER NOTEBOOK)

![image](https://user-images.githubusercontent.com/59358774/168701647-de5e06d6-58cf-4a75-8f94-1417dcb62b08.png)
![image](https://user-images.githubusercontent.com/59358774/168701687-2bf6215c-371e-41bd-8b24-e677324ee0ba.png)
![image](https://user-images.githubusercontent.com/59358774/168701712-37bc1a9f-7760-4a72-8edb-83d64f6ef587.png)

# Conclusion and Future works

We have successfully implemented our own framework based on a structure guided lane detection framework SG-Net. Although our framework is a bit different in that ours is more of an attention guided framework as compared to the structure guided framework proposed in the paper. It should be noted that the feature extractor used by us is similar to the one used in the paper and hence it can be concluded that the backbone of our framework is based on the SG-Net framework although the lane representations and the procedure to learn them are a bit different.

Keeping an eye on the future prospects of this project, we can look to implement a solution to further dissect multiple lanes (as was done in the original SG-Net paper). This is currently a limitation of our project; it fails to distinguish multiple lines. This is something that we would like to work on in the future.
