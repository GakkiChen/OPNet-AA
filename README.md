# OPNet-AA

## Abstract
An action-aware object tracking model with pre-trained Faster-RCNN for object detection, and a series of LSTMs for 
occlusion and containment relationships reasoning. Added action through weight matrix multiplication to boost performance.

Collaboration with Ying Siu Liang, Dongkyu Choi, and Kenneth Kwok from ASTAR IHPC. 
Paper accepted at IROS2021, available at: [Improving Object Permanence using Agent Actions and Reasoning](https://github.com/GakkiChen/OPNet-AA/blob/main/IROS2021_Improving_Object_Permanence_using_Action_Annotations_and_Reasoning.pdf)

## Model Architecture
Expansion and pruning at different network level is illustrated here:
![Alt text](./img/model_structure.PNG?raw=true "OPNet_AA_structure")
