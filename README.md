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
exifdata = image.getexifmet
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

After the sucessfull completion of the step and running all the above mentioned codes we will be sucessfully outputed with the metadata we provided.
