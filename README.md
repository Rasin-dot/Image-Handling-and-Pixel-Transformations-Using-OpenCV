# Image-Handling-and-Pixel-Transformations-Using-OpenCV 


### Program Developed By:
### Name: Rasindhan R
### Register Number: 212224230222


## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program:

#### 1. Read the image ('exp 1.jpeg.jpeg') using OpenCV imread() as a grayscale image.
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
img = cv2.imread('My_Ph1.jpg', cv2.IMREAD_COLOR)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

#### 2. Print the image width, height & Channel.
```python
img.shape
```

#### 3. Display the image using matplotlib imshow().
```python
img_gray = cv2.cvtColor(img_rgb, cv2.COLOR_RGB2GRAY)
plt.imshow(img_gray,cmap='gray')
plt.show()
```
#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
img=cv2.imread('exp 1.jpeg.jpeg')
cv2.imwrite('dipt_image.png',img)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
img=cv2.imread('exp 1.jpeg.jpeg')
img_rgb = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
plt.imshow(img)
plt.show()
img.shape
```
#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
crop = img_rgb[0:450,200:550] 
plt.imshow(crop[:,:,::-1])
plt.title("Cropped Region")
plt.axis("off")
plt.show()
crop.shape
```
#### 8. Resize the image up by a factor of 2x.
```python
res= cv2.resize(crop,(200*2, 200*2))
```

#### 9. Flip the cropped/resized image horizontally.
```python
flip= cv2.flip(res,1)
plt.imshow(flip[:,:,::-1])
plt.title("Flipped Horizontally")
plt.axis("off")
```
#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
img=cv2.imread('diptimage2.png',cv2.IMREAD_COLOR)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
img_rgb.shape
```
#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
text = cv2.putText(img_rgb, "Apollo 11 Saturn V Launch, July 16, 1969", (300, 700),cv2.FONT_HERSHEY_SIMPLEX, 1, (255, 255, 255), 2)  
plt.imshow(text, cmap='gray')  
plt.title("New image")
plt.show()
```
#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
rcol= (255, 0, 255)
cv2.rectangle(img_rgb, (400, 100), (800, 650), rcol, 3)
```
#### 13. Display the final annotated image.
```python
plt.title("Annotated image")
plt.imshow(img_rgb)
plt.show()
```
#### 14. Read the image ('Boy.jpg').
```python
img =cv2.imread('diptimage3.png',cv2.IMREAD_COLOR)
img_rgb= cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```
#### 15. Adjust the brightness of the image.
```python
m = np.ones(img_rgb.shape, dtype="uint8") * 50
```

#### 16. Create brighter and darker images.
```python
img_brighter = cv2.add(img_rgb, m)  
img_darker = cv2.subtract(img_rgb, m)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(img_rgb), plt.title("Original Image"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(img_brighter), plt.title("Brighter Image"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(img_darker), plt.title("Darker Image"), plt.axis("off")
plt.show()
```
#### 18. Modify the image contrast.
```python
matrix1 = np.ones(img_rgb.shape, dtype="float32") * 1.1
matrix2 = np.ones(img_rgb.shape, dtype="float32") * 1.2
img_higher1 = cv2.multiply(img.astype("float32"), matrix1).clip(0,255).astype("uint8")
img_higher2 = cv2.multiply(img.astype("float32"), matrix2).clip(0,255).astype("uint8")
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(img), plt.title("Original Image"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(img_higher1), plt.title("Higher Contrast (1.1x)"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(img_higher2), plt.title("Higher Contrast (1.2x)"), plt.axis("off")
plt.show()
```
#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
b, g, r = cv2.split(img)
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(b, cmap='gray'), plt.title("Blue Channel"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(g, cmap='gray'), plt.title("Green Channel"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(r, cmap='gray'), plt.title("Red Channel"), plt.axis("off")
plt.show()
```
#### 21. Merged the R, G, B , displays along with the original image
```python
merged_rgb = cv2.merge([r, g, b])
plt.figure(figsize=(5,5))
plt.imshow(merged_rgb)
plt.title("Merged RGB Image")
plt.axis("off")
plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv_img = cv2.cvtColor(img, cv2.COLOR_RGB2HSV)
h, s, v = cv2.split(hsv_img)
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(h, cmap='gray'), plt.title("Hue Channel"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(s, cmap='gray'), plt.title("Saturation Channel"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(v, cmap='gray'), plt.title("Value Channel"), plt.axis("off")
plt.show()
```

#### 23. Merged the H, S, V, displays along with original image.
```python
merged_hsv = cv2.cvtColor(cv2.merge([h, s, v]), cv2.COLOR_HSV2RGB)
combined = np.concatenate((img_rgb, merged_hsv), axis=1)
plt.figure(figsize=(10, 5))
plt.imshow(combined)
plt.title("Original Image  &  Merged HSV Image")
plt.axis("off")
plt.show()
```

## Output:
i) Original image

<img width="428" height="447" alt="image" src="https://github.com/user-attachments/assets/872ecde4-7ac7-4657-9ac5-8a0ecb797bed" />


ii) Image with line , circle, rectangle, text.

<img width="432" height="452" alt="image" src="https://github.com/user-attachments/assets/3ff086b4-a555-4844-afa2-5a472431a1e3" />


<img width="437" height="462" alt="image" src="https://github.com/user-attachments/assets/658be4fa-b576-422e-ba9e-bd5d058f8a27" />


<img width="435" height="460" alt="image" src="https://github.com/user-attachments/assets/da7f30dc-dcf1-484f-a8bb-63e6cd3c4910" />


<img width="432" height="457" alt="image" src="https://github.com/user-attachments/assets/f9e54eb6-b05d-42b7-87a5-fe816e63d9fe" />


iii) Image - HSV , Grayscale , YCeCb and HSV to RGB . 

<img width="432" height="450" alt="image" src="https://github.com/user-attachments/assets/4fa794a8-89f4-4044-afb6-e2269ac9b970" />


<img width="437" height="446" alt="image" src="https://github.com/user-attachments/assets/32d0bf6a-a213-4d03-9c9e-89337264f1ea" />


<img width="417" height="456" alt="image" src="https://github.com/user-attachments/assets/ef82a0b8-c8d4-4359-a95d-c03e88c3d13a" />


<img width="433" height="453" alt="image" src="https://github.com/user-attachments/assets/549b5c1e-23eb-459f-b91e-f232c7ee2c07" />


<img width="430" height="457" alt="image" src="https://github.com/user-attachments/assets/c7242e08-8bb0-430d-ada2-2b02da2f5b6b" />



iv) Image with block .

<img width="440" height="458" alt="image" src="https://github.com/user-attachments/assets/ad4cab9d-5df7-400a-b6f9-c2f3e737d4b1" />


v) Image - Resized Image (Half Size) , Cropped Region of Interest (ROI),Flipped Horizontally ,Flipped Vertically 

<img width="565" height="462" alt="image" src="https://github.com/user-attachments/assets/e6a8481e-2f5e-4c94-8b87-0402b618d238" />


<img width="438" height="458" alt="image" src="https://github.com/user-attachments/assets/5927fd7e-0432-465c-a62a-bfe1369fc32a" />


<img width="437" height="466" alt="image" src="https://github.com/user-attachments/assets/81bcbb99-1860-4cb5-bb2c-46822233f7a8" />


<img width="433" height="455" alt="image" src="https://github.com/user-attachments/assets/4324b721-fcb6-4663-b82f-56d114080366" />





## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

