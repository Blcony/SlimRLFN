# SlimRLFN

**SlimRLFN: Making RLFN Smaller and Faster Again**

[NTIRE2024 Efficient Super-Resolution](https://codalab.lisn.upsaclay.fr/competitions/17547)

Shenglong Zhou<sup>1</sup>, and Binbin Chen<sup>2</sup>

<sup>1</sup>University of Science and Technology of China (USTC)

<sup>2</sup>Huazhong University Of Science And Technology (HUST)

## Introduction
![SlimRLFN](https://github.com/Blcony/SlimRLFN/assets/26156941/9307555f-a447-4304-b8e3-40115e0f1441)

We propose the SlimRLFN for the efficient super-resolution task. 
The network architecture is inspired by the design of RLFN, while fully exploring the capacity of reparameterizable convolution, light distillation, and iterative model pruning. 
The whole architecture is shown above, which mainly consists of six SRLFB modules and a pixel shuffle module. 
Reparameterizable convolutions are utilized in the SRLFB module, aiming to improve the super-resolution capability without introducing any additional parameter overhead during the inference stage. Meanwhile, the network is optimized by the pixel-wise loss such as charbonnier loss or L2 loss, along with the distillation loss provided by a light but efficient teacher model. Last but not least, we use iterative pruning to shrink the model size while maintaining the promising performance at the last training stage.

## Requirements
For the datasets and environments, please refer to the [Official Repo](https://github.com/Amazingren/NTIRE2024_ESR).

## Usage
To obtain the results of our SlimRLFN, please conduct the following command:
```shell
CUDA_VISIBLE_DEVICES=0 python test_demo.py --data_dir [path to your data dir] --save_dir [path to your save dir] --model_id 21
```

To obtain the results of our SlimRLFN after pruning, please conduct the following command:
```shell
CUDA_VISIBLE_DEVICES=0 python test_demo.py --data_dir [path to your data dir] --save_dir [path to your save dir] --model_id 21 --use_prune
```

## Contact
Please be free to contact us by e-mail (slzhou96@mail.ustc.edu.cn) or WeChat (slzhou96) if you have any questions.


