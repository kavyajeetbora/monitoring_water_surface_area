# Monitoring Inland Surface Water Area tool

<img src='https://github.com/kavyajeetbora/monitoring_water_surface_area/assets/38955297/3adf7376-06a2-4147-a914-4d0d184a6912' height=400/>

Tool was developed to monitor the inland surface water area of any given area over the years. The tool creates 
- a time-series plot for the total surface area vs year
- a GIF image showing the animation of the changes in surface water over the years

Here is the link to the google colab notebook:

<a target="_blank" href="https://colab.research.google.com/github/kavyajeetbora/monitoring_water_surface_area/blob/master/notebooks/monitoring_inland_water_area_v2.ipynb">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

## 1. Input
This tool takes in a geojson text as input geometry which you can create using this [application](https://www.keene.edu/campus/maps/tool/?coordinates=77.1200409%2C%2011.5324541%0A76.9923248%2C%2011.5062217%0A76.9916382%2C%2011.3467571%0A77.1529998%2C%2011.4261642%0A77.1200409%2C%2011.5324541):

[<img src='https://github.com/kavyajeetbora/monitoring_water_surface_area/assets/38955297/f2b4c6aa-63b3-4f28-a5f3-9fd3ecc06270' height=200/>](https://www.keene.edu/campus/maps/tool/?coordinates=77.1200409%2C%2011.5324541%0A76.9923248%2C%2011.5062217%0A76.9916382%2C%2011.3467571%0A77.1529998%2C%2011.4261642%0A77.1200409%2C%2011.5324541)

Copy the geojson code generated on the right hand side and paste in the colab notebook and rull the notebook

## 2. About the Data: JRC Global Surface Water Dataset

The surface water area is downloaded from:

[JRC Global Surface Water Data](https://developers.google.com/earth-engine/datasets/catalog/JRC_GSW1_4_YearlyHistory): This dataset contains maps of the location and temporal distribution of surface water from 1984 to 2021 and provides statistics on the extent and change of those water surfaces

This dataset has a waterClass property that classifies a pixel whether it is a surface water or not. It has 4 classes: 

|Value|Color|Description|
|-----|------|-------------|
|0|#cccccc|No data|
|1|#ffffff|Not water|
|2|#99d9ea|Seasonal water|
|3|#0000ff|Permanent water|

For this case, to classify a pixel to be water, we will consider class 2 or 3 to be as water and rest of the pixel we can mask them as `nodata`

## 3. Calculating the area

After classifying the water pixel from the dataset, area of each pixel is calculated using `ee.Image.pixelArea()` function. After that the total area is calculated using the `reduceRegion()` function of the google earth engine python api.

## 4. Calculate area for image collection

In this step, calculate the total area of surface water for each image in the image collection.

## 5. Plot the timeseries

Once the total surface water area is calculated for each image, extract the `year` and `area` values from each image and plot the time series:

<img src='https://github.com/kavyajeetbora/monitoring_water_surface_area/assets/38955297/0b61a653-3958-4383-8240-ba69889c9dea' height=300/>

## 6. Plot the timelapse (optional)

Create the timelapse of the surface water over the years using the `gee` and `PIL` python library: 

<img src='https://github.com/kavyajeetbora/monitoring_water_surface_area/assets/38955297/3adf7376-06a2-4147-a914-4d0d184a6912' height=400/>

## Conclusion

A tool was developed to visualize the surface water area for a given area using the JRC global surface water dataset where the dataset contains pixels classified as either surface water or no water. 
Alternatively we can also use remote sensing indices like `NDWI` to detech surface water. Here is a [notebook](https://github.com/kavyajeetbora/monitoring_water_surface_area/blob/master/notebooks/monitoring_inland_water_area.ipynb) showing the results using NDWI.
This method is not very accurate in detecting water but there are more advanced indices that are more accurate. Here is a list of those indices: [Water spectral indices](https://github.com/awesome-spectral-indices/awesome-spectral-indices?tab=readme-ov-file#water)







