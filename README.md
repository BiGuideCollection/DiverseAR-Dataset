# VIP Datasets
This repository accompanies the paper "_3D Object Detection with VI-SLAM Point Clouds: The Impact of
Object and Environment Characteristics on Model Performance_", to appear in the Proceedings of IEEE ICRA 2024. It introduces **VIP500**, a dataset of 4772 VI-SLAM point clouds that covers 500 different object and environment configurations. We also provide **VIP500-D**, an accompanying dataset of 20 RGB-D point clouds of the object classes and shapes in VIP500, for comparison purposes.

# Datasets
The full VIP500 and VIP500-D datasets can be downloaded here: [https://github.com/timscargill/VIP-Datasets/tree/main/VIP-Datasets.](https://github.com/timscargill/VIP-Datasets/tree/main/VIP-Datasets) The dataset follows the hierarchical file structure shown below:
```
VIP-Datasets
└───VIP500
│   │
│   └───carpet_chair1_1.txt
│   └───carpet_chair1_2.txt
│   └───carpet_chair1_3.txt
│   ...
│
└───VIP500-D
│   │
│   └───chair1.pcd
│   └───chair2.pcd
│   └───chair3.pcd
|   ...
```

**VIP500**

_Format:_ Each point cloud in the VIP500 dataset is in .txt format, with each line specifying the coordinates of a point and the object class that point is associated with (x y z class). The numerical value in the class column refers to the following object class assignments (derived from the order in the [ModelNet10 dataset](https://modelnet.cs.princeton.edu/)):

0 - No object  
3 - Chair  
4 - Desk  
8 - Sofa  
9 - Table

_Creation:_ To generate this dataset we used [Virtual-Inertial SLAM](https://github.com/timscargill/Virtual-Inertial-SLAM), which facilitates the creation of semi-synthetic visual-inertial SLAM input data. We created virtual environments in Unity 2020.3.14f1, consisting of a single object in a 8m×6m×4m room with blank walls and a textured floor. For each type of object (e.g., a chair) we created different configurations, in which we varied the object shape by
using different 3D models, the object texture, and the floor texture, as illustrated below:

<img width="407" alt="Virtual chair variations" src="https://github.com/timscargill/VIP-Datasets/assets/62528878/2fd88f30-10ec-4ff6-99b5-6faf5b1ec932"><img width="406" alt="Virtual desk, sofa and table variations" src="https://github.com/timscargill/VIP-Datasets/assets/62528878/89b54594-5f40-46ec-9364-3010764a9272">

We used the A4 trajectory in the [SenseTime VI-SLAM dataset](http://www.zjucvg.net/eval-vislam/dataset/) to generate a new sequence for each environment variant, then ran them on a state-of-the-art open-source VI-SLAM algorithm, [ORB-SLAM3](https://github.com/UZ-SLAMLab/ORB_SLAM3). We modified the ORB-SLAM3 software to save the generated point cloud to a text file. A video of two VI-SLAM point clouds being generated with ORB-SLAM3 is shown below:

![VIP-500 point cloud generation](https://github.com/timscargill/VIP-Datasets/assets/62528878/c0754259-fd51-4f5b-bb61-b0cc260e0d38)

Finally, we segmented and labeled these point clouds using the [Open3D](https://www.open3d.org/) Python library. We applied plane detection and outlier removal to identify points not part of the object, and appended a new column to each line in the point cloud file indicating the object class for that point. Examples of the point clouds generated are shown below (object points in blue, environment points in red):

<img width="401" alt="Chair point cloud examples" src="https://github.com/timscargill/VIP-Datasets/assets/62528878/4ca2f0ec-af4a-4b26-9858-f49850b3ee94"><img width="409" alt="Desk, sofa and table point cloud examples" src="https://github.com/timscargill/VIP-Datasets/assets/62528878/9ddd1c67-9267-4095-bd92-496a7d43c145">

_Contents:_ VIP500 consists of 4772 labeled VI-SLAM point clouds generated using the above process. It covers 500 different environment configurations: 4 common indoor object classes from the [ModelNet10 dataset](https://modelnet.cs.princeton.edu/) (chair, desk, sofa, and table) x 5 object shapes x 5 object textures x 5 floor textures. We ran 10 ORB-SLAM3 trials for each configuration; some configurations resulted in the loss of tracking in some trials and invalid point clouds, which were excluded from the dataset.

**VIP500-D**

_Format:_ Each point cloud in the VIP-500D dataset is in .pcd format.

_Creation:_ We also created an RGB-D dataset that accompanies VIP500, to study the differences between the VI-SLAM point clouds and point clouds generated from 3D scanners. We generated the dataset using the same virtual environments with the same object shapes as those used in VIP500. We exported the virtual environments used to generate VIP500 (built in Unity), to FBX files and imported them to Unreal Engine 4.27.2. To generate the VIP500-D point clouds, we leveraged the Unreal plugin [AirSim](https://microsoft.github.io/AirSim/unreal_custenv/), which facilitates the creation of RGB-D point clouds after capturing RGB camera images and depth sensor readings. Examples of the RGB-D point clouds in VIP500-D are shown below:

<img width="528" alt="Chair model variations in VIP500-D" src="https://github.com/timscargill/VIP-Datasets/assets/62528878/1b0fbd32-5172-4ec8-a040-4b7e43a6bd9d">

_Contents:_ VIP500-D contains four object classes (chair, desk, sofa, and table), each with five object shapes. We do not consider different object and floor textures because these characteristics have minimal influence on RGB-D point clouds. 


# Citation

If you use Virtual-Inertial SLAM in an academic work, please cite: 

```
@inproceedings{VIP-500,
  title={3D Object Detection with VI-SLAM Point Clouds: The Impact of Object and Environment Characteristics on Model Performance},
  author={Duan, Lin, and Scargill, Tim and Chen, Ying and Gorlatova, Maria},
  booktitle={Proceedings of IEEE ICRA 2024},
  year={2024}
 }
 ```

# Acknowledgements 

The authors of this repository are Tim Scargill, Ying Chen and Maria Gorlatova. Contact information of the authors:

* Tim Scargill (timothyjames.scargill AT duke.edu)
* Ying Chen (ying.chen151 AT duke.edu)
* Maria Gorlatova (maria.gorlatova AT duke.edu)

This work was supported in part by NSF grants CSR-1903136, CNS-1908051, CNS-2312760, and CNS-2112562, NSF CAREER Award IIS-2046072, a CISCO Research Award, and a Meta Research Award.
 


