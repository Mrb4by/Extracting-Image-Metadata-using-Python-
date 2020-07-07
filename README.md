# Extracting-Image-Metadata-using-Python-
In this repo, we are trying how we can extract some useful metadata within images using Pillow library in Python.  Devices such as digital cameras, smartphones and scanners uses the EXIF standard to save image or audio files. This standard contains many useful tags to extract which can be useful for forensic investigation, such as the make, model of the device, the exact date and time of image creation and even the GPS information on some devices.
To get started, we need to install Pillow library:

pip3 install Pillow
Open up a new Python file and follow along:

from PIL import Image
from PIL.ExifTags import TAGS
Now this will only work on JPEG image files, take any image you took and test it for this tutorial
# path to the image or video
imagename = "image.jpg"

# read the image data using PIL
image = Image.open(imagename)
After reading the image using Image.open() function, let's call the getexif() method on the image which returns image metadata:

# extract EXIF data
exifdata = image.getexif()
The problem with exifdata variable now is that the field names are just IDs, not a human readable field name, that's why we gonna need the TAGS dictionary from PIL.ExifTags module which maps each tag ID into a human readable text:

# iterating over all EXIF data fields
for tag_id in exifdata:
    # get the tag name, instead of human unreadable tag id
    tag = TAGS.get(tag_id, tag_id)
    data = exifdata.get(tag_id)
    # decode bytes 
    if isinstance(data, bytes):
        data = data.decode()
    print(f"{tag:25}: {data}")
Here is my output:

ExifVersion              : 0220
ShutterSpeedValue        : (406, 100)
ApertureValue            : (1851, 1000)       
DateTimeOriginal         : 2016:11:10 18:22:47
DateTimeDigitized        : 2016:11:10 18:22:47
BrightnessValue          : (-109, 100)        
ExposureBiasValue        : (0, 10)
MaxApertureValue         : (1851, 1000)       
MeteringMode             : 2
Flash                    : 0
FocalLength              : (220, 100)
UserComment              :
ColorSpace               : 1
ExifImageWidth           : 2592
FocalLengthIn35mmFilm    : 22
SceneCaptureType         : 0
ExifImageHeight          : 1944
ImageWidth               : 2592
ImageLength              : 1944
Make                     : samsung
Model                    : SM-G920F
Orientation              : 8
YCbCrPositioning         : 1
ExposureTime             : (1, 17)
XResolution              : (72, 1)
YResolution              : (72, 1)
FNumber                  : (19, 10)
FNumber                  : (19, 10)
ImageUniqueID            : B05LLHA01PM
ISOSpeedRatings          : 400
ISOSpeedRatings          : 400
ISOSpeedRatings          : 400
ISOSpeedRatings          : 400
ResolutionUnit           : 2
ExifOffset               : 226
ExposureMode             : 0
FlashPixVersion          : 0100
WhiteBalance             : 0
Software                 : G920FXXS4DPI4
DateTime                 : 2016:11:10 18:22:4
MakerNote                :       0100                      Z   @         P          
                                                           Z   @         P
A bunch of useful stuff, by quickly googling the Model, I concluded that this image was taken by a Samsung Galaxy S6, run this on images that was captured by other devices and you'll see different (maybe more) fields.

