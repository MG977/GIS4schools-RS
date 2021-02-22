.. include:: html_lat.txt


2. Principles of image analysis 
===============================

2.1. The spectral signatures
----------------------------

2.1.1. What is a spectral signature
````````````````````````````````````
Each natural and manmade material reflects the sunlight depending on its *chemical composition*, *physical properties*, *texture*, *moisture*, *surface roughness*, and *alteration/degradation state*. |br|
This reflected sunlight is called **reflectance** and is represented with the symbol :math:`\rho`.

In other words, the material’s properties and status define the brightness (i.e. the **reflectance**) of the “colours” (i.e. the **wavelengths**) sensed in the different “lights” (i.e. the **spectral bands**). |br|
This variation of reflectance with wavelengths is called **spectral signature**.

Since each material has a unique spectral signature (like a fingerprint), that means:

- If we know the object material, we can use its spectral signature to monitor health status or degradation (for more details see :any:`Spectral-indices-for-environmental-monitoring`. For exercises see :any:`Monitoring-lake-trophic-state` and :any:`Monitoring-crops-vegetative-stage`),
- If we don’t know the object material, we can use its spectral signature for its identification (for more details see :any:`Automatic-land-cover-mapping`. For exercises see :any:`Mapping-crop-types`).

.. note:: **The acquisition of images in the VISIBLE, NEAR INFRARED, and SHORT-WAVE INFRARED spectral bands and the analysis of their spectral signatures is the principles of multispectral Earth observation.**

When studying the Earth’s ecosystems, we are interested in monitoring our planet’s changes. :numref:`Fig1_signature` shows the distribution of the main land covers on Earth.

.. _Fig1_signature:
.. figure:: /Figure/Fig1_signature.png

	Distribution of main land covers on Earth.

Thus, we use satellites to study how such land covers’ spectral signatures change in time. |br|
:numref:`Fig2_signature` - :numref:`Fig7_signature` show the typical spectral signatures of the main land covers.

.. _Fig2_signature:
.. figure:: /Figure/Fig2_signature.png

	Typical spectral signature of clear water (open Ocean).

.. _Fig3_signature:
.. figure:: /Figure/Fig3_signature.png

	Typical spectral signatures of snow and ice.

.. _Fig4_signature:
.. figure:: /Figure/Fig4_signature.png

	Typical spectral signature of clouds.

.. _Fig5_signature:
.. figure:: /Figure/Fig5_signature.png

	Typical spectral signature of bare soil (unvegetated).

.. _Fig6_signature:
.. figure:: /Figure/Fig6_signature.png

	Typical spectral signature of healthy vegetation.

.. _Fig7_signature:
.. figure:: /Figure/Fig7_signature.png

	Typical spectral signatures of clear water (open Ocean) and polluted water (coastal water with chlorophyll content).



2.1.2. How to measure spectral signatures with satellites
`````````````````````````````````````````````````````````
Remember that satellites record the surface reflectance in different spectral bands and produce multiband grayscale images (:any:`Spectral-characteristics`).

Thus, if we look at a single image pixel and plot its values stored in all the multiband image’s spectral bands, **we extract its spectral signature** (:numref:`Fig8_signature`).

.. _Fig8_signature:
.. figure:: /Figure/Fig8_signature.png

	How to calculate the spectral signature with satellite images.

.. warning:: **Remember to use ONLY atmospherically corrected images!** |br|
	Multispectral satellite images capture both the sunlight reflected by the Earth’s surface and the light scattered by the atmosphere. However, when monitoring the environment, **atmospheric scattering is a noise** that must be removed before image manipulation or analysis.



.. _Spectral-indices-for-environmental-monitoring:

2.2. Spectral indices for environmental monitoring
--------------------------------------------------

2.2.1. What is a spectral index
````````````````````````````````
A spectral index is a math expression applied to a multispectral image to highlight specific properties of different land covers, their state of alteration, amount or health.

Spectral indices combine the reflectance information from multiple spectral bands into **ONE** numeric value. Thus, they turn satellite images *from a qualitative visual inspection tool into a quantitative numerical analysis tool.* |br|
:numref:`Tab1_SI` shows the most common mathematical formulas.

.. _Tab1_SI:
.. table:: Spectral indices.

   ===================================  =============================================  ===============================================================================  ============================================================
   Family                               Pros                                           Cons                                                                             Example
   ===================================  =============================================  ===============================================================================  ============================================================
   Difference                           Simple                                         Absolute values might depend on external factors (e.g. atmospheric disturbance)  `CRI <https://www.indexdatabase.de/db/i-single.php?id=254>`_
   Ratio                                Less affected by residual atmospheric effects  Unbounded range of values                                                        `RVI <https://www.indexdatabase.de/db/i-single.php?id=72>`_
   Normalized                           Can be used to compared different situations   Are not linear                                                                   `NDVI <https://www.indexdatabase.de/db/i-single.php?id=58>`_
   Any complex mathematical expression  Could map the phenomenon more accurately       Might be challenging to handle or interpret                                      `EVI <https://www.indexdatabase.de/db/i-single.php?id=16>`_
   ===================================  =============================================  ===============================================================================  ============================================================

The most popular spectral indices are those to retrieve the status of vegetation and crops. However, there are also indices designed to:

- Estimate soil properties,
- Delineate burned areas,
- Monitor built-up features,
- Map water bodies,
- Estimate the abundance of minerals or lithotypes,
- Evaluate the snow cover,
- And many others.


.. _Examples-of-spectral-indices-for-studying-vegetation:

2.2.2. How spectral indices are designed 
````````````````````````````````````````
Every land feature reflects the sunlight differently (the spectral signature), depending on their physical state, chemical composition, moisture content, state of alteration (e.g. weathering) or health (for vegetation). Besides, any variation of these parameters produces a corresponding modification in the spectral signature.

Let's see some examples for vegetation.

Look at the spectral signature of a vegetated image pixel (:numref:`Fig1_SI`). |br|
The gap between the low reflectance in the red band (due to chlorophylls), and the high reflectance in the NIR band (due to internal leaf structure) is an indicator of the greenness of the biosphere.

.. _Fig1_SI:
.. figure:: /Figure/Fig1_SI.png

	Spectral signature of a decidous tree with highlighted the gap between the red and NIR.

Moreover, the more vigour the vegetation is, or the more green biomass is present, the larger this gap is (:numref:`Fig2_SI`). Thus, the difference between NIR and red reflectances is used as a proxy for overall "amount and health" of green vegetation.

.. _Fig2_SI:
.. figure:: /Figure/Fig2_SI.png

	Colours and spectral signatures of healthy and senescing leaves.

**Ratio Vegetation Index (RVI)** |br|
This is the basic greenness vegetation index and it is effective over a wide range of different conditions. Equation :eq:`eqSI1` shows its simple mathematical formula:

.. math:: RVI=\frac{\rho_{NIR}}{\rho_{red}}
   :label: eqSI1

RVI is a positive index. The larger the ratio, the more “amount of green and healthy vegetation” is present in the image pixel. |br|
Typical values for vegetation cover range from **RVI=4** (parse or sick vegetation) to **RVI=30** (very dense and healthy vegetation). |br|
Unfortunately, RVI is not bounded from above, making it difficult to compare different vegetation covers.

**Normalized Difference Vegetation Index (NDVI)** |br|
This is the most known and used greenness vegetation index. Equation :eq:`eqSI2` shows its mathematical formula:

.. math:: NDVI=\frac{\rho_{NIR}-\rho_{Red}}{\rho_{NIR}+\rho_{Red}}
	:label: eqSI2

NDVI is a normalized index ranging from -1 to 1, but for vegetated lands it has positive values. The larger the ratio, the more “amount of green and healthy vegetation” is present in the image pixel. |br|
The threshold **NDVI=0.2** is often used to differentiate bare ground (NDVI<0.2) from vegetated land (NDVI>0.2). |br|
Moderate values (**0.2<NDVI<0.6**) are typical for shrubs, grass and crops. |br|
Higher values (**NDVI>0.6**) are typical for temperate and tropical forests.

Conversely to RVI, for vegetation cover NDVI is bounded from below (often 0.2) and bounded from above (1). Thus, it is a useful index to compare different vegetation covers and types.

If we are looking at a mixed image pixel with healthy vegetation, then:

- Moderate values (**0.2<NDVI<0.4**) are typical for sparse vegetation,
- Intermediate values (**0.4<NDVI<0.6**) are typical for moderately-density vegetation,
- And higher values (**NDVI>0.6**) are typical for high-density vegetation.

On the other hand, if we are looking at a fully covered vegetated image pixel:

- Moderate values (**0<NDVI<0.2**) are typical for very sick vegetation,
- Intermediate values (**0.2<NDVI<0.6**) are typical for moderately healthy vegetation,
- And higher values (**NDVI>0.6**) are typical for very healthy vegetation.

While NDVI is meaningful ONLY for vegetated areas, it can be calculated for all land covers. In this case, NDVI will have the following values:

- NDVI **close to -1** is a typical value for clear water,
- **-1<NDVI<0** are typical values for polluted water, and for snow or ice,
- NDVI **close to 0** is a typical value for clouds,
- Slightly positive NDVI (**0<NDVI<0.2**) are typical values for bare soil (i.e. soil without vegetation).

.. hint:: **Small activity** |br|
	Most satellite-based crop monitoring systems use NDVI (or similar spectral indices) to show farmers which parts of their fields have more stressed vegetation. |br|
	See `CropSAT <https://cropsat.com/>`_ for a free online demo to highlight where to increase the fertilization rate (suggestion: try the location "Paderno Ponchielli, CR, Italia").

The list of existing spectral indices is very long, but you could build your own spectral index! All you need is the spectral signature of the standard/unaltered state of the land or object you are monitoring and how the phenomenon you are studying affects its reflectance.

.. tip:: **Looking for a specific spectral index?** |br|
	The `Index DataBase <https://www.indexdatabase.de/>`_ is a collection of spectral indices for different applications and sensors. Here you find a selection of `250 spectral indices designed to fit the images of the Sentinel-2 satellite <https://www.indexdatabase.de/db/is.php?sensor_id=96>`_. |br|
	If you like to import these spectral indices into Sentinel Hub EO Browser, try these `javascript <https://custom-scripts.sentinel-hub.com/custom-scripts/sentinel-2/indexdb/>`_.


.. _Automatic-land-cover-mapping:

2.3. Automatic land cover mapping
---------------------------------

2.3.1 Land cover maps vs land use maps
````````````````````````````````````````
Land cover maps describe the geospatial information on different **physical coverages of the Earth’s surface.** They also capture the land cover changes over time. |br|
Example of land cover classes are:

- Farmlands,
- Glaciers,
- Urban areas,
- Forests,
- Lakes.

*A very efficient method to determine the land cover is analysing satellite images.*

On the other hand, land use maps describe **how people use the land and which activities people do in a specific land cover type.** |br|
Some examples of land use classes are:

- Recreational,
- Residential,
- Commercial,
- Industrial.

Remote sensing systems can provide information on physical coverages. Thus *land use cannot be determined by analysing satellite images.*:numref:`Fig1_Maps` shows the difference between land cover and land use.

.. _Fig1_Maps:
.. figure:: /Figure/Fig1_Maps.png

	Land cover map vs land use map for the city of Toronto (Canada).



2.3.2 Supervised image classification
`````````````````````````````````````
Automatic mapping of land cover classes is done with supervised image classification.

The basic idea is to train a mathematical model to recognise spectral signatures. This is done using the spectral signatures of the **training samples**, which are image pixels selected in sites with **KNOWN land cover** (called *training sites*).

For each class, pick some training samples on the satellite image and label with their actual land cover (:numref:`Fig9_signature`). Thus, all the categories have a *reference spectral signature* defined by their training samples (often their mean value) and a *label* (i.e. the land cover class). |br|
**Remember to collect training samples for ALL land cover classes you want to map.** Otherwise, some categories will not be recognised!

.. _Fig9_signature:
.. figure:: /Figure/Fig9_signature.png

	Training sites and training samples..

Now we want the classification algorithm to **predict** each image pixel’s **UNKNOWN land cover** based on their spectral signature’s **similarity** (calculated from the multiband satellite images) with the **KNOWN training samples**. The output is a classification map with all the classes defined by the training samples (:numref:`Fig10_signature`).

**In other words, a classification map is a prediction based on the knowledge of some (limited) training sites.**

.. _Fig10_signature:
.. figure:: /Figure/Fig10_signature.png

	Prediction of the land cover.

.. note:: **How many training samples?** |br|
	Unfortunately, different classification techniques require a different number of (optimal) training samples! |br|
	**A starting point for multispectral images like Sentinel-2 or Landsat could be about 200 training samples (i.e. image pixels) for each class.**

A massive number of classification strategies are used in remote sensing. They have different requirements, constraints and accuracy. |br|
The subject is so vast that we cannot generalize, and it is out-of-scope for this training.

A simple and popular method is the **Minimum Distance (to Means)** classifier. This technique:

1. Calculates the mean spectral signature of each class’ training samples (with KNOWN land cover),
2. Calculates the spectral signature of each image pixels with UNKNOWN land cover,
3. Compares (1) and (2),
4. Assigns each image pixel to the land cover class with the “closest” spectral signature.

.. note:: See :any:`Mapping-crop-types` to check how the Minimum Distance (to Means) classifier works.



<----------------------------------------------------------------------------------------------------------------------------------------> |br|
<--------------------------------------------------- TO BE COMPLETED -------------------------------------------------> |br|
<----------------------------------------------------------------------------------------------------------------------------------------> |br|



2.4. Map validation
-------------------

2.4.1 Precision, bias and accuracy
````````````````````````````````````
To understand the differences between precision, bias and accuracy, let’s see the archer’s analogy.

Assume that three archers are participating in a tournament. |br|
The first archer always hit the same spot, but his arrows are systematically displaced from the target’s centre (:numref:`Fig1_validation`).

.. _Fig1_validation:
.. figure:: /Figure/Fig1_validation.png

	The first archer's shots.

The second archer fires his arrows close to the target’s centre, but scattered (:numref:`Fig2_validation`).

.. _Fig2_validation:
.. figure:: /Figure/Fig2_validation.png

	The second archer's shots.

Finally, the third archer fires his arrows all grouped in the target’s centre (:numref:`Fig3_validation`).

.. _Fig3_validation:
.. figure:: /Figure/Fig3_validation.png

	The third archer's shots.

The first archer is **precise** because his arrows always hit the same spot. Precision refers to the *reproducibility* of the archer’s shots. |br|
We can define precision as the degree to which repeated attempts (under unchanged conditions) give the same result. Thus, precision describes the *reliability* of a measure and lack of precision implies random errors.
Nevertheless, the first archer is not accurate because his arrows are systematically displaced from the target’s centre.

The second archer is **unbiased** but imprecise. His arrows do not have a systematic displacement from the target’s centre, but are not close to each other. Bias refers to *systematic errors* of the archer’s shots. |br|
We can define **bias** as the tendency of repeated attempts (under unchanged conditions) to systematically shift in one direction from the true value.

The third archer is **accurate**. His arrows are all grouped together and placed in the target’s centre. Accuracy refers to the *closeness* of the archer’s shots to the target centre. |br|
We can define **accuracy** as the degree to which repeated attempts (under unchanged conditions) are close to the true value. **Thus, an accurate archer is both precise and unbiased.**

2.4.2 How much is accurate a map?
`````````````````````````````````
Referring to the mapping process, **accuracy** is the most used performance metric and tells *“how many sites were mapped correctly.”*

Map accuracy is estimated using the **confusion matrix**, a table that relates the actual land cover of some KNOWN reference locations, called the *testing samples*, with their predicted values in the map. |br|
In this table, rows represent the instances of testing samples in the predicted land cover class, columns represent the instances of testing samples in the actual land cover class. |br|
:numref:`Fig1_confmatrix` shows an example of a confusion matrix computed for a 4-class thematic map. Instances belonging to the main diagonal (green cells) are the number of testing samples classified correctly. |br|
:numref:`Fig2_confmatrix` highlights the number of misclassified testing samples (red cells). Overall, the confusion matrix has 434 testing samples.

.. _Fig1_confmatrix:
.. figure:: /Figure/Fig1_confmatrix.png

	Confusion matrix. Number of testing samples correctly classified.

.. _Fig2_confmatrix:
.. figure:: /Figure/Fig2_confmatrix.png

	Confusion matrix. Number of misclassified testing samples.

.. note:: **What are the testing samples?** |br|
	To evaluate the map’s accuracy, we must compare predicted land cover classes with actual land cover classes. This is done using the testing samples, which are image pixels randomly collected, but those actual land cover is KNOWN. Results are then extended from the testing samples to the full map.

	**GUIDELINE: testing samples must be randomly collected for ALL land cover classes. There should be no less than 50 testing samples for each land cover class.**

**Overall accuracy** |br|
Suppose we want to quantify the proportion of correct predictions, without giving any insight into the single accuracy of land cover classes. *In other words, how many testing samples are globally labelled correctly in the classified map?* |br|
It is called **overall accuracy** and is usually expressed as a percent, with 0% being a perfect misclassification and 100% being a perfect classification:

.. math:: Overall\ accuracy=\frac{sum\ of\ testing\ samples\ being\ correctly\ classified}{total\ number\ of\ testing\ sample}
	:label: eqacc1

In our example (:numref:`Fig1_confmatrix`):

.. math:: Overall\ accuracy=\frac{65+81+85+90}{434}=74.0 \%
	:label: eqacc2

**Producer’s accuracy** |br|
Suppose we want to quantify the proportion of correct predictions for each of the real-world land cover class. *In other words, for a given land cover class in the real world, how many testing samples are labelled correctly in the classified map?* |br|
This is the accuracy from the point of view of the mapmaker (the producer). It called is called **producer’s accuracy** (also recall) and is usually expressed as a percent, with 0% being a perfect misclassification and 100% being a perfect classification:

.. math:: Producer\prime s\ accuracy\ for\ class\ i=\frac{number\ of\ testing\ samples\ being\ correctly\ classified\ in\ class\ i}{total\ number\ of\ testing\ sample\ in\ column\ i}
	:label: eqacc3

In our example (:numref:`Fig1_confmatrix`):

.. math:: Producer\prime s\ accuracy\ for\ class\ A=\frac{65}{65+6+0+4}=86.7 \%
	:label: eqacc4

.. math:: Producer\prime s\ accuracy\ for\ class\ B=\frac{81}{4+81+11+7}=78.6 \%
	:label: eqacc5

.. math:: Producer\prime s\ accuracy\ for\ class\ C=\frac{85}{22+5+85+3}=73.9 \%
	:label: eqacc6

.. math:: Producer\prime s\ accuracy\ for\ class\ D=\frac{90}{24+8+19+90}=63.8 \%
	:label: eqacc7

Thus, the classifier is mapping real world class A with higher accuracy.

**User’s accuracy** |br|
Suppose we want to quantify the proportion of correct predictions for each of the mapped classes. *In other words, for a given class in the map, how many testing samples are really present on the ground?* |br|
This is the accuracy from the point of view of the map user. It called is called **user’s accuracy** (also precision) and is usually expressed as a percent, with 0% being a perfect misclassification and 100% being a perfect classification:

.. math:: User\prime s\ accuracy\ for\ class\ i=\frac{number\ of\ testing\ samples\ being\ correctly\ classified\ in\ class\ i}{total\ number\ of\ testing\ sample\ in\ row\ i}
	:label: eqacc8

In our example (:numref:`Fig1_confmatrix`):

.. math:: User\prime s\ accuracy\ for\ class\ A=\frac{65}{65+4+22+24}=56.5 \%
	:label: eqacc9

.. math:: User\prime s\ accuracy\ for\ class\ B=\frac{81}{6+81+5+8}=81.0 \%
	:label: eqacc10

.. math:: User\prime s\ accuracy\ for\ class\ C=\frac{85}{0+11+85+19}=73.9 \%
	:label: eqacc11

.. math:: User\prime s\ accuracy\ for\ class\ D=\frac{90}{4+7+3+90}=86.5 \%
	:label: eqacc12

Thus, the classifier is predicting the map’s class A with lower accuracy.

Typically, user’s and producer’s accuracy for a given land cover class are different. In our example (:numref:`Fig1_confmatrix`), 86.7% of the testing samples for real-world class A are correctly identified as class A in the map (producer’s accuracy). However, only 56.5% of the areas identified as class A in the map are actually being class A on the ground.

.. hint:: **Small activity** |br|
	Which is the accuracy of your map? |br|
	Calculate the overall accuracy and the per-class producer’s accuracy and user’s accuracy of your own map. Try the free `Confusion matrix online calculator <http://www.marcovanetti.com/pages/cfmatrix/>`_.
