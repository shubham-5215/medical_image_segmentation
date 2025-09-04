# Medical Image Segmentation with CE-Net

### ⚙️ Model Architecture

The model is a **Context Encoder Network (CE-Net)**, specifically adapted for this project. The architecture consists of the following key components:

* **Feature Encoder:** A ResNet-34 based encoder is used to extract features from the input images.
* **Dense Atrous Convolution Block (DAC):** This block uses dilated convolutions to enlarge the receptive field and capture multi-scale context without increasing the number of parameters.
* **Residual Multi-kernel Pooling Block (RMP):** This component performs pooling with different kernel sizes to collect features from various scales, enhancing the model's ability to handle objects of different sizes.
* **Feature Decoder:** A decoder network reconstructs the segmentation mask from the encoded features.


***

### 📊 Dataset

The model is trained and validated on a dataset of 2D CT scan images and their corresponding lung masks from Kaggle. The code handles data loading and preprocessing, including resizing images to `448x448` and applying data augmentation techniques like random horizontal and vertical flips, and random contrast adjustments.

A total of 263 image-mask pairs are used, with a portion of the data excluded from the training and testing sets due to issues.

***

### 💻 Setup and Usage

#### Dependencies

The notebook uses the following Python libraries:
* `os`
* `numpy`
* `pandas`
* `math`
* `cv2`
* `sklearn`
* `tensorflow`
* `matplotlib.pyplot`

The model is built using the TensorFlow Keras API.

#### Loss Function and Metrics

The model is compiled with a combined Binary Cross-Entropy and Dice loss function (`bce_dice_loss`) and is trained using the Adam optimizer with an initial learning rate of 0.0001. The training process also includes a learning rate scheduler and early stopping based on the validation Intersection over Union (IoU) metric. The model's performance is monitored using the following metrics:
* Binary Cross-Entropy (`bce`)
* Dice Coefficient (`dice_coeff`)
* Intersection over Union (`iou`)

#### Training and Evaluation

The model is trained for a total of 100 epochs, but training can stop early if the validation IoU does not improve for 15 consecutive epochs. It saves the best model weights based on the validation IoU metric. The notebook concludes by showing example images, ground truth masks, and the model's predictions to visually evaluate the segmentation results.
