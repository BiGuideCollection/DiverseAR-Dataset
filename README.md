# DiverseAR Datasets
This repository accompanies the workshop paper "_Advancing the Understanding and Evaluation of AR-Generated Scenes: When Vision-Language Models Shine and Stumble_", submitted to GenAI-XR 2025. It introduces **DiverseAR**, a dataset of 318 images collected from two commercial AR platforms (Amazon and Scaniverse), three AR applications (HoloLens) previously developed by our lab \cite{qu2024looking, xiu2024lobstar, eom2022neurolens}, and two AR applications (Apple Vision Pro and Android) specifically created for this project. 

# Datasets
The full DiverseAR dataset can be downloaded here: [[https://github.com/timscargill/VIP-Datasets/tree/main/VIP-Datasets.]([https://github.com/timscargill/VIP-Datasets/tree/main/VIP-Datasets](https://duke.box.com/s/0lbyth1aq575a1sbve5awa3og2h0pq1b)](https://duke.box.com/s/0lbyth1aq575a1sbve5awa3og2h0pq1b)) The dataset follows the hierarchical file structure shown below:
```
VIP-Datasets
└───VIP500
│   │
│   └───carpet_chair1_1.txt
│   └───carpet_chair1_2.txt
│   └───carpet_chair1_3.txt
│   ...
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

# Acknowledgements 

The authors of this repository are Lin Duan, Yanming Xiu and Maria Gorlatova. Contact information of the authors:

* Lin Duan (lin.duan AT duke.edu)
* Yanming Xiu (yanming.xiu AT duke.edu)
* Maria Gorlatova (maria.gorlatova AT duke.edu)

This work was supported in part by NSF grants CSR-2312760, CNS-2112562 and IIS-2231975, NSF CAREER Award IIS-2046072, NSF NAIAD Award 2332744, a CISCO Research Award, a Meta Research Award, and Defense Advanced Research Projects Agency Young Faculty Award HR0011-24-1-0001. This paper has been approved for public release; distribution is unlimited. The contents of the paper do not necessarily reflect the position or the policy of the Defense Advanced Research Projects Agency. No official endorsement should be inferred.
 


