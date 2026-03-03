# Probability Density Function Using Generative Adversarial Network (GAN)

## Overview

This project implements a Generative Adversarial Network (GAN) to learn the probability density function (PDF) of a transformed NO₂ concentration variable using only data samples.

The model does not assume any analytical or parametric distribution. Instead, it learns the underlying distribution directly from data and generates synthetic samples that approximate the real probability density.

Roll Number Used: 102303412  
Transformation Parameters:  
. a_r = 0.5  
. b_r = 0.9  

Transformation applied:  
z = x + 0.5 sin(0.9 x)

---

## Project Structure

### 1. Data Loading and Preprocessing

. Loads NO₂ concentration data from `data.csv`  
. Computes transformation parameters using roll number 102303412  
. Applies non-linear sinusoidal transformation  
. Performs Z-score normalization for stable GAN training  

The GAN is trained only on samples of the transformed variable z.

---

### 2. Generator Network

The Generator maps random noise to synthetic samples that resemble the transformed data distribution.

. Input: 1-dimensional noise sampled from N(0,1)  
. Architecture:  
  . Linear: 1 → 32 (ReLU)  
  . Linear: 32 → 32 (ReLU)  
  . Linear: 32 → 1  
. Output: Generated sample z_f  

Purpose: Learn the unknown distribution of z by transforming noise into realistic samples.

---

### 3. Discriminator Network

The Discriminator distinguishes real samples from generated samples.

. Input: Single scalar value  
. Architecture:  
  . Linear: 1 → 32 (LeakyReLU)  
  . Linear: 32 → 32 (LeakyReLU)  
  . Linear: 32 → 1 (Sigmoid)  
. Output: Probability between 0 and 1  

Purpose: Improve generator performance by penalizing unrealistic samples.

---

### 4. GAN Training

The Generator and Discriminator are trained adversarially.

. Loss Function: Binary Cross-Entropy (BCE)  
. Optimizer: Adam  
. Learning Rate: 0.0002  
. Training Process:  
  . Train Discriminator on real samples (label = 1)  
  . Train Discriminator on fake samples (label = 0)  
  . Train Generator to fool Discriminator (label = 1 for generated samples)  

The GAN learns the probability distribution of z purely from observed samples.

---

### 5. PDF Estimation and Visualization

After training:

. Generate 10,000 synthetic samples from Generator  
. Apply inverse normalization  
. Estimate probability density using:  
  . Histogram density estimation  
  . Kernel Density Estimation (Gaussian kernel)  
. Visualize:  
  . Real transformed distribution  
  . Generated distribution  
  . KDE-based PDF curve  

This evaluates how well the GAN captures the underlying density.

---

## Key Features

. Non-parametric PDF learning  
. Roll number-based personalized transformation  
. Adversarial deep learning using PyTorch  
. Data-driven distribution modeling  
. KDE-based smooth density estimation  
. CPU/GPU compatibility  

---

## Dependencies

. numpy  
. pandas  
. matplotlib  
. torch  
. scipy  

---

## Usage

. Ensure `data.csv` contains the NO₂ column  
. Confirm roll number is set to 102303412  
. Run all notebook cells sequentially  
  . Load and preprocess data  
  . Transform x to z  
  . Train GAN  
  . Generate synthetic samples  
  . Estimate and plot PDF  

---

## Output

The final output is a visualization comparing:

. Real transformed data distribution  
. GAN-generated synthetic distribution  
. Estimated probability density curve  

Close alignment between these curves indicates successful learning of the underlying distribution.

---

## Mathematical Concepts

. Non-linear transformation:  
  z = x + 0.5 sin(0.9 x)  

. GAN objective: Binary Cross-Entropy loss  

. Normalization: Z-score scaling  

. Density estimation: Kernel Density Estimation with Gaussian kernel  

This project demonstrates how generative models can learn complex probability distributions directly from data without requiring an analytical expression for the PDF.
