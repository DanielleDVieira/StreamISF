# StreamISF
This repository contains a tool for segmenting streaming video.

## Streaming Graph-based Supervoxel Computation Based on Dynamic Iterative Spanning Forest

Streaming video segmentation decreases processing time by creating supervoxels taking into account small parts of the video instead of using all video content. Thanks to the good performance of the Iterative Spanning Forest to compute Supervoxels (ISF2SVX) based on Dynamic Iterative Spanning Forest (DISF) for video segmentation framework we propose a new graph-based streaming video segmentation method for supervoxel generation by using dynamic iterative spanning forest framework, so-called StreamISF, based on a pipeline composed of six stages: 

<img src="https://github.com/DanielleDVieira/StreamISF/blob/main/imagesReadme/stream-methodology.jpeg" width=800>

- (1) formation of the graph for each block of the video;
- (2) seed oversampling;
- (3) IFT-based supervoxel design;
- (4) reduction in the number of supervoxels;
- (5) spread of trees;
- (6) creation of the segmented video.

The difference in our proposed method is that it is unnecessary to have all the video in memory and the only previous information necessary to segment a block is the intersection frame between the blocks.


<img src="https://github.com/DanielleDVieira/StreamISF/blob/main/imagesReadme/exampleVideoSegmentations.png" width=800>

Example of video segmentations for a video extracted of the GATech. The original frames are illustrated in the first row. We illustrate examples of the proposed method changing the seed sampling. We illustrate results for (a) 10 and (b) 500 supervoxels, considering ISF2SVX-GRID-DYN and StreamISF with k = 30% and allowing tree merges (second and third rows). Each resulting region is colored by its mean color.
It is possible to observe in the figure above that in the first segmented blocks, the skater’s dress is a region that is not in the ISF2SVX result, and even after the dress does not appear in the last blocks due to tree mergers during the propagation of the labels of the intersection trees, the sign on the wall is more detailed in our proposed method in all the images, both for 10 supervoxels and for 500 supervoxels.

### Languages supported

C/C++ (Implementation)

## Requirements

The following tools are required in order to start the installation.
- OpenMP
        
## Compiling 

- To compile GFT:

  1. Copy the "gft" files to a folder on your computer.
  2. Create an environment variable GFT_DIR and place it in .bashrc:
   
      `export export GFT_DIR=/home/user/gft`
  3. Go to the "gft" folder and do:
   
      `make clean`
     
      `make`
  5. If the error "fatal error: zlib.h: No such file or directory" occurs, then you have to install the zlib package: zlib1g-dev. Repeat step 3 again.
   

- To compile DISF programs and the main program streamISF.cpp:

  1. Go to the folder where the streamISF.cpp program is and do:
   
      `make`
   

- To compile just the DISF programs, go to the streamISF.cpp program folder and do:
  
  `make -f MakefileDisf.make clean`
  
  `make -f MakefileDisf.make`
  
## Running

In the make file itself there is an example of how to run the main program streamISF.cpp. Below is this same example and an explanation of the parameters with their respective order.

`./streamISF ./datasets/soccer output/soccer 5000 300 30 1 0 1 50`
1. `./streamISF` is the executable program generated when compiling the streamISF.cpp program.
2. `./datasets/soccer` is the path where the .ppm images that you want to segment are located. The name of these images must be 00001, 00002, 00003 and so on (if you want to test with another video that is not in the datasets folder).
3. `output/soccer` it is the path where you want to save the images segmented by the streamISF algorithm.
4. `5000` number of initial seeds in oversampling.
5. `300` final number of supervoxels in the entire video. The streamISF algorithm will make sure you have a number close to this.
6. `30` number of frames per block is a percentage of the total number of frames.
7. `1` images by intersection. For now, our code only supports one image at the intersection, as it contains the best performance result.
8. `0` coloring type when saving segmented image. 0: Medium color - 1: Random color.
9. `1` do tree merges, 1 if yes, 0 if no.
10. `50` rate to stop supervoxel decrement. Ex.: 10, will be 0.10 of the number of supervoxels.

## Cite
If this work was useful for your research, please cite our paper:

```
@InProceedings{vieira2023streamISF,
  title={Streaming Graph-based Supervoxel Computation Based on Dynamic Iterative Spanning Forest},
  author={Danielle Vieira and Isabela Borlido Barcelos, Bel{\'e}m, Felipe and Falc{\~a}o, Alexandre Xavier and do Patroc{\'\i}nio, Zenilton KG and Guimar{\~a}es, Silvio Jamil F},
  booktitle={},
  publisher={},
  pages={},
  year={2023},
  organization={}
}
```
