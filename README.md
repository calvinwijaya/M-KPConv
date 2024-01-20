# M-KPConv
This repository contain personal modification of Kernel Point Convolution (KPConv) implemented in Pytorch created by Hugues THOMAS. Please check the [original repository](https://github.com/HuguesTHOMAS/KPConv-PyTorch) for complete and details explanation of KPConv. KPConv is a point convolution operator presented in [ICCV2019 paper (arXiv)](https://arxiv.org/abs/1904.08889). This modification of KPConv used to learn how the code structured and works, by changing it into binary problem to segment ground and off-ground point cloud. The modification that has been made into the script in this repository:
1. Change class into off-ground (0) and ground (1)
2. Change data input and output into LAS file with UTM compatibility
3. Change how data input prepared (changing folder order)
4. Add several parser argument for user as input

## Prerequisites & Instalations
This implementation has been tested on Ubuntu 22.04.3. The original repo implemented with Ubuntu 18.04 and Windows 10. Check the [Installation guide](https://github.com/HuguesTHOMAS/KPConv-PyTorch/blob/master/INSTALL.md) in original repository for details.
1. Make sure CUDA and cuDNN are installed. Configuration has been tested:
```
PyTorch 1.4.0, CUDA 10.1 and cuDNN 7.6 (Original repo)
PyTorch 2.1.2+cu118, CUDA 12.2 and cuDNN 8.9 (This repo)
```
2. Ensure all python packages are installed :
```
sudo apt update
sudo apt install python3-dev python3-pip python3-tk
```
3. Follow [PyTorch installation procedure](https://pytorch.org/get-started/locally/).
4. Install the other dependencies with pip:
```
numpy
scikit-learn
PyYAML
matplotlib (for visualization)
mayavi (for visualization)
PyQt5 (for visualization)
```
5. Compile the C++ extension modules for python located in cpp_wrappers. Open a terminal in this folder, and run:
```
sh compile_wrappers.sh
```
You should now be able to train Kernel-Point Convolution models

## How to use
This repository only try Scene Segmentation to train KP-FCNN on scene segmentation task. For other use such as object classification and SLAM segmentation please check the [original documentation](https://github.com/HuguesTHOMAS/KPConv-PyTorch/tree/master/doc).

### Data
Place LAS point cloud data into `./data` folder. Now, you can use LAS point cloud with UTM compatibility. Besides LAS file, create a textfile containing name of the LAS file such as:
```
Area_1
Area_2
```
And save it with name `list` and TXT format. Look example at `./data` folder in this repository.
![Example inside data folder](https://github.com/calvinwijaya/M-KPConv/assets/88726143/9a216010-6558-44eb-b654-1d769e1899ca)

### Training
Simply run the following script to start the training:
```
python3 train.py
```
Several parser arguments that user can define:
- log_dir, Log directory for load pre-trained models
- test_area, Area for testing
- expected_N, Expected batch size order of magnitude
After training, a folder name `./results` is created automatically, containing: model checkpoint (in TAR format), potentials folder, and prediction folders. There are also several logs for parameters, training, and val_IoUs.

### Test
Simply run the following script to start the test:
```
python3 test.py
```
Several parser arguments that user can define:
- validation_size, Validation size for testing
- validation, Set data to use: validation or test
- test_area, Area for testing
- expected_N, Expected batch size order of magnitude
After test, a folder name `./test` is created automatically, containing: potentials, predictions, and probs folder. The prediction result is also in LAS format now, besides PLY format.

# Citation
```
@article{thomas2019KPConv,
    Author = {Thomas, Hugues and Qi, Charles R. and Deschaud, Jean-Emmanuel and Marcotegui, Beatriz and Goulette, Fran{\c{c}}ois and Guibas, Leonidas J.},
    Title = {KPConv: Flexible and Deformable Convolution for Point Clouds},
    Journal = {Proceedings of the IEEE International Conference on Computer Vision},
    Year = {2019}
}
```
