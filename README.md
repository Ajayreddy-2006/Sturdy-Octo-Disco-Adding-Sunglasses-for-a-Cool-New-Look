# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

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

## Program 
```
import cv2
import matplotlib.pyplot as plt
import numpy as np
faceImage = cv2.imread('passport.jpeg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
![image](https://github.com/user-attachments/assets/140e55e6-d219-46a9-bc95-48380803b02d)
```
glassPNG = cv2.imread('glasses.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
![image](https://github.com/user-attachments/assets/5fee4751-4059-4f0e-adc8-4ab16d5782ee)
```
glassPNG = cv2.resize(glassPNG, (465,285))
print("image Dimension ={}".format(glassPNG.shape))
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
![image](https://github.com/user-attachments/assets/885d9fd0-4256-4c47-a169-238f1753eecd)
```
faceWithGlassesNaive = faceImage.copy()
faceWithGlassesNaive[290:575, 405:870] = glassBGR
plt.imshow(faceWithGlassesNaive[...,::-1])
```
![image](https://github.com/user-attachments/assets/0d603648-e4d5-4554-a84f-67ddf14f7084)
```
glassMask = cv2.merge((glassMask1, glassMask1, glassMask1))
glassMask = np.uint8(glassMask / 255) 

faceWithGlassesArithmetic = faceImage.copy()

eyeROI = faceWithGlassesArithmetic[290:575, 405:870]  
maskedEye = cv2.multiply(eyeROI, (1 - glassMask))  
maskedGlass = cv2.multiply(glassBGR, glassMask) 

eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
plt.figure(figsize=[20,20])
plt.subplot(131); plt.imshow(maskedEye[..., ::-1]); plt.title("Masked Eye Region")
plt.subplot(132); plt.imshow(maskedGlass[..., ::-1]); plt.title("Masked Sunglass Region")
plt.subplot(133); plt
```
![image](https://github.com/user-attachments/assets/ad1b709e-0e31-4e87-8852-1a8de6ecc1e9)
```
faceWithGlassesArithmetic[290:575, 405:870]=eyeRoiFinal
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
![image](https://github.com/user-attachments/assets/a62a433e-3460-461c-a4b3-f63400b6c728)

Feel free to fork, contribute, or customize this project for your creative needs!
