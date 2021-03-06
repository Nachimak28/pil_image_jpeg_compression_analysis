# JPEG image compression analysis and trying to preserve pixel information

We know that saving an image in the JPEG format leads to inveitable lossy compression.
If dealing with applications which are sensitive to pixel intensities, one must be careful how to handle it.

To prevent any loss happening while saving images, PNG is the format to use.
But saving a PNG image to disc is time consuming. If there are some thousand images to process, the time taken to process and save images as PNG could increase significantly. 

On the other hand, JPEGs are easy to deal with, take less time to save on disc. But leads to data quality degradation. 

**Checkout the [Notebook](https://github.com/Nachimak28/pil_image_jpeg_compression_analysis/blob/main/jpeg_compression_analysis.ipynb) for a working example and some insights**

Example:
![JPEG comparison](https://github.com/Nachimak28/pil_image_jpeg_compression_analysis/blob/0992560d8694015bcdbd23baff52abf9018511b2/assets/jpeg_image_compression_visual_analysis.png)

## Solution:

*  Use PNG or TIFF format to save to the disc

* Use ```subsampling=0``` for saving jpeg images with ```quality=100``` when using Pillow. This still leads to compression happening but shuts down some parts of the JPEG compression algorithm. 

```
pillow_image.save('abcd.jpeg', format='JPEG', quality=100, subsampling=0)
```

The difference with using ```subsampling=0``` can be seen below.


![JPEG subsampling comparison](https://github.com/Nachimak28/pil_image_jpeg_compression_analysis/blob/0992560d8694015bcdbd23baff52abf9018511b2/assets/jpeg_image_compression_visual_analysis_with_subsampling_0.png)

We can't tell the difference with our eyes as we could in the earlier image.


Also a simple analysis of average time taken to save respective image formats for a small 40x80 pixel image on disc is as follows:

![Saving Time comparisons](https://github.com/Nachimak28/pil_image_jpeg_compression_analysis/blob/0992560d8694015bcdbd23baff52abf9018511b2/assets/saving_time_comparison.PNG)


**Insights:**
* PNG takes the longest time. 
* JPEG without subsampling takes shortest time for RGB image. 
* JPEG with or without subsampling takes same time for Grayscale image.
* JPEG with subsampling=0 saving takes time ranging between that of PNG being max and JPEG with subsampling being min.
