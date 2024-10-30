# Waterloo-Point-Cloud-Database-5.0

This database was created by Honglei Su ([suhonglei@qdu.edu.cn](mailto:suhonglei@qdu.edu.cn)) and Dongshuai Duan(dsduan00@gmail.com) from Qingdao University in 2024. We welcome everyone to carry on the test and propose the modification opinion. If you use our database [WPC5.0]( https://drive.google.com/drive/folders/1WF5MHuixfaWm_TsSsv9ClIh0N7z2pXou?usp=sharing) (a Google account required) in your paper, please cite our paper:

@article{duan2024perceptual,  
title={Perceptual Quality Assessment of Octree-RAHT Encoded 3D Point Clouds},  
author={Duan, Dongshuai and Su, Honglei and Liu, Qi and Yuan, Hui and Gao, Wei and Song, Jiarun and Wang, Zhou},  
journal={arXiv preprint arXiv:2410.06729},  
year={2024}  
}

The WPC5.0 database is composed of 400 Octree-RAHT encoded point clouds and corresponding bitstreams whose 20 original point clouds (Bag, Banana, Biscuits, Cake, Cauliflower, Flowerpot, Glasses_case, Honeydew_melon, House, Litchi, Mushroom, Pen_container, Pineapple, Ping-pong_bat, Puer_tea, Pumpkin, Ship, Statue, Stone, Tool_box) are from the [WPC database](https://github.com/qdushl/Waterloo-Point-Cloud-Database). Each original point cloud is encoded by 4 geometry parameters PQS{1, 0.5, 0.25, 0.125} and 5 texture parameters QP{22, 28, 34, 40, 46} to produce 20 distortion levels. The rest of the encoding parameters are set with default values. The subjective test settings and raw data processing are the same as those in the WPC database.<br/><br/>

# streamPCQ-OR model

In order to extract parameters of streamPCQ-OR model from bitstream of distorted point cloud, we have reformed the source code files from [mpeg-pcc-tmc13-release-v20.0](https://github.com/MPEGGroup/mpeg-pcc-tmc13/releases/tag/release-v20.0). We use the reformed version to realize predicting perceptual quality of distorted point cloud without the need for fully decoding. And the modifications are applied to PCCTMC3Decoder.h, decoder.cpp and TMC3.cpp in tmc3 project. Moreover, we introduce two new files, streamPCQ_OR.h and streamPCQ_OR.cpp, to construct the streamPCQ-OR model and modify CMakeLists.txt to compile the two files into tmc3 project. It should be noted that the refactor version soley adds streamPCQ-OR model into tmc3 project and other code remain the same as in tmc3 project. And the method to used it is completely identical to method of application of mpeg-pcc-tmc13-release-v20.0 (cmake, generate solutions, use generated tmc3.exe to encode or decode point cloud). The difference is that the reformed version will output perceptual quality of point cloud encoded by Octree-RAHT in terminal window at work mode of decoding.

If you have any specific questions about the reformed version, feel free to ask.

In addition, we also provide the scores predicted by the comparison algorithms mentioned in the paper on multiple databases in predscore_models.xlsx for subsequent research.

## Running

We provide streamPCQ_OR.exe generated according to the above settings. There are different usage methods for perceptual quality assessment of a single point cloud or multiple point clouds.

### Single assessment

For perceptual quality assessment of a single point cloud stream, open a terminal window in the working directory and execute the following script:

```console
streamPCQ_OR.exe -c decoder.cfg --compressedStreamPath="your_file_name.bin" --reconstructedDataPath=" your_file_name.ply"
```

Note that the file name in the script should be set to the corresponding file name.

### Batch assessment

For perceptual quality assessment of batch point cloud streams, we have generated the corresponding batch file streamPCQ-OR.bat. Simply put streamPCQ-OR.bat, decoder.cfg, streamPCQ_OR.exe and the point cloud stream files that need quality assessment in the same folder, and double-click streamPCQ-OR.bat to perform perceptual quality assessment of all point cloud stream files in the current folder. The assessment results are saved in streamPCQ-OR_predMOS.xlsx.

### Demo

We provide the corresponding demo file. Double-click the streamPCQ-OR.bat file in the demo folder to predict the perceptual quality of all point cloud stream files in the current folder. The prediction results will be saved in the streamPCQ-OR_predMOS.xlsx file in the current folder.

***-----------COPYRIGHT NOTICE STARTS WITH THIS LINE------------***
***Copyright (c) 2024 The Qingdao University All rights reserved.***

Permission is hereby granted, without written agreement and without license or royalty fees, to use, copy, modify, and distribute this database (the point clouds, the results and the source files) and its documentation for any purpose, provided that the copyright notice in its entirety appear in all copies of this database, and the original source of this database, Intelligent Multimedia Signal Processing (IMSP) Laboratory at Qingdao University, is acknowledged in any publication that reports research using this database.

***Additional Restrictions for streamPCQ-OR Model:***

The streamPCQ-OR model is intended for non-commercial academic research use only. Any use of the streamPCQ-OR model for commercial purposes is strictly prohibited without the prior written consent of The Qingdao University. Redistribution or modification of the streamPCQ-OR model for commercial gain is not allowed.

***-----------COPYRIGHT NOTICE ENDS WITH THIS LINE------------***

# Acknowledgment

This project is based on [G-PCC](https://www.mpeg.org/standards/MPEG-I/9/) of [MPEG](https://www.mpeg.org), thanks for their excellent works.
