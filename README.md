# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look
```
Name: Markandeyan Gokul
### Register Number : 212224240086
```

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

Feel free to fork, contribute, or customize this project for your creative needs!

## Code
```

import cv2
import numpy as np
import matplotlib.pyplot as plt

faceImage = cv2.imread('/content/How To Robert Downey Jr Hairstyle at Ryandreher.jpeg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
![image](https://github.com/user-attachments/assets/2dd634f5-bb44-469d-b982-136c4636f9cb)

```
faceImage.shape
```
![image](https://github.com/user-attachments/assets/224cd26b-6ed0-44cc-ae55-f1d3c5d167d9)

```
glassPNG = cv2.imread('/content/584999937b7d4d76317f5ffd (1).png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
![image](https://github.com/user-attachments/assets/f790f7f1-258d-45c5-900c-a810328b933d)

```
glassPNG.shape
```
![image](https://github.com/user-attachments/assets/c214ae0f-8ead-4278-bfc9-5fe421f158b1)

```
glassPNG = cv2.resize(glassPNG,(240,150))
print("image Dimension ={}".format(glassPNG.shape))
```
![image](https://github.com/user-attachments/assets/e777a615-58e5-4db3-96d8-9d3172c6ee44)

```
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]

plt.figure(figsize=[16,16])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
![image](https://github.com/user-attachments/assets/bd61b586-69cb-473e-ba1c-e976de7bcd0b)

```
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[205:355,105:345]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```
![image](https://github.com/user-attachments/assets/b39f012a-a800-4315-9b0a-3dc635b81e0c)

```
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[205:355,105:345]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```
![image](https://github.com/user-attachments/assets/42a289c7-c773-482e-b0c6-6fc53e78b14d)

```
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[205:355,100:340]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
![image](https://github.com/user-attachments/assets/b44da584-0a47-4d69-a97f-d45c0929ba84)

## Result
Program for adding Sunglasses to a Passport Photo Using OpenCV, Successfully executed
