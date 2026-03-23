# PetroSynthGAN：Semantic Image Synthesis of Rock Slice Based on Conditional Generative Adversarial Networks

Official PyTorch implementation of the paper "Semantic Image Synthesis of Anime Characters Based on Conditional Generative Adversarial Networks".  The code allows the users to reproduce and extend the results reported in the study.  Please cite the paper when reporting, reproducing or extending the results.

# Abstract

This project proposes a Polarization Modality Tensor-Conditioned Generator based on polarization modality identification. Specifically, polarization mode identification tensors are used to control the generator to map the semantic label graph to a specific polarization mode. Furthermore, borrowing from StyleGAN, we introduce conditional noise to enhance the generator's ability to fit color features, resulting in more natural colors in the generated images. Secondly, a semantic texture dual-supervised discriminator is proposed, which uses a dual-branch structure at the end of the network to perform semantic segmentation and texture extraction simultaneously. This discriminator effectively supervises the texture features in the rock slice image, thus encouraging the generator to generate higher quality texture details.

![fig](./figs/fig.png)

# Datasets

The folder structure should be

```
datasets                
└── example
    ├──test_glcm
    ├──test_xpl
    ├──test_ppl
    ├──test_inst
    ├──test_label_xpl
    ├──test_label_ppl
    ├──train_glcm
    ├──train_xpl
    ├──train_ppl
    ├──train_inst
    ├──train_label_xpl
    ├──train_label_ppl
    └── class.txt
```

# GLCM
A Python tool for extracting Gray-Level Co-occurrence Matrix (GLCM) texture features from images. This implementation focuses on computational efficiency and provides multiple GLCM-based texture measures.The folder structure should be

```
datasets                
└── glcm
```

To glcm on the example dataset, for example:

```
cd ./datasets/glcm
python fast_glcm.py -i ./input_images -o ./texture_maps --resize -W 512 -H 512
```

# Pretrained models


You can generate images with a pre-trained checkpoint via `test.py`. 

The example of example :

```
python test.py --class_num 2  --name example --class_dir ./datasets/example/class.txt \
--ckpt_iter best --dataset_mode custom --dataroot ./datasets/example  --batch_size 1 --gpu_ids 0
```

# Train the model

To train on the example dataset, for example:

```
python train.py --name example  --class_dir datasets/example /class.txt --class_num 2 --dataset_mode custom \
--dataroot ./datasets/example  --gpu_ids 0 --num_epochs 1000 --batch_size 1
```

The `--class_dir` is the path for storing the character ID tag txt. The `--class_num`  is the number of anime characters contained in the dataset.

# Test the model

To test on the example dataset, for example:

```
python test.py --class_num 2  --name example --class_dir ./datasets/example/class.txt \
--ckpt_iter best --dataset_mode custom --dataroot ./datasets/example --batch_size 1 --gpu_ids 0
```


# Contact

If you have any questions, please create an issue on this repository or contact us at 

zhengdongyu@cdut.edu.cn

# Acknowledgement

This code is based on [https://github.com/boschresearch/OASIS]()

# License

This project is open-sourced under the AGPL-3.0 license. See the
[LICENSE](LICENSE) file for details.

For a list of other open source components included in this project, see the
file [3rd-party-licenses.txt](3rd-party-licenses.txt).
