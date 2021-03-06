# MMGCN: Multi-modal Graph Convolution Network for Personalized Recommendation of Micro-video
This is our Pytorch implementation for the paper:  
> Yinwei Wei, Xiang Wang, Liqiang Nie, Xiangnan He, Richang Hong, and Tat-Seng Chua(2019). MMGCN: Multi-modal Graph Convolution Network for Personalized Recommendation of Micro-video. In ACM MM`19, NICE, France,Oct. 21-25, 2019  

## Introduction
Multi-modal Graph Convolution Network is a novel multi-modal recommendation framework based on graph convolutional networks, explicitly modeling modal-specific user preferences to enhance micro-video recommendation. 

## Environment Requirement
The code has been tested running under Python 3.5.2. The required packages are as follows:
- Pytorch == 1.1.0
- torch-cluster == 1.4.2
- torch-geometric == 1.2.1
- torch-scatter == 1.2.0
- torch-sparse == 0.4.0
- numpy == 1.16.0

## Example to Run the Codes
The instruction of commands has been clearly stated in the codes.
- Kwai dataset  
```python train.py --model_name='MMGCN' --l_r=0.0005 --weight_decay=0.1 --batch_size=1024 --dim_latent=64 --num_workers=30 --aggr_mode='mean' --num_layer=2 --concat=False```
- Tiktok dataset  
`python train.py --model_name='MMGCN' --l_r=0.0005 --weight_decay=0.1 --batch_size=1024 --dim_latent=64 --num_workers=30 --aggr_mode='mean' --num_layer=2 --concat=False`
- Movielens dataset  
`python train.py --model_name='MMGCN' --l_r=0.0001 --weight_decay=0.0001 --batch_size=1024 --dim_latent=64 --num_workers=30 --aggr_mode='mean' --num_layer=2 --concat=False`  

Some important arguments:  


- `model_name`: 
  It specifies the type of model. Here we provide three options: 
  1. `MMGCN` (by default) proposed in MMGCN: Multi-modal Graph Convolution Network for Personalized Recommendation of Micro-video, ACM MM2019. Usage: `--model_name='MMGCN'`
  2. `VBPR` proposed in [VBPR: Visual Bayesian Personalized Ranking from Implicit Feedback](https://arxiv.org/abs/1510.01784), AAAI2016. Usage: `--model_name 'VBPR'`  
  3. `ACF` proposed in [Attentive Collaborative Filtering: Multimedia Recommendation with Item- and Component-Level Attention
](https://dl.acm.org/citation.cfm?id=3080797), SIGIR2017. Usage: `--model_name 'ACF'`  
  4. `GraphSAGE` proposed in [Inductive Representation Learning on Large Graphs](https://arxiv.org/abs/1706.02216), NIPS2017. Usage: `--model_name 'GraphSAGE'`
  5. `NGCF` proposed in [Neural Graph Collaborative Filtering](https://arxiv.org/abs/1905.08108), SIGIR2019. Usage: `--model_name 'NGCF'`  


- `aggr_mode` 
  It specifics the type of aggregation layer. Here we provide three options:  
  1. `mean` (by default) implements the mean aggregation in aggregation layer. Usage `--aggr_mode 'mean'`
  2. `max` implements the max aggregation in aggregation layer. Usage `--aggr_mode 'max'`
  3. `add` implements the sum aggregation in aggregation layer. Usage `--aggr_mode 'add'`
  
  
- `concat`:
  It indicates the type of combination layer. Here we provide two options:
  1. `concat`(by default) implements the concatenation combination in combination layer. Usage `--concat 'True'`
  2. `ele` implements the element-wise combination in combination layer. Usage `--concat 'False'`
## Dataset
We provide three processed datasets: Kwai, Tiktok, and Movielnes.  
- You can find the full version of recommendation datasets via [Kwai](https://www.kuaishou.com/activity/uimc), [Tiktok](http://ai-lab-challenge.bytedance.com/tce/vc/), and [Movielens](https://grouplens.org/datasets/movielens/).
<!--- We select some users and micro-videos in [Kwai](https://drive.google.com/open?id=1Xk-ofNoDnwcZg_zYE5tak9s1iW195kY2) and [Tiktok](https://drive.google.com/open?id=1mlKTWugOr8TxRb3vq_-03kbr0olSJN_7) datasets accoding to the timestamp. 
- We extract the visual, acoustic, and textual features of all trailers in [Movielens](https://drive.google.com/open?id=1I1cHf9TXY88SbVCDhRiJV1drWX5Tc1-8) dataset.
-->
||#Interactions|#Users|#Items|Visual|Acoustic|Textual|
|:-|:-|:-|:-|:-|:-|:-|
|Kwai|1,664,305|22,611|329,510|2,048|-|100|
|Tiktok|726,065|36,656|76,085|128|128|128|
|Movielens|1,239,508|55,485|5,986|2,048|128|100|

-`train.npy`
   Train file. Each line is a user with her/his positive interactions with items: (userID and micro-video ID)  
-`val.npy`
   Validation file. Each line is a user with her/his 1,000 negative and several positive interactions with items: (userID and micro-video ID)  
-`test.npy`
   Test file. Each line is a user with her/his 1,000 negative and several positive interactions with items: (userID and micro-video ID)  
