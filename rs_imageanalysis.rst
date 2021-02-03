.. include:: html_lat.txt



3. Principles of image analysis 
===============================

3.1. Spectral indices for environmental monitoring
--------------------------------------------------
3.1.1. What is a spectral index
````````````````````````````````
A spectral index is a math expression applied to a multispectral image to highlight specific properties of different land covers, their state of alteration, amount or health. Spectral indices combine the reflectance information from multiple spectral bands into one numeric value; thus, they turn satellite images from a qualitative visual inspection tool into a quantitative numerical analysis of environmental phenomena. :numref:`Tab1_SI` shows the most common mathematical formulas.

.. _Tab1_SI:
.. table:: Spectral indices.

   ===================================  =============================================  ===============================================================================  =======
   Family                               Pros                                           Cons                                                                             Example
   ===================================  =============================================  ===============================================================================  =======
   Difference                           Simple                                         Absolute values might depend on external factors (e.g. atmospheric disturbance)  CRI
   Ratio                                Less affected by residual atmospheric effects  Unbounded range of values                                                        RVI
   Normalized                           Can be used to compared different situations   Are not linear                                                                   NDVI
   Any complex mathematical expression  Could map the phenomenon more accurately       Might be challenging to handle or interpret                                      EVI
   ===================================  =============================================  ===============================================================================  =======

The most popular spectral indices are those to retrieve the status of vegetation and crops. However, there are also indices designed to:

- Estimate soil properties,
- Delineate burned areas,
- Monitor built-up features,
- Map water bodies,
- Estimate the abundance of minerals or lithotypes,
- Evaluate the snow cover.

3.1.2. How are designed the spectral indices
````````````````````````````````````````````
Every land feature reflects the sunlight differently (the spectral signature), depending on their physical state, chemical composition, abundance, state of alteration (e.g. weathering) or health (for vegetation). Besides, any variation of these parameters produces a corresponding modification in the spectral signature.

Concerning vegetation, the gap between the low reflectance in the red band (due to chlorophylls), and the high reflectance in the NIR band (due to internal leaf structure) is an indicator of the greenness of the biosphere (:numref:`Fig1_SI`).

.. _Fig1_SI:
.. figure:: /Figure/Fig1_SI.png

	Spectral signature of a decidous tree with highlighted the gap between the red and NIR.

Moreover, the more vigour the vegetation is, or the more green biomass is present, the larger this gap is (:numref:`Fig2_SI`). Therefore, the difference between NIR and red reflectances is used as a proxy for overall amount + health of green vegetation.

.. _Fig2_SI:
.. figure:: /Figure/Fig2_SI.png

	Spectral signatures of healthy and senescing leaves.

.. _Examples-of-spectral-indices-for-studying-vegetation:

3.1.3. Examples of spectral indices for studying vegetation
````````````````````````````````````````````````````````````
**Ratio Vegetation Index (RVI)** |br|
This is the basic greenness vegetation index and is effective over a wide range of different conditions. Equation :eq:`eqSI1` shows its simple mathematical formula:

.. math:: RVI=\frac{\rho_{NIR}}{\rho_{red}}
   :label: eqSI1

RVI is a positive index. The larger the ratio, the more “amount of green and healthy vegetation” is present in the image. Typical values for vegetation cover range from **RVI=4** (for sparse or sick vegetation) to **RVI=30** (for very dense and healthy vegetation). |br|
Unfortunately, RVI is not bounded from above, making it difficult to compare different vegetation covers.

**Normalized Difference Vegetation Index (NDVI)** |br|
This is the most known and used greenness vegetation index. Equation :eq:`eqSI2` shows its mathematical formula:

.. math:: NDVI=\frac{\rho_{NIR}-\rho_{Red}}{\rho_{NIR}+\rho_{Red}}
	:label: eqSI2

NDVI is a normalized index ranging from -1 to 1, but it assumes only positive values for vegetated lands. Thus, threshold **NDVI=0.2** is often used to differentiate bare ground (NDVI<0.2) from vegetated land (NDVI>0.2). |br|
The larger the ratio, the more “amount of green and healthy vegetation” is present in the image. Moderate values (0.2<NDVI<0.6) are typical for shrubs, grass and crops, while higher values (NDVI>0.6) are typical for temperate and tropical forests.

Conversely to RVI, NDVI is bounded from below (0, or more often 0.2) and bounded from above (1). Thus, it is useful to compare different vegetation covers. If we are looking at healthy vegetation, then:

- Moderate values (0.2<NDVI<0.4) are typical for sparse vegetation,
- Intermediate values (0.4<NDVI<0.6) are typical for moderately-density vegetation,
- And higher values (NDVI>0.6) are typical for high-density vegetation.

On the other hand, if we are looking at a fully covered vegetated plot:

- Moderate values (0<NDVI<0.2) are typical for very sick vegetation,
- Intermediate values (0.2<NDVI<0.6) are typical for moderately healthy vegetation,
- And higher values (NDVI>0.6) are typical for very healthy vegetation.

While NDVI is meaningful only for vegetated areas, it can be calculated for all land covers. In this case, NDVI will have the following values:

- NDVI close to -1 is a typical value for clear water,
- -1<NDVI<0 are typical values for polluted water, snow or ice,
- NDVI close to 0 is a typical value for clouds,
- Slightly positive NDVI (0<NDVI<0.2) are typical values for bare soil (i.e. soil without vegetation).


<----------------------------------------------------------------------------------------------------------------------------------------> |br|
<--------------------------------------------------- TO BE COMPLETED -------------------------------------------------> |br|
<------------------------------------------------- ADDITIONAL EXAMPLE -------------------------------------------------------------------> |br|
<----------------------------------------------------------------------------------------------------------------------------------------> |br|


.. hint:: **Monitoring crops.** |br|
	Most satellite-based crop monitoring systems use NDVI, and similar spectral indices, to show farmers which parts of their fields have more stressed vegetation. |br|
	See `CropSAT <https://cropsat.com/>`_ for a free online demo.

.. hint:: **Looking for a specific spectral index?** |br|
	The `Index DataBase <https://www.indexdatabase.de/>`_ is a collection of spectral indices for different applications and sensors. Here you find a selection of `250 spectral indices designed to fit the images of the Sentinel-2 satellite <https://www.indexdatabase.de/db/is.php?sensor_id=96>`_. |br|
	If you like to import these spectral indices into Sentinel Hub EO Browser, try these `javascript <https://custom-scripts.sentinel-hub.com/custom-scripts/sentinel-2/indexdb/>`_.

3.2. Automatic land cover mapping
---------------------------------
3.2.1 Land cover maps vs land use maps
````````````````````````````````````````
Land cover maps describe the geospatial information on different **physical coverages of the Earth’s surface.** They also capture the land cover changes over time. |br|
Example of land cover classes are:

- Farmlands,
- Glaciers,
- Urban areas,
- Forests,
- Lakes.

*A very efficient method to determine the land cover is analysing satellite images.*

On the other hand, land use maps describe **how people use the land and which activities people do in a specific land cover type.**. |br|
Some examples of land use classes are:

- Recreational,
- Residential,
- Commercial,
- Industrial.

Remote sensing systems can provide information on physical coverages. Thus *land use cannot be determined by analysing satellite images.*:numref:`Fig1_Maps` shows the difference between land cover and land use.

.. _Fig1_Maps:
.. figure:: /Figure/Fig1_Maps.png

	Land cover map vs land use map for the city of Toronto (Canada).

3.2.2 From spectral signatures to spectral classes
````````````````````````````````````````````````````

<----------------------------------------------------------------------------------------------------------------------------------------> |br|
<--------------------------------------------------- TO BE COMPLETED -------------------------------------------------> |br|
<----------------------------------------------------------------------------------------------------------------------------------------> |br|


3.2.3 Supervised image classification
`````````````````````````````````````
Automatic mapping of different land cover types is done with supervised image classification. The basic idea is to label each image pixel based on their spectral signature’s similarity with some known land cover locations, called the *training samples*. |br|
The training samples define the map’s legend and define the spectral classes.

<----------------------------------------------------------------------------------------------------------------------------------------> |br|
<--------------------------------------------------- TO BE COMPLETED -------------------------------------------------> |br|
<----------------------------------------------------------------------------------------------------------------------------------------> |br|


3.3. Map validation
-------------------
3.3.1 Precision, bias and accuracy
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

Finally, the third archer fires all his arrows in the target’s centre (:numref:`Fig3_validation`).

.. _Fig3_validation:
.. figure:: /Figure/Fig3_validation.png

	The third archer's shots.

The first archer is **precise** because his arrows always hit the same spot. |br|
Precision refers to the *reproducibility* of the archer’s shots. We can define precision as the degree to which repeated attempts (under unchanged conditions) give the same result. Thus, precision describes the *reliability* of a measure and lack of precision implies random errors.
Nevertheless, the first archer is not accurate because his arrows are systematically displaced from the target’s centre.

The second archer is imprecise because his arrows are not close to each other. However, his arrows do not have a systematic displacement from the target’s centre; thus, he is **unbiased**. |br|
Bias refers to *systematic errors* of the archer’s shots. We can define **bias** as the tendency of repeated attempts (under unchanged conditions) to systematically shift in one direction from the true value.

The third archer is **accurate**. His arrows are all grouped together and placed in the target’s centre. |br|
Accuracy refers to the *closeness* of the archer’s shots to the target centre. We can define **accuracy** as the degree to which repeated attempts (under unchanged conditions) are close to the true value. Thus an accurate attempt is both precise and unbiased.

3.3.2 How much is accurate a map?
`````````````````````````````````
Referring to the mapping process, **accuracy** is the most used performance metric and tells *“how many sites were mapped correctly.”*

Accuracy is estimated using the confusion matrix, a table that relates the actual land cover of some known reference locations, called the *testing samples*, with their predicted values in the map. In this table, rows represent the instances of testing samples in the predicted land cover class, columns represent the instances of testing samples in the actual land cover class. |br|
:numref:`Fig1_confmatrix` shows an example of a confusion matrix computed for a 4-class thematic map. Instances belonging to the main diagonal (green cells) are the number of testing samples classified correctly. |br|
:numref:`Fig2_confmatrix` highlights the number of misclassified testing samples (red cells). Overall, the confusion matrix has 434 testing samples.

.. _Fig1_confmatrix:
.. figure:: /Figure/Fig1_confmatrix.png

	Confusion matrix. Number of testing samples correctly classified.

.. _Fig2_confmatrix:
.. figure:: /Figure/Fig2_confmatrix.png

	Confusion matrix. Number of misclassified testing samples.

.. note:: **What are the testing samples?** |br|
	To evaluate the map’s accuracy, we must compare predicted land cover classes vs actual land cover classes. This is done using the testing samples, which are image pixels randomly collected, but those actual land cover is known. Results are then extended from the testing samples to the full map.

	**GUIDELINE: testing samples must be randomly collected for ALL land cover classes. There should be no less than 50 testing samples for each land cover class.**

**Overall accuracy** |br|
Suppose we want to quantify the proportion of correct predictions, without giving any insight into the single accuracy of land cover classes. *In other words, how many testing samples are globally labelled correctly in the classified map?* |br|
It is called overall accuracy and is usually expressed as a percent,,with 0% being a perfect misclassification and 100% being a perfect classification:

.. math:: Overall\ accuracy=\frac{sum\ of\ testing\ samples\ being\ correctly\ classified}{total\ number\ of\ testing\ sample}
	:label: eqacc1

In our example:

.. math:: Overall\ accuracy=\frac{65+81+85+90}{434}=74.0 \%
	:label: eqacc2

**Producer’s accuracy** |br|
Suppose we want to quantify the proportion of correct predictions for each of the real-world classes. *In other words, for a given land cover class in the real world, how many testing samples are labelled correctly in the classified map?* |br|
This is the accuracy from the point of view of the mapmaker (the producer). It called is called producer’s accuracy (also recall) and is usually expressed as a percent, with 0% being a perfect misclassification and 100% being a perfect classification:

.. math:: Producer\prime s\ accuracy\ for\ class\ i=\frac{number\ of\ testing\ samples\ being\ correctly\ classified\ in\ class\ i}{total\ number\ of\ testing\ sample\ in\ column\ i}
	:label: eqacc3

In our example:

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
Suppose we want to quantify the proportion of correct predictions for each of the mapped classes. *In other words, for a given class in the map, how many testing samples are really present on the ground?.* |br|
This is the accuracy from the point of view of the map user. It called is called user’s accuracy (also precision) and is usually expressed as a percent, with 0% being a perfect misclassification and 100% being a perfect classification:

.. math:: User\prime s\ accuracy\ for\ class\ i=\frac{number\ of\ testing\ samples\ being\ correctly\ classified\ in\ class\ i}{total\ number\ of\ testing\ sample\ in\ row\ i}
	:label: eqacc8

In our example:

.. math:: Producer\prime s\ accuracy\ for\ class\ A=\frac{65}{65+4+22+24}=56.5 \%
	:label: eqacc9

.. math:: Producer\prime s\ accuracy\ for\ class\ B=\frac{81}{6+81+5+8}=81.0 \%
	:label: eqacc10

.. math:: Producer\prime s\ accuracy\ for\ class\ C=\frac{85}{0+11+85+19}=73.9 \%
	:label: eqacc11

.. math:: Producer\prime s\ accuracy\ for\ class\ D=\frac{90}{4+7+3+90}=86.5 \%
	:label: eqacc12

Thus, the classifier is predicting the map’s class A with lower accuracy.

Typically, user’s and producer’s accuracy for a given land cover class are different. In our example, 86.7% of the testing samples for real-world class A are correctly identified as class A in the map (producer’s accuracy). However, only 56.5% of the areas identified as class A in the map are actually being class A on the ground.

.. hint:: **Which is the accuracy of your map?** |br|
	Calculate the overall accuracy and the per-class producer’s accuracy and user’s accuracy of your own map. Try the free `Confusion matrix online calculator <http://www.marcovanetti.com/pages/cfmatrix/>`_.
