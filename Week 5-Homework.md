## Week 5

### First modification

The original result

<img width="336" alt="截屏2023-06-05 15 55 27" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/22923a2f-d1f9-403c-b17c-e213814dd00f">

#### Modified the potential vector dimension

Noise_dim= 100
Modified to Noise_dim=200

<img width="1280" alt="image" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/25f3c7b9-14e6-4dfb-93ef-81482b263c1c">

### The results

#### Results after the first modification

<img width="341" alt="截屏2023-06-13 17 18 31" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/68985d9d-82f2-4448-9238-52d1d4f3e920">
It has an inverse effect on the results. The image is more blurred.

### Second modification

#### Modify the number of cores and layers

The number of modified kernels and the number of layers are modified on the basis of modifying the dimensionality of the potential vector.

<img width="681" alt="截屏2023-06-13 17 26 52" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/cab31b64-d6c8-4776-aefb-8ac59527fad8">
<img width="676" alt="截屏2023-06-13 17 27 14" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/cd5c171a-5428-4467-a285-a9f89c69a484">

#### Results after the second modification

<img width="379" alt="截屏2023-06-07 09 21 05" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/5584e7ca-d63d-4d2b-b8ba-1dbabdb43393">

There was a significant effect on the results. The images are clearer and more realistic.

### (More difficult) Training this GAN on a new dataset. 

<img width="634" alt="1" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/5fa0f2ed-6ef2-44b2-ab84-40c5f0e141f0">
<img width="633" alt="2" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/3c55acf0-d62b-4f55-8e18-bb3fd77be30b">
<img width="633" alt="修改了图像预处理函数preprocess_image" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/d133f70c-0903-4349-9013-96c24b33006e">
<img width="1005" alt="修改了生成器模型make_generator_model" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/acbedb47-9b4a-4b8f-9f5d-85753c5f538f">
<img width="1005" alt="修改了判别器模型make_discriminator_model" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/ed7802a2-e419-4912-ba51-8a7eeb8ca9ec">
<img width="1004" alt="修改了损失函数generator_loss" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/61a2fbbb-ed6f-44f8-8b47-9b22579e331e">
<img width="1017" alt="修改了训练步骤train_step中的输入参数" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/126d4234-c864-4dd8-b737-65ca38cc7270">
<img width="1007" alt="修改了生成和保存图像的函数generate_and_save_images" src="https://github.com/yanzhang22010/Coding-3-homework/assets/119860662/bffcf558-cc89-4fb6-8862-28e4772e909e">

1. Dataset Loading and Preprocessing:
Replaced the MNIST dataset loading code with TensorFlow Datasets (TFDS) code to load the CIFAR-100 dataset (tfds.load('cifar100')).
Modified the preprocess_image function to resize the images to 32x32 and normalize them to the range of [-1, 1].
Created a train_df dataframe using tfds.as_dataframe to extract the images from the loaded dataset.

2. Generator Model:
Adjusted the input shape of the first dense layer to (100,) to match the input noise size.
Updated the output shape assertion to (None, 8, 8, 256) to match the reshaped tensor dimensions.
Modified the last convolutional transpose layer to have an output shape of (None, 32, 32, 3) to generate color images.

3.Discriminator Model:
Modified the input shape of the first convolutional layer to [32, 32, 3] to match the input image size.

4.Loss Functions:
Updated the generator loss function to use tf.keras.losses.BinaryCrossentropy directly instead of the generator_loss function used in Code 1.

5.Dataset Batching:
Modified the batch size to 256 to match the batch size used in Code 2.

6.Image Generation and Saving:
Adjusted the image plotting and saving code to handle color images correctly.

7.Training Loop:
Modified the train_step function to extract the images from the tuple, as the CIFAR-100 dataset returns a tuple containing images and labels.
Updated the training step to use only the images for both the real and generated images.
