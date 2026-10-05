# Pix2Pix Sketch-to-Image Translation

A deep learning image-to-image translation project that generates realistic RGB flower images from grayscale sketches using Pix2Pix.

The project compares a reconstruction-based encoder-decoder baseline with conditional GAN architectures using a U-Net generator and PatchGAN discriminators.

> Developed as an academic final project focused on generative deep learning and image-to-image translation.

## Project Overview

The goal is to transform a **128×128 sketch image** into a **128×128 RGB flower image**.

The project uses the **Oxford Flowers 102** dataset and automatically converts flower images into sketch-image pairs for supervised training.

Two main approaches are explored:

- **Naive Encoder-Decoder** trained using reconstruction loss
- **Pix2Pix Conditional GAN** using a U-Net generator and PatchGAN discriminator

## Model Architecture

### Naive Baseline

An encoder-decoder model is used as a baseline to evaluate image reconstruction without adversarial training.

Different reconstruction losses are explored, including:

- Mean Squared Error (MSE)
- Mean Absolute Error (MAE)
- Combined MAE + MSE

### Pix2Pix

The Pix2Pix architecture combines:

- **U-Net Generator** for sketch-to-image generation
- **PatchGAN Discriminator** for adversarial training
- **L1 Reconstruction Loss** for structural preservation
- **Adversarial Loss** for improved realism and texture

Different PatchGAN receptive fields and loss weights are evaluated.

## Experiments

The project compares multiple configurations, including:

- Naive Encoder-Decoder
- Pix2Pix with PatchGAN `n_layers = 3`
- Pix2Pix with PatchGAN `n_layers = 4`
- Different reconstruction losses
- Different Pix2Pix λ values

Models are evaluated using:

- L1 / MAE
- MSE
- PSNR
- SSIM
- Visual output quality

## Final Model

The selected model is:

**Pix2Pix with PatchGAN (`n_layers = 3`) and λ = 100**

Although some configurations achieved slightly better individual numerical metrics, the selected model provided the strongest overall balance between:

- Sharpness
- Color realism
- Structural consistency
- Visual quality

## Test Environment

The test notebook provides a simple inference workflow:

1. Load the trained generator.
2. Upload a sketch image.
3. Resize and normalize the input.
4. Generate an RGB flower image.
5. Display the sketch and generated result.

## Project Structure

```text
Pix2Pix-Sketch-to-Image/
├── notebooks/
│   ├── Train_Notebook.ipynb
│   ├── Experiments_Notebook.ipynb
│   └── Test_Notebook.ipynb
│
├── README.md
├── requirements.txt
└── .gitignore
```

## Technologies

- Python
- TensorFlow
- Keras
- OpenCV
- NumPy
- Pandas
- Matplotlib
- TensorFlow Datasets
- Google Colab
- gdown

## Dataset

The project uses the **Oxford Flowers 102** dataset.

Images are resized to `128×128` and converted into sketch-target pairs. The sketch is used as the model input, while the original RGB flower image is used as the target.

The dataset is loaded programmatically using TensorFlow Datasets and is not included directly in this repository.

## Notebooks

### Training Notebook

Contains the main training pipeline, including:

- Dataset loading and preprocessing
- Sketch generation
- Naive baseline training
- Pix2Pix training
- U-Net generator
- PatchGAN discriminators
- Training visualization
- Model saving

### Experiments Notebook

Contains additional experimentation and model comparison, including:

- Quantitative evaluation
- Visual comparisons
- Reconstruction loss experiments
- PatchGAN comparisons
- Hyperparameter experiments
- Final model selection

### Test Notebook

Provides an inference environment for testing the selected trained generator on uploaded sketch images.

## Model Files

Trained model files are not stored directly in this repository due to their size.

The test and experiment notebooks use `gdown` to retrieve the required trained models when needed.

## Reference

This project is based on the Pix2Pix approach introduced in:

**Image-to-Image Translation with Conditional Adversarial Networks**  
Phillip Isola, Jun-Yan Zhu, Tinghui Zhou, and Alexei A. Efros (2017).

## Limitations

- Images are generated at a resolution of `128×128`.
- The project focuses specifically on flower images.
- Quantitative image similarity metrics do not always fully represent perceived visual realism.
- Generated quality depends on the structure and characteristics of the input sketch.
