1. Install Tesseract to work with Python and Opencv

Before proceeding with the installation of Tesseract, it’s important to understand all the tools that we are going to use and the purpose of each of them.

These are the tools that we need:

    Python and Opencv: we will use the python programming language and Opencv to load the image, and do some image preprocessing (for example remove the areas where there is no text, remove some noise, apply some image filter to make the text more readable).
    Tesseract: it’s the OCR engine, so the core of the actual text recognition. It takes the image and in return gives us the text.
    Pytesseract: it’s the tesseract binding for python. With this library we can use the tesseract engine with python with just a few lines of code.

1.1 Install Python and Opencv

First of all let’s make sure that you have python and Opencv installed. If not, you can follow this guide to install Opencv and Python on Windows.
1.2 Install Tesseract

Windows
Then it’s the moment to install Tesseract.
If you have windows, go on this page https://github.com/UB-Mannheim/tesseract/wiki, download and install tesseract 64 bit.
If you want to follow step by step the installation process, you can watch it on my video tutorial above.

Linux
On Linux you can simply open the terminal and insert the following commands:

```bib
sudo apt install tesseract-ocr
sudo apt install libtesseract-dev
```

If the commands don’t work, you can refer to the Tesseract website page for more instructions: https://tesseract-ocr.github.io/tessdoc/Home.html.

Mac
To install tesseract on Mac use this command:

```bib
  sudo port install tesseract
```
If this command doesn’t work, check this page for more instructions: https://tesseract-ocr.github.io/tessdoc/Home.html
1.3 Install PyTesseract

Pytesseract is an essential library if we want to use tesseract with Python. It can be easily installed as any other python library using the pip command.
So copy the following commands on your terminal.
```bib
pip install pytesseract
pip3 install pytesseract
2. Read text from an image
```
After we’re done with the installation, it’s the time for us to try Tesseract to read the text from an image.

## **Define all necessary Functions**
```bib
import cv2
import numpy as np
import pytesseract
from google.colab.patches import cv2_imshow

def rectify(h):
    h = h.reshape((4,2))
    hnew = np.zeros((4,2),dtype = np.float32)

    add = h.sum(1)
    hnew[0] = h[np.argmin(add)]
    hnew[2] = h[np.argmax(add)]

    diff = np.diff(h,axis = 1)
    hnew[1] = h[np.argmin(diff)]
    hnew[3] = h[np.argmax(diff)]

    return hnew

def resize_image(image,width,height):
	image = cv2.resize(image,(width,height))
	return image

def gray_image(image):
	image = cv2.cvtColor(image,cv2.COLOR_BGR2GRAY)
	return image

def canny_edge_detection(image):
	blurred_image = cv2.GaussianBlur(image,(5,5), 0)
	edges = cv2.Canny(blurred_image,0,50)
	return edges

def find_contours(image):
	(contours, _) = cv2.findContours(image, cv2.RETR_LIST, cv2.CHAIN_APPROX_NONE)
	contours = sorted(contours, key=cv2.contourArea, reverse=True)
	for c in contours:
	    p = cv2.arcLength(c, True)
	    approx = cv2.approxPolyDP(c, 0.02 * p, True)

	    if len(approx) == 4:
	        target = approx
	        break
	return target

def draw_contours(orig_image,image, target):
	approx = rectify(target)
	pts2 = np.float32([[0,0],[800,0],[800,800],[0,800]])

	M = cv2.getPerspectiveTransform(approx,pts2)
	result = cv2.warpPerspective(image,M,(800,800))

	cv2.drawContours(image, [target], -1, (0, 255, 0), 2)
	result = cv2.cvtColor(result, cv2.COLOR_BGR2GRAY)
	return result

```

*italicized text*# **Text Detection and Detect contours for paper boundary detection**
```bib
target = find_contours(edges)
output = draw_contours(orig,image,target)
text = pytesseract.image_to_string(output)
print("Text Detected: \n"+text)
cv2_imshow(output)
```

```bib
Text Detected: 
 

The
Sparks
Foundation

.inspiring, innovating,
integrating
```
<a >
  <img align="left" width="500px" src="https://github.com/eagleanurag/TSF-Internship/blob/main/Task-1-Optical-Character-Recognition/output.png" />
</a>
