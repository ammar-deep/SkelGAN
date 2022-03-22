# SkelGAN
SkelGAN: A Font Image Skeletonization Method

## Introduction

This is the Tensorflow implementation of **SkelGAN: A Font Image Skeletonization Method**.

[paper](https://www.koreascience.or.kr/article/JAKO202109651163015.pdf)

## Abstract
In this research, we study the problem of font image skeletonization using an end-to-end deep adversarial network, in contrast with the state-of-the-art methods that use mathematical algorithms. Several studies have been concerned with skeletonization, but a few have utilized deep learning. Further, no study has considered generative models based on deep neural networks for font character skeletonization, which are more delicate than natural objects. In this work, we take a step closer to producing realistic synthesized skeletons of font characters. We consider using an end-to-end deep adversarial network, SkelGAN, for font-image skeletonization, in contrast with the state-of-the-art methods that use mathematical algorithms. The proposed skeleton generator is proved superior to all well-known mathematical skeletonization methods in terms of character structure, including delicate strokes, serifs, and even special styles. Experimental results also demonstrate the dominance of our method against the state-of-the-art supervised image-to-image translation method in font character skeletonization task.

## Prerequisites

- Windows
- CPU or NVIDIA GPU + CUDA cuDNN
- python 3.6.8
- tensorflow-gpu 1.13.1
- pillow 6.1.0 

## Get Started

### Installation

#### Setting up the environment
1. ```
   conda create --name skelgan python=3.6.8
   ```
2. ```
   conda activate skelgan or activate skelgan
   ```
3. ```
   conda install -c anaconda tensorflow-gpu=1.13.1
   ```
4. ```
   conda env update --file tools.yml
   ```
### Datasets
Our model consists of a conditional GAN in paired setting (pix2pix). We need to prepare a paired dataset. i.e. a font to corresponding skeleton dataset. 
To do this, place N number of Korean fonts in the fonts directory. Then run the below commands for data preprocessing.

#### Generate Font images
``` python ./tools/trg-font-image-generator.py ```

#### Generate Font skeleton images
```python ./tools/trg-skeleton-image-generator.py```

#### Combine font and corresponding skeleton images
```python ./tools/combine_images.py --input_dir font-image-data/images --b_dir skel-image-data/images --operation combine```

#### Convert images to TFRecords
```python ./tools/images-to-tfrecords.py```

### Training the model
```
python main.py --mode train --output_dir trained_model --max_epochs 15 
```
### Testing the model
Generate images just like before (follow the previous data generation steps) but this time use a different module for creating testing TFRecords with the below mentioned command.
#### Convert images to TFRecords
  ```
  python ./tools/test-images-to-tfrecords.py
  ```
#### Generate test results
 ```
python main.py --mode test --output_dir testing_results --checkpoint trained_model
 ```
## Acknowledgements

This code is inspired by the [pix2pix tensorflow](https://github.com/affinelayer/pix2pix-tensorflow) project.

Special thanks to the following works for sharing their code and dataset.

- [tensorflow-hangul-recognition](https://github.com/IBM/tensorflow-hangul-recognition)
- [pix2pix](https://github.com/affinelayer/pix2pix-tensorflow)

## Citation

Please cite our work if you like it.

Debbie Honghee Ko, Ammar Ul Hassan, Saima Majeed, and Jaeyoung Choi. Skelgan: A font image skeletonization method. Journal of Information Processing Systems,
17(1):1–13, 2021.

## Copyright

The code and other helping modules are only allowed for PERSONAL and ACADEMIC usage.
