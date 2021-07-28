# OPNet-AA

## Abstract
An action-aware object tracking model with pre-trained Faster-RCNN for object detection, and a series of LSTMs for 
occlusion and containment relationships reasoning. Added action through weight matrix multiplication to boost performance.

Collaboration with Ying Siu Liang, Dongkyu Choi, and Kenneth Kwok from ASTAR IHPC. 
Paper accepted at IROS2021, available at: [Improving Object Permanence using Agent Actions and Reasoning](https://github.com/GakkiChen/OPNet-AA/blob/main/IROS2021_Improving_Object_Permanence_using_Action_Annotations_and_Reasoning.pdf)

## Model Architecture
We augmented OPNet with action annotations (AA) generated from the ground-truth scene annotations and object detection results provided in the CATER dataset.  
The action annotation is a vector of length 300, same as the total number of frames. Each element in the vector will be the target object id, if the target is visible at that frame, or id of the object blocking it if it’s occluded or contained.
We can generate a weight matrix A∈R^(N×K) from the action annotations by 
1) initialize a matrix with elements all equals to 1; 
2) at each frame, set the element corresponds to the object id in action annotation to a multiple of 1;
3) softmax the matrix to obtain a normalized weight.
here N is the total frame count and K is the maximal object count. 
In the original OPNet paper, there is a “who to track” module responsible for understanding which object is currently covering the target. It consists of a single LSTM layer with a hidden dimension of 256 neurons and a linear projection matrix. It projects the LSTM output to K neurons then apply a SoftMax layer to compute the attention mask.
We then augment this attention mask by multiplying it with our weight matrix A. Theoretically, this augmented attention incorporates explicit guidance on which object to track, and we can vary the strength of the guidance by changing the weight parameter. 
![Alt text](./img/model_structure.PNG?raw=true "OPNet_AA_structure")
