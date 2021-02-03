.. include:: html_lat.txt


4. Hands-on exercises
=======================

<----------------------------------------------------------------------------------------------------------------------------------------> |br|
<--------------------------------------------------- TO BE COMPLETED -------------------------------------------------> |br|
<----------------------------------------------------------------------------------------------------------------------------------------> |br|



4.1. Monitoring lake’s trophic state
------------------------------------
4.1.1 The environmental problem
````````````````````````````````
The trophic state of a water body describes the amount of nutrients (mainly phosphorus and nitrogen) available to grow aquatic vegetation and phytoplankton. However, when water becomes rich with nutrients, phytoplankton’s rapid growth (called **algae bloom**) could cause negative impacts on the marine environment, like:

- The disruption of the normal ecosystem functioning,
- The consumption of oxygen in the water, resulting in the death of aquatic organisms and fishes,
- The reduction of sunlight reaching aquatic plants under the water surface,
- The production of harmful toxins.

Lakes are usually classified into 4 trophic states, according to chlorophyll’s concentration present in the water. :numref:`Tab1_WQ` shows the most common definitions.

.. _Tab1_WQ:
.. table:: Chlorophyll’s concentration and trophic level of lakes.

   ==============  ===========================  ====================================
   Trophic level   Chlorophyll’s concentration  Primary productivity
   ==============  ===========================  ====================================
   Oligotrophic    0-2.6 mg/m3                  Low due to nutrient deficiency
   Mesotrophic     2.6-20 mg/m3                 Intermediate
   Eutrophic       20-56 mg/m3                  High due to excessive nutrients
   Hypereutrophic  >56 mg/m3                    Very High due to excessive nutrients
   ==============  ===========================  ====================================

.. Warning:: **The role of climate change** |br|
   Climate change may indirectly cause eutrophication by increasing runoff from the land, affecting nutrient load, due to increased precipitation resulting from global warming.

4.1.2 Scope of the exercise
````````````````````````````
This exercise shows a very simple method to monitor the eutrophic level of a lake with satellites.

4.1.3 Satellite images
````````````````````````
The analysis is done using ten cloud-free Sentinel-2 images collected in the following dates of Summer 2016:

- 18 July 2016,
- 4 August 2016,
- 14 August 2016,
- 17 August 2016,
- 24 August 2016,
- 27 August 2016,
- 3 September 2016,
- 13 September 2016,
- 23 September 2016,
- 26 September 2016.

.. warning:: **Remember to use ONLY atmospherically corrected images!** |br|
   Today (February 2021), Sentinel-2 data collected on 2016 are only provided only as ``L1C`` products. That means these satellite images are NOT corrected for the atmospheric disturbance. Thus, **they are NOT ready for image processing!**

   Atmospheric correction is an advanced topic not covered in training. Thus, this exercise uses the most simple atmospheric compensation technique, called Dark Object Subtraction (DOS), to derive pseudo ``L2A`` products.

.. _The-modelling-WQ:

4.1.4 The modelling
````````````````````
The Ratio Vegetation Index (RVI) is a spectral index proportional to chlorophyll’s concentration. Thus, it could be used as a proxy for its estimation. |br|
Phytoplankton are microorganisms that float on the water body and contain chlorophyll. Thus, they could be detected with RVI.

In this exercise we use a simple linear regression model described by equation :eq:`eqWQ1`:

.. math:: Chl\ \left[mg/m^3\right]=a\times RVI+b
   :label: eqWQ1

For Sentinel-2 images, we calculate Equation :eq:`eqWQ1` as follows:

.. math:: Chl\ \left[mg/m^3\right]=a\times\frac{\rho_{Band 4}}{\rho_{Band 3}}+b
   :label: eqWQ2

4.1.5 Chlorophyll’s concentration data
````````````````````````````````````````
The Ratio Vegetation Index (RVI) is proportional to chlorophyll’s concentration, but it does not represent its exact value. Thus, we need some experimental data of known chlorophyll’s concentration vs RVI value for the calibration of the equation :eq:`eqWQ2`.


<----------------------------------------------------------------------------------------------------------------------------------------> |br|
<--------------------------------------------------- TO BE COMPLETED -------------------------------------------------> |br|
<----------------------------------------------------------------------------------------------------------------------------------------> |br|


:numref:`Fig1_WQ` shows Lake Trasimeno with superimposed five sampling locations (green dots) where the chlorophyll’s concentration was measured on 18 July 2016. These data are used for the model’s calibration.

.. _Fig1_WQ:
.. figure:: /Figure/Fig1_WQ.png

   Lake Trasimeno with superimposed the sampling locations (green dots).

4.1.6 QGIS set-up
`````````````````
Open QGIS. Go to the menu bar and click ``Plugins`` → ``Manage and Install Plugins...`` (:numref:`Fig3_WQ_Plugins`).

.. _Fig3_WQ_Plugins:
.. figure:: /Figure/Fig3_WQ_Plugins.png

   Sample screenshot.

In the search bar write **SCP** and select the ``Semi-Automatic Classification Plugin``. Press ``Install plugin`` in the bottom-right corner of the window and close the window (:numref:`Fig4_WQ_Install_Plugin`).

.. _Fig4_WQ_Install_Plugin:
.. figure:: /Figure/Fig4_WQ_Install_Plugin.png

   Sample screenshot.

In QGIS main window, select ``New Empty Project`` (:numref:`Fig2_WQ_New_Project`).

.. _Fig2_WQ_New_Project:
.. figure:: /Figure/Fig2_WQ_New_Project.png

   Sample screenshot.

4.1.7 Prepare the satellite images
````````````````````````````````````
Open the Semi-Automatic Classification Plugin (SCP) (:numref:`Fig5_WQ_Open_SCP`).

.. _Fig5_WQ_Open_SCP:
.. figure:: /Figure/Fig5_WQ_Open_SCP.png

   Sample screenshot.

In the left-side window open ``Preprocessing`` → ``Sentinel-2`` (:numref:`Fig6_WQ_Import_Sentinel2`). This tool provides the pre-processing tasks to prepare the satellite images for the analysis.

.. _Fig6_WQ_Import_Sentinel2:
.. figure:: /Figure/Fig6_WQ_Import_Sentinel2.png

   Sample screenshot.

Select the following parameters (:numref:`Fig7_WQ_Import_Sentinel2_part2`):

- ``Directory containing Sentinel-2 bands:`` open the folder where you saved the Sentinel-2 image ``S2A_MSIL1C_20160718T101032_N0204_R022_T32TQN_20160718T101028.SAFE`` → ``S2A_MSIL1C_20160718T101032_N0204_R022_T32TQN_20160718T101028.SAFE`` → ``GRANULE`` → ``L1C_T32TQN_A005596_20160718T101028`` → ``IMG_DATA``,
- ``Select metadata file (MTD_MSI):`` select the file **MTD_MSIL1C** in the folder ``S2A_MSIL1C_20160718T101032_N0204_R022_T32TQN_20160718T101028.SAFE`` → ``MTD_MSIL1C``,
- ``Apply DOS1 atmospheric correction:`` select this option. This command applies the simple DOS atmospheric correction to the satellite images.

Click the button **RUN** and select the output directory (:numref:`Fig7_WQ_Import_Sentinel2_part2`).

.. _Fig7_WQ_Import_Sentinel2_part2:
.. figure:: /Figure/Fig7_WQ_Import_Sentinel2_part2.png

   Sample screenshot.

The outcomes of this processing are 10 spectral bands:

- 4 bands with 10-meters spatial resolution saved in GeoTiff format,
- 6 bands (with original 20-meters spatial resolution) resampled to match the 10-meters spatial resolution of the first 4 bands, saved in GeoTiff format.

Now we want to merge all the spectral bands in a single image. This is called **multiband image** (or **multispectral image**).

In the Semi-Automatic Classification Plugin window, select **Band set** (Upper left corner) and flag the option **Create raster of band set (stack bands)** (:numref:`Fig8_CROP_20m_wrong_band_order`).

Click the button **RUN** and select the output directory (:numref:`Fig8_WQ_Create_Stack`). Name the output file with the name of the input image followed by ``stack_raster``. For example ``RT_T32TQN_20160718T101032_B0stack_raster``.

.. _Fig8_WQ_Create_Stack:
.. figure:: /Figure/Fig8_WQ_Create_Stack.png

   Sample screenshot.

Remove from QGIS all the layer, except ``RT_T32TQN_20160718T101032_B0stack_raster``. To remove a layer, right-click the layer in the windows **Layers** and select ``Remove layer``.

The image is loaded in QGIS. However, its colours are not what we expect because the satellite’s spectral bands are not loaded in the correct order (:numref:`Fig9_WQ_Sentinel2_Visaulization`).

.. _Fig9_WQ_Sentinel2_Visaulization:
.. figure:: /Figure/Fig9_WQ_Sentinel2_Visaulization.png

   Sample screenshot.

To solve this problem, we need to tell QGIS which spectral bands correspond to Red, Green and Blue.

.. _Load-the-satellite-images-with-the-correct-colours:

4.1.8 Load the satellite images with the correct colours
`````````````````````````````````````````````````````````
Right-click on the image name → ``Properties`` → ``Symbology`` and set (:numref:`Fig10_WQ_Layer_Symbology`):

- ``Red band:`` set ``Band 03``. The satellite’s band 3 collects the Red reflected sunlight,
- ``Green band:`` set ``Band 02``. The satellite’s band 2 collects the Green reflected sunlight,
- ``Blue band:`` as ``Band 01``. The satellite’s band 1 collects the Blue reflected sunlight.

Click the button ``Apply`` and then click the button ``OK``.

.. _Fig10_WQ_Layer_Symbology:
.. figure:: /Figure/Fig10_WQ_Layer_Symbology.png

   Sample screenshot.

Now QGIS shows the satellite image with the correct colours (:numref:`Fig11_WQ_True_Color`).

.. _Fig11_WQ_True_Color:
.. figure:: /Figure/Fig11_WQ_True_Color.png

   Sample screenshot.

4.1.9 Resize the image
````````````````````````
The Sentinel-2 images cover a larger area than our study area. Thus, we can resize them before starting the data processing.

Import in QGIS the vector layer ``..\Study_area\trasimeno_proj.shp``.
To resize (i.e. clip) the satellite image, search in the **Processing Toolbox** panel the command **clip** and open the tool **Clip raster by mask layer** in the *GDAL package* (:numref:`Fig13_WQ_Toolbox_Clip`).

.. _Fig13_WQ_Toolbox_Clip:
.. figure:: /Figure/Fig13_WQ_Toolbox_Clip.png

   Sample screenshot.

.. hint:: If the Processing Toolbox panel is not loaded, open the QGIS menu ``View`` → ``Panels`` and select ``Processing Toolbox``.

A new window appears (:numref:`Fig14_WQ_Clip_parameters`). In the **Clip Raster by Mask Layer** window, set the following parameters:

- ``Input layer:`` set ``RT_T32TQN_20160718T101032_B0stack_raster``,
- ``Mask layer:`` set ``Trasimeno_proj``,
- ``Source CRS:`` Not set,
- ``Target CRS:`` Not set,
- ``Assign a specified nodata value to output bands:`` Not set,
- ``Create an output alpha band:`` unselect,
- ``Match the extent of the clipped raster to the extent o the mask layer:`` select,
- ``Keep resolution of input raster:`` select,
- ``Set output file resolution``: unselect,
- ``X Resolution of output bands``: Not set,
- ``Y Resolution of output bands``: Not set,
- ``Clipped (mask):`` Click on the three dots [...]. Select ``Save to file`` and browse to the folder where you saved the merged images. Now save the new resized (clipped) image with the file name ``RT_T32TQN_20160718T101032_Clip``.

.. _Fig14_WQ_Clip_parameters:
.. figure:: /Figure/Fig14_WQ_Clip_parameters.png

   Sample screenshot.

Click the button ``RUN``, then ``CLOSE``.

The new clipped image will appear in QGIS (:numref:`Fig15_WQ_Lake_Clip`). Now the image is smaller; thus, the subsequent data processing will be faster.

.. _Fig15_WQ_Lake_Clip:
.. figure:: /Figure/Fig15_WQ_Lake_Clip.png

   Sample screenshot.

Like it happened when importing the full-size Sentinel-2 image, the resized image is loaded with the wrong order’s spectral bands. Thus, Lake Trasimeno has the wrong colour.

Repeat the steps described in :any:`Load-the-satellite-images-with-the-correct-colours` (:numref:`Fig16_WQ_Lake_Clip_Symbology`).

.. _Fig16_WQ_Lake_Clip_Symbology:
.. figure:: /Figure/Fig16_WQ_Lake_Clip_Symbology.png

   Sample screenshot.

Now QGIS shows the satellite image with the correct colours (:numref:`Fig17_WQ_Lake_True_color_visualization`).

.. _Fig17_WQ_Lake_True_color_visualization:
.. figure:: /Figure/Fig17_WQ_Lake_True_color_visualization.png

   Sample screenshot.

4.1.10 Calculate the Ratio Vegetation Index
````````````````````````````````````````````
Remember we use the spectral model described in (:any:`The-modelling-WQ`). Thus we calculate the Ratio Vegetation Index (RVI) (:any:`Examples-of-spectral-indices-for-studying-vegetation`) with Sentinel-2’s band 3 (B3) and band 4 (B4).

Now we do some calculations with images using the **Raster Calculator**. This tool allows evaluating equations based on the image pixel values. |br|
Open **Raster Calculator** from the menu ``Raster`` → ``Raster Calculator...`` (:numref:` Fig18_WQ_Raster_Calculator`).

.. _Fig18_WQ_Raster_Calculator:
.. figure:: /Figure/Fig18_WQ_Raster_Calculator.png

   Sample screenshot.

Now, we have to write Equation :eq:`eqWQ3` using QGIS syntax, so the software can understand it.

.. math:: RVI=frac{\rho_{Band 4}}{\rho_{Band 3}}
   :label: eqWQ3

With the help of the calculator buttons, write the following expression in ``Raster Calculator Expression``:

"RT_T32TQN_20160718T101032_Clip@4/RT_T32TQN_20160718T101032_Clip@3"

.. hint:: **How to read QGIS equations?**

   "RT_T32TQN_20160718T101032_Clip@4" means: |br|
   *“pick each pixel value of the resized image RT_T32TQN_20160718T101032_Clip for band 4 (@4)”*.

   "RT_T32TQN_20160718T101032_Clip@3" means: |br|
   *“pick each pixel value of the resized image RT_T32TQN_20160718T101032_Clip for band 3 (@3)”*.

   **Equations are calculated on a pixel basis. Thus the same equation is computed for each image pixel individually. The results are shown in a new image.**

In **Result Layer** click on the three dots ``[...]`` next to ``Output layer`` and select where you want to save the classification results. Name the file ``Ratio_b4_b3.tif`` (:numref:`Fig19_WQ_Raster_Calculator_expression`).

.. _Fig19_WQ_Raster_Calculator_expression:
.. figure:: /Figure/Fig19_WQ_Raster_Calculator_expression.png

   Sample screenshot.

The output is a grayscale image, where each pixel contains its RVI value just computed (:numref:`Fig20_WQ_B4_b3_Index`).

.. _Fig20_WQ_B4_b3_Index:
.. figure:: /Figure/Fig20_WQ_B4_b3_Index.png

   Sample screenshot.

4.1.11 Sample the RVI in the calibration sites
````````````````````````````````````````````````
We know chlorophyll’s concentration in the five calibration sites because it was measured *on site*. But also we need the satellite-derived RVI.

Import in QGIS the layer ``..Points/Sampling_2016.shp``. This file contains five small red polygons where the chlorophyll was sampled (:numref:`Fig21_WQ_Points`).

.. _Fig21_WQ_Points:
.. figure:: /Figure/Fig21_WQ_Points.png

   Sample screenshot.

To extract from the satellite image the RVI of the calibration sites, we use the **Zonal statistics** tool. |br|
Unlike the **Cell Statistics** algorithm that computes per-pixel statistics, the **Zonal statistics** algorithm calculates per-polygon statistics. That means the output (e.g. minimum, maximum, sum, count, *etc.*) is calculated only on pixels within the selected polygons.

Search in the **Processing Toolbox** panel for the **Zonal statistics** (or write *zonal statistics* in the Processing Toolbox search bar) and double-click on it (:numref:`Fig22_WQ_Toolbox_Zonal_Statistics`).

.. _Fig22_WQ_Toolbox_Zonal_Statistics:
.. figure:: /Figure/Fig22_WQ_Toolbox_Zonal_Statistics.png

   Sample screenshot.

.. hint:: If the Processing Toolbox panel is not loaded, open the QGIS menu ``View`` → ``Panels`` and select ``Processing Toolbox``.

The Zonal Statistics window opens. Select the following parameters (:numref:`Fig23_WQ_Zonal_Statistics_parameters`): 

- **Raster layer:** set to ``Ratio_b4_b3``,
- **Raster band:** set to ``Band 1 (Gray)``,
- **Vector layer containing zones:** set to ``Sampling_2016``,
- **Output column prefix:** set to ``b4/b3_``,
- Statistics to calculate:

   - Click on the three dots ``[...]``,
   - Select **Mean** and unselect all the other statistics,
   - Click the blue back arrow, located in the upper-left corner.

Click the button ``RUN`` to execute the data processing.

.. _Fig23_WQ_Zonal_Statistics_parameters:
.. figure:: /Figure/Fig23_WQ_Zonal_Statistics_parameters.png

   Sample screenshot.

The data processing adds a new attribute (i.e. column) to the attribute table of the shapefile **Sampling_2016**. It is called **Ratio_b4_b3**. |br|
The new attribute **Ratio_b4_b3** contains the RVI mean value of each polygon (i.e. rows) (:numref:`Fig24_WQ_Points_attribute_table`).

.. _Fig24_WQ_Points_attribute_table:
.. figure:: /Figure/Fig24_WQ_Points_attribute_table.png

   Sample screenshot.

4.1.12 Build the spectral model
````````````````````````````````````````````````











<----------------------------------------------------------------------------------------------------------------------------------------> |br|
<--------------------------------------------------- TO BE COMPLETED -------------------------------------------------> |br|
<----------------------------------------------------------------------------------------------------------------------------------------> |br|















4.2 Mapping crop types
------------------------
4.2.1 The environmental problem
`````````````````````````````````
Agriculture is highly dependent on the climate. For any crop type, the effect of climate change will depend on the crop’s optimal temperature and water availability for growth and reproduction.

The temperature increase will change farming practices. In some countries, warming could increase productivity or allow farmers to shift to crops that are currently grown in warmer areas. A higher temperature could exceed the crop’s optimum temperature in some other countries, and production will decline.

.. Warning:: **The role of climate change.** |br|
   Overall, climate change may make it difficult to grow crops the same ways and in the same places as in the past.

4.2.2 Scope of the exercise
`````````````````````````````
This exercise shows a very simple method to map crop types with satellites.

4.2.3 Study area
````````````````````
The study area is Wallonia, the southern and most extensive region of Belgium. The climate is temperate, moderately humid, with an annual rainfall of about 780 mm well distributed over the year. |br|
The soil is loamy and moderately well-drained; thus, it does not require irrigation. The main winter crops are Wheat and Barley, while the main Summer crops are Potatoe, Sugar beet and Maize. Field size ranges from 3 ha to 15 ha.


4.2.4 Satellite images
`````````````````````````
The analysis is done using two cloud-free Sentinel-2 images collected in the following dates of Spring-Summer 2018:

- 18 April 2018,
- 27 June 2018.

.. Warning:: The Sentinel-2 images used in this exercise are supplied as atmospherically corrected ``L2A`` products. **THUS, THEY CAN BE USED WITHOUT ANY FURTHER PRE-PROCESSING.**

4.2.5 Land cover information
````````````````````````````````
Information on the actual land cover is provided as polygons (shapefiles). Each red polygon in :numref:`Fig1_CROP_Study_area` stands for a crop field with available information on the cultivated crop type.

In the study area are cultivated the following main crops:

- Barley,
- Chicory,
- Wheat,
- Flax (linseed),
- Maize,
- Peas,
- Potato,
- Sugar beet.

.. _Fig1_CROP_Study_area:
.. figure:: /Figure/Fig1_CROP_Study_area.png

   Farmlands in the Wallonia region.

4.2.6 Methods
````````````````
The mapping process uses the **Minimum Distance** supervised classification algorithm. The training samples, called *Region Of Interest (ROI)* in QGIS, are extracted from available land cover polygons.

4.2.7 QGIS set-up
````````````````````
Open QGIS and select ``New Empty Project`` in the main window (:numref:`Fig2_CROP_New_Project`).

.. _Fig2_CROP_New_Project:
.. figure:: /Figure/Fig2_WQ_New_Project.png

   Sample screenshot.

.. _Prepare-multiband-files-for-10-meter-satellite-images:

4.2.8 Prepare multiband files for 10-meter satellite images
`````````````````````````````````````````````````````````````
Open the folder ``S2A_MSIL2A_20180418T104021_N0207_R008_T31UFS_20180418T125356.SAFE`` → ``GRANULE`` → ``L2A_T31UFS_A014734_20180418T104512`` → ``IMG_DATA`` → ``R10m``.

Each 10-meter Sentinel-2’s spectral band is stored as a single file. Now select the spectral bands with 10 m spatial resolution, those file names end with  (:numref:`Fig3_CROP_Band_selection`):

- “..._B02_10m.jp2”,
- “..._B03_10m.jp2”,
- “..._B04_10m.jp2”,
- “..._B08_10m.jp2”.

.. _Fig3_CROP_Band_selection:
.. figure:: /Figure/Fig3_CROP_Band_selection.png

   Sample screenshot.

Import these files in QGIS. In the menu bar open ``Layer`` → ``Data Source Manager`` (:numref:`Fig101_Data_Source_Manager`).

.. _Fig101_Data_Source_Manager:
.. figure:: /Figure/Fig101_Data_Source_Manager.png

   Sample screenshot.

On the left-side menu, select **Raster** (:numref:`Fig102_Import_Raster`).

.. _Fig102_Import_Raster:
.. figure:: /Figure/Fig102_Import_Raster.png

   Sample screenshot.

Select the following parameters:

- ``Source type:`` select ``File (Default option)``,
- ``Source:``

- Click on the three dots ``[...]``, browse to the folder ``S2A_MSIL2A_20180418T104021_N0207_R008_T31UFS_20180418T125356.SAFE`` → ``GRANULE`` → ``L2A_T31UFS_A014734_20180418T104512`` → ``IMG_DATA`` → ``R10m``,
- Select the four images (files “.jp2”),
- Click on ``Open`` (:numref:`Fig103_Select_bands`).

.. _Fig103_Select_bands:
.. figure:: /Figure/Fig103_Select_bands.png

   Sample screenshot.

Click **Add** (:numref:`Fig104_add_bands`).

.. _Fig104_add_bands:
.. figure:: /Figure/Fig104_add_bands.png

   Sample screenshot.

Now create the multiband file. |br|
In QGIS menu bar open the ``Raster`` menu and select ``Miscellaneous`` → ``Merge`` (:numref:`Fig4_CROP_Merge`).

.. _Fig4_CROP_Merge:
.. figure:: /Figure/Fig4_CROP_Merge.png

   Sample screenshot.

In the **merge window** click on the three dots ``[...]`` at the end of the ``Input layers`` parameter (:numref:`Fig5_CROP_Merge_window`).

.. _Fig5_CROP_Merge_window:
.. figure:: /Figure/Fig5_CROP_Merge_window.png

   Sample screenshot.

Select all the layers and click **OK** (:numref:`Fig6_CROP_Merge_band_selection`).

.. Caution:: Be careful to check that files are sorted in the following order: **B02, B03, B04 and B08.** |br|
   If the order is different, the saved image will have the wrong order’s spectral bands, and the image processing will give incorrect results.

.. _Fig6_CROP_Merge_band_selection:
.. figure:: /Figure/Fig6_CROP_Merge_band_selection.png

   Sample screenshot.

Select the following parameters in the **Merge window**:

- ``Grab pseudocolor table from first layer:`` unselected,
- ``Place each input file into a separate band:`` select,
- ``Output data type:`` Float32,
- ``Merged:`` Click on the three dots ``[...]``:

   - Save to File
   - Select the folder where you want to save the image. Use the following file name ``S2_20180418_10m.tif``.

.. _Fig105_Merge_settings_10m:
.. figure:: /Figure/Fig105_Merge_settings_10m.png

   Sample screenshot.

4.2.9 Prepare multiband files for 20-meter satellite images
`````````````````````````````````````````````````````````````
Repeat the same data processing done for the 10-meter satellite images, and create multiband files for the 20-meter satellite images.

Remove the open layers from QGIS and open the folder ``S2A_MSIL2A_20180418T104021_N0207_R008_T31UFS_20180418T125356.SAFE`` → ``GRANULE`` → ``L2A_T31UFS_A014734_20180418T104512`` → ``IMG_DATA`` → ``R20m``.

Each 20-meter Sentinel-2’s spectral band is stored as a single file. Now select the spectral bands with 20 m spatial resolution, those file names end with (:numref:`Fig7_CROP_20m_band_selection`):

- “…B02_20m.jp2”,
- “…B03_20m.jp2”,
- “…B04_20m.jp2”,
- “…B05_20m.jp2”,
- “…B06_20m.jp2”,
- “…B07_20m.jp2”,
- “…B8A_20m.jp2”,
- “…B11_20m.jp2”,
- “…B12_20m.jp2”.

.. _Fig7_CROP_20m_band_selection:
.. figure:: /Figure/Fig7_CROP_20m_band_selection.png

   Sample screenshot.

Now create the multiband file by merging together the spectral bands, as described in :any:`Prepare-multiband-files-for-10-meter-satellite-images`.

.. Caution:: Be careful when selecting the input layers. Band **B8A** is the last entry by default. **IT MUST BE MOVED AFTER BAND B07** (:numref:`Fig8_CROP_20m_wrong_band_order`).

.. _Fig8_CROP_20m_wrong_band_order:
.. figure:: /Figure/Fig8_CROP_20m_wrong_band_order.png

   Sample screenshot.

Once band **B8A** is moved AFTER band B07, the list will look like :numref:`Fig9_CROP_20m_correct_band_order`).

.. _Fig9_CROP_20m_correct_band_order:
.. figure:: /Figure/Fig9_CROP_20m_correct_band_order.png

   Sample screenshot.

Select the following parameters in the **Merge window**:

- ``Grab pseudocolor table from first layer:`` unselected,
- ``Place each input file into a separate band:`` select,
- ``Output data type:`` Float32,
- ``Merged:`` Click on the three dots ``[...]``:
- ``Save to File: `` Save the output file as ``S2_20180418_20m.tif`` in the same folder used for 10-meters Sentinel-2 images.

.. _Fig106_Merge_Settings_20m:
.. figure:: /Figure/Fig106_Merge_Settings_20m.png

   Sample screenshot.

4.2.10 Resize the image
````````````````````````
The Sentinel-2 images cover a larger area than our study area. Thus, we can resize them before starting the classification process.

In the menu bar select ``Layer`` → ``Data Source Manager`` (:numref:`Fig107_Data_Source_Manager_Vector`).

.. _Fig107_Data_Source_Manager_Vector:
.. figure:: /Figure/Fig107_Data_Source_Manager_Vector.png

   Sample screenshot.

In the left-side menu select **Vector** and set the following parameters (:numref:`Fig109_Add_Vector`):

- ``Source Type:`` set ``File (Default setting)``,
- ``Source:`` Click on the three dots ``[...]`` and browse to the folder ``Study_area\``. Select the file ``Wallonia_Study_Area.shp`` (:numref:`Fig108_Select_Study_Area_Layer`).

Click the button ``Add``.

.. _Fig109_Add_Vector:
.. figure:: /Figure/Fig109_Add_Vector.png

   Sample screenshot.

.. _Fig108_Select_Study_Area_Layer:
.. figure:: /Figure/Fig108_Select_Study_Area_Layer.png

   Sample screenshot.

A rectangle will appear in the bottom left corner of the image (:numref:`Fig110_Study_Area_Visualization`). This is the extent of the study area.

.. _Fig110_Study_Area_Visualization:
.. figure:: /Figure/Fig110_Study_Area_Visualization.png

   Sample screenshot.

To resize (i.e. clip) the satellite image, search in the **Processing Toolbox** panel the command *clip* and open the tool *Clip raster by mask layer* in the GDAL package (:numref:`Fig111_Clip_tool`).

.. hint:: If the Processing Toolbox panel is not loaded, open the QGIS menu ``View`` → ``Panels`` and select ``Processing Toolbox``.
.. _Fig111_Clip_tool:
.. figure:: /Figure/Fig111_Clip_tool.png

   Sample screenshot.

In the **Clip Raster by Mask Layer** window, set the following parameters (:numref:`Fig112_Clip_tool_Settings`):

- ``Input layer:`` set ``S2_20180418_20m``,
- ``Mask layer:`` set ``Wallonia_Study_Area``,
- ``Source CRS:`` Not set,
- ``Target CRS:`` Not set,
- ``Assign a specified nodata value to output bands:`` Not set,
- ``Create an output alpha band:`` unselect,
- ``Match the extent of the clipped raster to the extent o the mask layer:`` select,
- ``Keep resolution of input raster:`` select,
- ``Set output file resolution``: unselect,
- ``X Resolution of output bands``: Not set,
- ``Y Resolution of output bands``: Not set,
- ``Clipped (mask):`` Click on the three dots [...]. Select ``Save to file`` and browse to the folder where you saved the merged images. Now save the new resized (clipped) image the file name ``S2_20180418_20m_clip``.

Click the button ``RUN``.

.. _Fig112_Clip_tool_Settings:
.. figure:: /Figure/Fig112_Clip_tool_Settings.png

   Sample screenshot.

The new clipped image will appear in QGIS (:numref:`Fig113_Clipped_image`). Now the image is smaller; thus, the subsequent data processing will be faster.

.. _Fig113_Clipped_image:
.. figure:: /Figure/Fig113_Clipped_image.png

   Sample screenshot.

Remove all the layers from QGIS.

4.2.11 Create the training samples for image classification
`````````````````````````````````````````````````````````````
In our study area, farmlands are much more extensive than 20 m x 20 m. Thus, we use the 20-meters Sentinel-2 image to perform the classification process. On the one hand we do not need greater detail, and on the other hand the 20-meters images have much more spectral bands, thus allowing a better recognition of crop types.

Import in QGIS the Sentinel-2 multiband image of 27 June 2018 ``S2_20180627_20m_clip.tif`` (:numref:`Fig114_Import_Clipped_Image`).

.. _Fig114_Import_Clipped_Image:
.. figure:: /Figure/Fig114_Import_Clipped_Image.png

   Sample screenshot.

Import in QGIS the shapefile ``Wallonia_2018_In_Situ_Extracted_v1.shp`` that describes a field with available information on the cultivated crop type. This information is stored in the attribute table (:numref:`Fig10_CROP_Dataset_attribute_table`). |br|
To see the attributes, right-click the layer ``Wallonia_2018_In_Situ_Extracted_v1.shp`` and select ``Open Attribute Table``.

.. _Fig10_CROP_Dataset_attribute_table:
.. figure:: /Figure/Fig10_CROP_Dataset_attribute_table.png

   Sample screenshot.

The attribute **LC** (i.e. land cover) describes the crop type, and the attribute **Class_code** assigns a unique numerical code to each land cover class. The database uses the coding scheme of :numref:`Tab1_CROP`.

.. _Tab1_CROP:
.. table:: Land cover classes and class code numbering.

   ===============  ==========
   Land cover       Class code
   ===============  ==========
   Barley           1
   Chicory          2
   Common wheat     3
   Flax (Linseed)   4
   Grassland        5
   Maize            6
   Not Agriculture  7
   Peas             8
   Potato           9
   Sugar beet       10
   ===============  ==========

.. important:: We need some *a priori* information on the land cover for EACH crop type we want to map. This information is used as training samples during the classification process.

Now we have to tell the software which satellite image we want to classify (:numref:`Fig11_CROP_Define_band_set`). |br|
Open the **SCP** tool window. |br|
Select **Band set** from the left-side menu. |br|
Set the parameter ``Multiband image list`` to the Sentinel-2 multiband image ``S2_20180627_20m``.

.. _Fig11_CROP_Define_band_set:
.. figure:: /Figure/Fig11_CROP_Define_band_set.png

   Sample screenshot.

Then we need to convert the shapefile into ROI (Region of Interest) for the classification process to use these polygons as training samples.

Open the **SCP Dock** (:numref:`Fig12_CROP_SCP_Dock_tool`).

.. tip:: If you don’t have the SCP Dock window opened in QGIS, select: ``View`` → ``Panels`` → ``Activate SCP Dock``.

.. _Fig12_CROP_SCP_Dock_tool:
.. figure:: /Figure/Fig12_CROP_SCP_Dock_tool.png

   Sample screenshot.

Open the tab ``Training input`` and click on the icon **Create a new ROI file** (:numref:`Fig13_CROP_Create_new_ROI_file`).

.. _Fig13_CROP_Create_new_ROI_file:
.. figure:: /Figure/Fig13_CROP_Create_new_ROI_file.png

   Sample screenshot.

Select the folder where you want to save the training samples file and name it ``Training``.

Open the main SCP window again and go to the panel ``Basic Tools panel`` → ``Import signatures`` (:numref:`Fig14_CROP_Import_signature`).

.. _Fig14_CROP_Import_signature:
.. figure:: /Figure/Fig14_CROP_Import_signature.png

   Sample screenshot.

and click the button ``Import vector`` (:numref:`Fig15_CROP_Signature_from_vector`)

.. _Fig15_CROP_Signature_from_vector:
.. figure:: /Figure/Fig15_CROP_Signature_from_vector.png

   Sample screenshot.

Now open the shapefile ``Wallonia_2018_In_Situ_Extracted_v1.shp`` (:numref:`Fig16_CROP_Select_the_vector_file`). |br|
The software shows the following information:

- ``MC ID field`` (i.e. Macro Class ID field): this field requires a numerical code to identify the classes we want to classify. QGGIS allows to use an attribute of the shapefile; thus we use the **Class_code**,
- ``MC Name field`` (i.e. Macro Class Name field): this field requires the class name linked with the **MC ID field**. The attribute containing the class name is **LC**,
- In this exercise, we will not use the fields ``C ID`` (i.e. Class ID) and ``C Name`` (i.e. Class Name). Thus, select the same attributes of the Macro Classes.

.. _Fig16_CROP_Select_the_vector_file:
.. figure:: /Figure/Fig16_CROP_Select_the_vector_file.png

   Sample screenshot.

Click the ``Import vector`` icon (:numref:`Fig17_v2_CROP_ROI_Creation`).

.. _Fig17_v2_CROP_ROI_Creation:
.. figure:: /Figure/Fig17_v2_CROP_ROI_Creation.png

   Sample screenshot.

.. important:: Wait until the importing is finished! |br|
   This process might take some minutes, depending on your PC performances.

4.2.12 Automatic mapping of crop types
````````````````````````````````````````
Let’s start the classification process.

Open the ``SCP window`` and go to the ``Band processing`` panel. Select ``Classification`` and set the parameters as follows (:numref:`Fig18_CROP_Classification_tool`):

- ``Select input band set:`` set **1**. We set earlier the Sentinel-2 multiband image ``S2_20180627_20m`` as the band set 1,
- ``Use:`` flag **MC ID**. We set earlier the crop type as ``MC ID``,
- ``Algorithm:`` select **Minimum Distance**. We use the minimum distance classification algorithm,
- ``Threshold:`` set **0**. We are telling the algorithm to classify all the image pixels.

.. _Fig18_CROP_Classification_tool:
.. figure:: /Figure/Fig18_CROP_Classification_tool.png

   Sample screenshot.

Click the button ``RUN`` and select the folder where you want to save the classification map. Name the folder ``20180627_Classification`` (:numref:`Fig115_Save_Classification`).

.. _Fig115_Save_Classification: 
.. figure:: /Figure/Fig115_Save_Classification.png

   Sample screenshot.

The data processing transforms the input satellite image into a land cover map of crops types. Each pixel of the map is coded with its **Class_code** (:numref:`Tab1_CROP`). All the image pixels whose land cover is not recognized are assigned the **"special" Class_code 0** (unclassified). :numref:`Fig19_CROP_Classification_result` shows the result.

.. _Fig19_CROP_Classification_result:
.. figure:: /Figure/Fig19_CROP_Classification_result.png

   Sample screenshot.

4.2.13 Simple analysis of results
````````````````````````````````````
If we want to estimate the most farmed crop, right-click on the classification layer ``20180627_Classification`` and select ``Properties`` (:numref:`Fig20_CROP_Classification_properties`).

.. _Fig20_CROP_Classification_properties:
.. figure:: /Figure/Fig20_CROP_Classification_properties.png

   Sample screenshot.

In the left-side menu select ``Histogram`` and then click the button ``Compute Histogram``. |br|
This tool counts the number of pixels for each land cover class, called **frequency** (:numref:`Fig21_CROP_Classification_histogram`). |br|
We see that the crop Flax (Linseed), *coded with the class number 4*, is the most farmed in the study area.

.. _Fig21_CROP_Classification_histogram:
.. figure:: /Figure/Fig21_CROP_Classification_histogram.png

   Sample screenshot.

.. hint:: If we have some information on the land cover and satellite images for the same location, but in a different period, we can compare how the farming of crop types changes in time.

.. hint:: If we have some information on the land cover and satellite images for the same period, but in a different location, we can compare how crop types are farmed in other places.


4.3 Monitoring crops’ vegetative stage
----------------------------------------
.. _The-environmental-problem-agricultural-productivity:

4.3.1 The environmental problem
`````````````````````````````````
Agricultural productivity is strictly related to environmental factors. For example:

- Rising levels of CO2 reduce protein content and essential minerals in most crops, including Wheat, Soybeans, and Rice, resulting in a loss of food quality,
- Extreme temperature and precipitation can prevent crops from growing,
- Floods and droughts can harm crops and reduce productivity,
- Droughts can cause desertification,
- Many insects and fungi prosper under warmer temperatures, wetter climates, and increased CO2 levels,
- Pollutants reduce agricultural productivity.

.. Warning:: **The role of climate change** |br|
   Climate change is modifying the temperature and the precipitation regimes, intensifying extreme weather, and increasing desertification in many fragile territories. That has an impact on the health of vegetation and crops.

3.2 Scope of the exercise
````````````````````````````
This exercise shows satellites’ use to evaluate Barley and Potatoes’ vegetative stage in different periods of the year.

4.3.3 Study area
````````````````````
The study area is Wallonia, the southern and most extensive region of Belgium. The climate is temperate, moderately humid, with an annual rainfall of about 780 mm well distributed over the year. |br|
The soil is loamy and moderately well-drained; thus, it does not require irrigation. The main winter crops are Wheat and Barley, while the main Summer crops are Potatoe, Sugar beet and Maize. Field size ranges from 3 ha to 15 ha.

4.3.4 Satellite images
````````````````````````
The analysis is done using two cloud-free Sentinel-2 images collected in the following dates of Spring-Summer 2018:

- 18 April 2018,
- 27 June 2018.

.. Warning:: The Sentinel-2 images used in this exercise are supplied as atmospherically corrected ``L2A`` products. **THUS, THEY CAN BE USED WITHOUT ANY FURTHER PRE-PROCESSING.**

4.3.5 Land cover information
````````````````````````````````
Information on the actual land cover is provided as polygons (shapefiles). Each red polygon in :numref:`Fig1_NDVI_Study_area` stands for a crop field with available information on the cultivated crop type.

In the study area are cultivated the following main crops:

- Barley,
- Chicory,
- Wheat,
- Flax (linseed),
- Maize,
- Peas,
- Potato,
- Sugar beet.

.. _Fig1_NDVI_Study_area:
.. figure:: /Figure/Fig1_CROP_Study_area.png

   Farmlands in the Wallonia region.

4.3.6 Methods
````````````````
The monitoring of vegetative stage is done using the **Normalized Difference Vegetation Index (NDVI)** (:any:`Examples-of-spectral-indices-for-studying-vegetation`) described by Equation :eq:`eqSI2`:

.. math:: NDVI=\frac{\rho_{NIR}-\rho_{Red}}{\rho_{NIR}+\rho_{Red}}

4.3.7 QGIS set-up
````````````````````
Open QGIS and select ``New Empty Project`` in the main window (:numref:`Fig2_NDVI_New_Project`).

.. _Fig2_NDVI_New_Project:
.. figure:: /Figure/Fig2_WQ_New_Project.png

   Sample screenshot.

.. _Calculate_NDVI:

4.3.8 Calculate NDVI
````````````````````````
To compute NDVI, we need only the NIR and Red bands. Thus, we use Sentinel-2’s highest spatial resolution images (10-meters).

Open the folder ``…\Sentinel-2\10m`` and import in QGIS the image ``S2_20180418_10m``.

.. note:: Prepare the input multiband satellite images as described in :any:`Prepare-multiband-files-for-10-meter-satellite-images`.

Now we do some calculations with images using the **Raster Calculator**. This tool allows evaluating equations based on the image pixel values. |br|
Open **Raster Calculator** from the menu ``Raster`` → ``Raster Calculator...`` (:numref:`Fig1_NDVIRaster_calculator`).

.. _Fig1_NDVIRaster_calculator:
.. figure:: /Figure/Fig1_NDVI_Raster_calculator.png

   Sample screenshot.

We want to calculate the NDVI for each of the satellite image pixels (for more information refer to :any:`Examples-of-spectral-indices-for-studying-vegetation`):

.. math:: NDVI=\frac{\rho_{NIR}-\rho_{Red}}{\rho_{NIR}+\rho_{Red}}

Before writing the calculation formula for NDVI, we need to know which are the Red and NIR spectral bands. |br|
Remember that Sentinel-2’s 10-meters resolution Red band is band 3 (B3), and its 10-meters resolution NIR band is band 4 (B4). Thus, the NDVI equation written for Sentinel-2 images becomes Equation :eq:`eqNDVI1`:

.. math:: NDVI=\frac{\rho_{Band\ 4}-\rho_{Band\ 3}}{\rho_{Band\ 4}+\rho_{Band\ 3}}
   :label: eqNDVI1

Equation :eq:`eqNDVI1` can also be written as follows:

.. math:: NDVI=(B4-B3)/(B4+B3)
   :label: eqNDVI2

where: |br|
B3 are the pixel values in Band 3 (i.e. the Red band), |br|
B4 are the pixel values in Band 4 (i.e. the NIR band).

Now, we have to write Equation :eq:`eqNDVI2` using QGIS syntax, so the software can understand it. |br|
With the help of the calculator buttons, write the following expression in ``Raster Calculator Expression``:

("S2A_20180418_10m@4" - "S2A_20180418_10m@3")/("S2A_20180418_10m@4"+"S2A_20180418_10m@3")

.. hint:: **How to read QGIS equations?**

   "S2A_20180418_10m@4" means: |br|
   *“pick each pixel value of image S2A_20180418_10m for band 4 (@4)”*.

   "S2A_20180418_10m@3" means: |br|
   *“pick each pixel value of image S2A_20180418_10m for band 3 (@3)”*.

   **Equations are calculated on a pixel basis. Thus the same equation is computed for each image pixel individually. The results are shown in a new image.**

In **Result Layer** click on the three dots ``[...]`` next to ``Output layer`` and select where you want to save the classification results. Name the folder ``..\NDVI`` and the file ``2018_04_18_NDVI``  (:numref:`Fig2_NDVI_Raster_Calculator_window`).

.. _Fig2_NDVI_Raster_Calculator_window:
.. figure:: /Figure/Fig2_NDVI_Raster_Calculator_window.png

   Sample screenshot.

The output is a grayscale image, where each pixel contains its NDVI value just computed (:numref:`Fig3_NDVI_April_NDVI`).

.. _Fig3_NDVI_April_NDVI:
.. figure:: /Figure/Fig3_NDVI_April_NDVI.png

   Sample screenshot.

Now repeat the data processing again for the satellite image collected on 27 June 2018 (multiband file ``S2_20180627_10m``). |br|
Remember to use **"S2A_20180627_10m@3"** and **"S2A_20180627_10m@4"** in the expression for calculating NDVI on 27 June 2018. Save results as ``..\NDVI\2018_06_27_NDVI``.

.. tip:: To simplify the processing, remove all the layer from QGIS and start from scratch (:any:`Calculate_NDVI`).

3.9 Select the NDVI information for Barley and Potato
````````````````````````````````````````````````````````
Once computed the NDVI for both the satellite images, we want to compare Barley and Potato’s vegetative stage in April and June.

Open the attribute table of the shapefile **Wallonia_2018_In_Situ_Extracted_v1**: right-click on ``Wallonia_2018_In_Situ_Extracted_v1`` → ``Open Attribute Table`` (:numref:`Fig4_NDVI_Open_Attribute_table`).

.. _Fig4_NDVI_Open_Attribute_table:
.. figure:: /Figure/Fig4_NDVI_Open_Attribute_table.png

   Sample screenshot.

To filter the attribute table by land cover type (the attribute **LC**), we need the tool **Select feature using an expression.** Click the icon showed in (:numref:`Fig5_NDVI_Select_by_expression`).

.. _Fig5_NDVI_Select_by_expression:
.. figure:: /Figure/Fig5_NDVI_Select_by_expression.png

   Sample screenshot.

The window **Select by Expression** opens. Expand the tree **Fields and Values** and double click on ``LC`` (:numref:`Fig6_NDVI_select_LC`).

.. _Fig6_NDVI_select_LC:
.. figure:: /Figure/Fig6_NDVI_select_LC.png

   Sample screenshot.

The main window **Expression** automatically fills with “LC”. |br|
Click the button ``=`` and then click the button ``All Unique``. This command shows, on the right side, the list of all available land cover in the shapefile **Wallonia_2018_In_Situ_Extracted_v1**. |br|
Double click on ``Barley (winter)``. Now the expression in the main window becomes "LC" =  'Barley (winter)' (:numref:`Fig7_NDVI_Select_Barley`).

.. _Fig7_NDVI_Select_Barley:
.. figure:: /Figure/Fig7_NDVI_Select_Barley.png

   Sample screenshot.

We are telling the software to select the land cover Barley. But we want to select also Potato. |br|
Expand the tree **Operators** and double click on the **OR** operator (:numref:`Fig8_NDVI_Select_OR_operator`).

.. _Fig8_NDVI_Select_OR_operator:
.. figure:: /Figure/Fig8_NDVI_Select_OR_operator.png

   Sample screenshot.

Expand the tree **Fields and Values** again, double click **LC**, click the button ``=`` and then click the button ``All Unique``. Now double click on ``Potato``.

The expression in the main window becomes "LC"  =  'Barley (winter)'  OR  "LC"  =  'Potato (non-early)' (:numref:`Fig9_NDVI_Select_Potato`). We are now telling the software to select from the attribute table all the polygons whose land cover is Barley or Potato.

.. _Fig9_NDVI_Select_Potato:
.. figure:: /Figure/Fig9_NDVI_Select_Potato.png

   Sample screenshot.

Click the button **Select Features** (bottom right of the window) and then **Close** the window.

As a result, 13 polygons out of 55 are selected. Now export these polygons in a new layer. Right-click on the layer name → ``Export`` → ``Save Selected Features As...`` (:numref:`Fig10_NDVI_Export_Selected_Features`).

.. _Fig10_NDVI_Export_Selected_Features:
.. figure:: /Figure/Fig10_NDVI_Export_Selected_Features.png

   Sample screenshot.

A window opens. Select the following parameters (:numref:`Fig11_NDVI_Save_Vector_Layer_as`):

- ``Format:`` set to ``ESRI Shapefile``,
- ``File name:`` Double-click on the three dots ``[...]`` and select the folder where you want to save the file. Name it: ``Barley_Potato``,
- ``Layer name:`` Leave this field empty,
- ``CRS:`` Keep the default value. QGIS automatically takes the Coordinate Reference System (CRS) of the original file.
- Keep the default values for the other parameters.

.. _Fig11_NDVI_Save_Vector_Layer_as:
.. figure:: /Figure/Fig11_NDVI_Save_Vector_Layer_as.png

   Sample screenshot.

4.3.10 Compare winter crops and summer crops
````````````````````````````````````````````````
Now we want to compare the different vegetative stage of Barley and Potato. For this task, we use the **Zonal statistics** tool. |br|
Unlike the **Cell Statistics** algorithm that computes per-pixel statistics, the **Zonal statistics** algorithm calculates per-polygon statistics. That means the output (e.g. minimum, maximum, sum, count, *etc.*) is calculated only on pixels within the selected polygons.

Search in the **Processing Toolbox** panel for the **Zonal statistics** (or write *zonal statistics* in the Processing Toolbox search bar) and double-click on it (:numref:`Fig11_NDVI_Zonal_Statistics`).

.. hint:: If the Processing Toolbox panel is not loaded, open the QGIS menu ``View`` → ``Panels`` and select ``Processing Toolbox``.

.. _Fig11_NDVI_Zonal_Statistics:
.. figure:: /Figure/Fig11_NDVI_Zonal_Statistics.png

   Sample screenshot.

The Zonal Statistics window opens. Select the following parameters (:numref:`Fig12_NDVI_Zonals_Statistics_Parameters`): 

- **Raster layer:** set to ``2018_04_18_NDVI``,
- **Raster band:** set to ``Band 1 (Gray)``,
- **Vector layer containing zones:** set to ``Barley_Potato``,
- **Output column prefix:** set to ``18_04_``,
- Statistics to calculate:

   - Click on the three dots ``[...]``,
   - Select **Mean** and unselect all the other statistics,
   - Click the blue back arrow, located in the upper-left corner (:numref:`Fig13_NDVI_Zonal_statistics_select_mean`).

Click the button ``RUN`` to execute the data processing.

.. _Fig12_NDVI_Zonals_Statistics_Parameters:
.. figure:: /Figure/Fig12_NDVI_Zonals_Statistics_Parameters.png

   Sample screenshot.

.. _Fig13_NDVI_Zonal_statistics_select_mean:
.. figure:: /Figure/Fig13_NDVI_Zonal_statistics_select_mean.png

   Sample screenshot.

The data processing adds a new attribute (i.e. column) to the attribute table of the shapefile **Barley_Potato**. It is called **18_04_mean**. |br|
The new attribute **18_04_mean** contains the NDVI mean value of each polygon (i.e. rows) (:numref:`Fig14_NDVI_18_April_NDVI_in_the_attribute_table`).

.. _Fig14_NDVI_18_April_NDVI_in_the_attribute_table:
.. figure:: /Figure/Fig14_NDVI_18_April_NDVI_in_the_attribute_table.png

   Sample screenshot.

Now compute the zonal statistics for the satellite image collected on 27 June 2018 (file ``2018_06_27_NDVI``).
Remember to set the **Raster layer** to ``2018_06_27_NDVI``, and **Output column prefix:** to ``27_06_``. |br|
:numref:`Fig15_NDVI_27_June_NDVI_in_the_attribute_table` shows the result.

.. _Fig15_NDVI_27_June_NDVI_in_the_attribute_table:
.. figure:: /Figure/Fig15_NDVI_27_June_NDVI_in_the_attribute_table.png

   Sample screenshot.

s4.3.11 Simple analysis of results
````````````````````````````````````
Let’s discuss our findings.

- **Mid April:**

   - **Barley has high NDVI values**, corresponding to a high amount of healthy biomass (just before harvesting),
   - **Potato has low NDVI values**, corresponding to a low biomass amount (because the seedling is not grown yet).

- **Late June:**

   - **Barley has low NDVI values**, corresponding to a low biomass amount (because the crop has been harvested),
   - **Potato has high NDVI values**, corresponding to a high amount of healthy biomass (because the crop grew up).

We thus **deduce** that *Barley is cultivated as a winter crop* in the study area. |br|
In contrast, we **deduce** that *Potato is cultivated as a summer crop* in the study area.

.. note::

   It is interesting to notice that, unlike one may expect, not all the fields with the same crop have the same NDVI values in the period of full growth. This phenomenon is easily explained because the seedlings’ health and vigour may vary due to non-optimal environmental conditions.

   Thus, fields cultivated with Barley in winter, or fields cultivated with Potato in summer, showing abnormal low NDVI values could have productivity issues related to environmental factors, as recalled in :any:`The-environmental-problem-agricultural-productivity`.
