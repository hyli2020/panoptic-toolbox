PanopticStudio Toolbox
======================

This repository shows how to work with the [Panoptic Studio](http://domedb.perception.cs.cmu.edu) (Panoptic) data.

## Quick start guide
Follow these steps to set up a simple example:

### 1. Check out the codebase
```
git clone https://github.com/CMU-Perceptual-Computing-Lab/panoptic-toolbox
cd panoptic-toolbox
```

### 2. Download the sample data
This bash script requires curl or wget.
```
./scripts/getData.sh sampleData
```

You can also download other seqeunce using the same script by using the name of the target sequence. 
```
./scripts/getData.sh 160422_ultimatum
```

You can also specify the number of videos you want to donwload. 
```
./scripts/getData.sh sampleData (VGA_Video_Number) (HD_Video_Number)
```

For example, the following command will download 240 vga videos and 10 videos.  
```
./scripts/getData.sh sampleData 240 10
```

Note that we have sorted the VGA camera order so that you download uniformly distributed view. 


### 3. Extract the images & skeleton data
This step requires [ffmpeg](https://ffmpeg.org/).
```
./scripts/extractAll.sh sampleData
```
This will extract images, for example `sampleData/vgaImgs/01_01/01_01_00000000.png`, and the corresponding 3D skeleton data, for example `sampleData/vgaPose3d_stage1/body3DScene_00000000.json`.

`extractAll.sh` is a simple script that combines the following set of commands (you shouldn't need to run these again):
```bash
cd sampleData
../scripts/vgaImgsExtractor.sh # PNG files from VGA video (25 fps)
../scripts/hdImgsExtractor.sh # PNG files from HD video (29.97 fps)
tar -xf vgaPose3d_stage1.tar # Extract skeletons at VGA framerate
tar -xf hdPose3d_stage1.tar # Extract skeletons for HD
cd ..
```

### 4. Run the examples
Python examples (require numpy, matplotlib):
```
cd python
jupyter notebook example.ipynb
```
The result should look like [this](https://github.com/CMU-Perceptual-Computing-Lab/panopticapi_d/blob/master/python/example.ipynb).

Matlab example:
```matlab
>>> cd matlab
>>> demo
```
