# Uterine Fibroid Detection from Ultrasound Images

**Can a deep learning model tell a uterus with fibroids from one without, using ultrasound alone?**

Uterine fibroids are the most common non-cancerous growth of the womb, and ultrasound is usually the first scan a woman gets. Reading those scans takes trained eyes and time. This project tests whether two well-known image models could support that first read.

## The data

- 1,990 ultrasound images in two classes: fibroid (UF) and no fibroid (NUF)
- Split 80:20 into 1,594 training and 396 test images
- Source: UMD (Uterine Myoma Dataset). The original DICOM scans were converted to JPG for training

## What I did

1. Explored and visualised the images
2. Augmented the training images (shear, zoom, rotation, flips) so the models learn shapes, not individual pictures
3. Fine-tuned two pretrained models: a custom ResNet50 and MobileNetV3 Large
4. Balanced the two classes with class weights and used early stopping to limit overfitting
5. Built an evaluation for sensitivity and specificity as well as accuracy, because in screening a missed fibroid and a false alarm carry different costs

## Results

| Model | Test accuracy |
| --- | --- |
| MobileNetV3 Large with custom layers | 86% |
| ResNet50, best variant (extra layers) | 85% |
| ResNet50 with class balancing | 83% |

Sensitivity and specificity will be added after a rerun. While reviewing this project I found the test images were shuffled during scoring, so those two figures were matched to the wrong labels. The code is now fixed. Accuracy was not affected.

## What this means

Both models classified around 85% of test scans correctly. MobileNetV3 matched the much larger ResNet50, which matters because a lighter model is cheaper and faster to run in a clinic. Accuracy alone does not show how many fibroids were missed, which is why sensitivity comes next.

## Limitations

- The test set also guided training (early stopping), so these scores are likely higher than on new scans
- One dataset, no external validation
- A research exercise, not a diagnostic tool

## Run it

Open fibroid_ultrasound_resnet50_vs_mobilenetv3.ipynb in Google Colab and run all cells. Place the images in a folder called UF_dataset with train and test subfolders.

## Tools

Python, TensorFlow, Keras, scikit-learn, Matplotlib, Seaborn, Google Colab
