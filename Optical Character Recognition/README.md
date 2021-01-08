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

I have this digitalized page of a book (“The big sleep”).
