<div align="center">   
  
# RadarDistill: Boosting Radar-based Object Detection Performance via Knowledge Distillation from LiDAR Features
</div>

> - [Paper in arXiv]([https://arxiv.org/abs/2403.05061)
> Geonho Bang*, Kwangjin Choi*, Jisong Kim, Dongsuk Kum, Jun Won Choi**


# Abstract
The inherent noisy and sparse characteristics of radar data pose challenges in finding effective representations for 3D object detection. In this paper, we propose RadarDistill, a novel knowledge distillation (KD) method, which can improve the representation of radar data by leveraging LiDAR data. RadarDistill successfully transfers desirable characteristics of LiDAR features into radar features using three key components: Cross-Modality Alignment (CMA), Activation-based Feature Distillation (AFD), and Proposal-based Feature Distillation (PFD). CMA enhances the density of radar features by employing multiple layers of dilation operations, effectively addressing the challenge of inefficient knowledge transfer from LiDAR to radar. AFD selectively transfers knowledge based on regions of the LiDAR features, with a specific focus on areas where activation intensity exceeds a predefined threshold. PFD similarly guides the radar network to selectively mimic features from the LiDAR network within the object proposals. Our comparative analyses conducted on the nuScenes datasets demonstrate that RadarDistill achieves state-of-the-art (SOTA) performance for radar-only object detection task, recording 20.5% in mAP and 43.7% in NDS. Also, RadarDistill significantly improves the performance of the camera-radar fusion model. 


<h1>Methods</h1>

![method](./figs/CRT-Fusion_overall.png "model arch")
**Overall architecture of RadarDistill**:The input point clouds from each modality are independently processed through Pillar Encoding followed by SparseEnc to extract low-level BEV features. CMA is then employed to densify the low-level BEV features in the radar branch. AFD then identifies active and inactive regions based on both radar and LiDAR features and minimizes their associated distillation losses. Subsequently, PFD conducts knowledge distillation based on proposal-level features obtained from DenseEnc. Note that the LiDAR branch is solely utilized during the training phase to enhance the radar pipeline and is not required during inference.


# Getting Started
Please see [getting_started.md](docs/getting_started.md)

<!--
## Training (R50 CRT-Fusion)
**Phase 1:**
```shell
./tools/dist_train.sh configs/crt-fusion/crtfusion-r50-fp16_phase1.py 4 --gpus 4 --work-dir {phase1_work_dirs} --no-validate
python tools/swap_ema_and_non_ema.py {phase1_work_dirs}/iter_10548.pth
```
**Phase 2:**
```shell
./tools/dist_train.sh configs/crt-fusion/crtfusion-r50-fp16_phase2.py 4 --gpus 4 --work-dir {phase2_work_dirs} --resume-from {phase1_work_dirs}/iter_10548_ema.pth
python tools/swap_ema_and_non_ema.py {phase2_work_dirs}/iter_42192.pth
```

## Inference (R50 CRT-Fusion)
**Run the following commands:**
```shell
./tools/dist_test.sh configs/crt-fusion/crtfusion-r50-fp16_phase2.py {phase2_work_dirs}/iter_42192_ema.pth 1 --eval bbox
```

## Model Zoo
We further optimized our models, which resulted in a slight difference compared to the performance reported in the paper.

|Method|mAP|NDS|Model
|-|-|-|-|
|[**R50 CRT-Fusion**](configs/crt-fusion/crtfusion-r50-fp16_phase2.py)|49.3|57.9|[Link](https://github.com/mjseong0414/CRT-Fusion/releases/download/v0.0.0/crt-fusion-r50-42192_ema.pth)
|[**R50 CRT-Fusion-light-cbgs**](configs/crt-fusion/crtfusion-r50-fp16_phase2_light_cbgs.py)|48.9|58.7|[Link](https://github.com/mjseong0414/CRT-Fusion/releases/download/v0.0.0/crt-fusion-r50-light-cbgs-160100_ema.pth)
-->

## Acknowledgements
We thank numerous excellent works and open-source codebases:
- [OpenPCDet](https://github.com/open-mmlab/OpenPCDet)

# Bibtex
If this work is helpful for your research, please consider citing the following BibTeX entry.

```
@article{bang2024radardistill,
  title={RadarDistill: Boosting Radar-based Object Detection Performance via Knowledge Distillation from LiDAR Features},
  author={Bang, Geonho and Choi, Kwangjin and Kim, Jisong and Kum, Dongsuk and Choi, Jun Won},
  journal={arXiv preprint arXiv:2403.05061},
  year={2024}
}
```
