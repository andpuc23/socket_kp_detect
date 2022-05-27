# socket_kp_detect
Repository for DL final project @Skoltech, '22


## How to use
1. ResNetExperiment contains code to train KeypointRCNN, data to train can be acqured by script in `scripts_utils` folder
2. SuperPoint module:
- Original repo: https://github.com/eric-yyjau/pytorch-superpoint
Before start working, please, install all packages from original repo as it instructed in the README file.
The repo is already contains all necessary data in datasets/COCO and datasets/HPatches folders.
- For validate MagicPoint model:
`python export.py export_detector_homoAdapt configs/magicpoint_coco_export.yaml magicpoint_synth_homoAdapt_coco`
- For train Superpoint model on Socket data (where is checkpoint, no necessary)
`python train4.py train_joint configs/superpoint_coco_train_heatmap.yaml superpoint_coco --eval --debug`
- For validation fine-tuned model
Set in config/magicpoint_repeatability_heatmap.yaml pretrained: pretrained: 'logs/superpoint_coco_heat2_0/checkpoints/superPointNet_170000_checkpoint.pth.tar'
`python export.py export_descriptor  configs/magicpoint_repeatability_heatmap.yaml superpoint_socket_sto_train2 --eval`
`python export.py export_descriptor  configs/magicpoint_repeatability_heatmap.yaml superpoint_socket_sto_train2 --eval`
- For validation not fine tuned model
Set in config/magicpoint_repeatability_heatmap.yaml pretrained: pretrained: 'logs/superpoint_coco/checkpoints/superPointNet_50000_checkpoint.pth.tar'
`python export.py export_descriptor  configs/magicpoint_repeatability_heatmap.yaml superpoint_socket_original2 --eval`
`python evaluation.py logs/superpoint_socket_original2/predictions --repeatibility --outputImg --homography --plotMatching`
Results are located in logs/<folder with name of experiment>/predictions/results.txt files

3. GAN part
To run GAN experiment follow instructions, provided in the cyclegan repo. 
To reproduce our results use `--dataroot ./train_data/{chosen_dataset} --name socket_3`
