A collection of python scripts to extract objects from microscopic images and reconstruct the object in 
3 dimensions. It's also possible to calculate some metrics on the reconstructed objects. 

This project is based mainly on [Pymesh](https://github.com/PyMesh/PyMesh) and 
[Scikit-Image](https://scikit-image.org/).

## Purpose

The code is based on 5 steps, from the image obtained after acquisition to the calculation of metrics, and
divided in 5 explicitly named python files.

### Image enhancement
I received microscopic images of a dendrite shaft with some spines. 
First of all the signal is very low, so I enhanced the signal from the neck by using two images, one focused
on the neck and another one focused on the spine head. This method is automatic.

### Segmentation
For the segmentation I used a semi-automatic method based on **Chan-Vese algorithm**. 

`An Active Contour Model without Edges, Tony Chan and Luminita Vese, Scale-Space Theories in Computer Vision, 1999, DOI:10.1007/3-540-48236-9_13)`

Each plans are segmented according to the z-stack.
z-Projection of maximum intensity of the image before segmentation (left) and 
z-Projection of maximum intensity of the image after segmentation (right) : 

![Spine before Segmentation](https://github.com/AymericFerreira/spineReconstruction/blob/master/resultExamples/MAX_spine_9.png)
![Spine after Segmentation](https://github.com/AymericFerreira/spineReconstruction/blob/master/resultExamples/MAX_spine_9_segmentedImage.png)




### Reconstruction
For the reconstruction I used a fully-automatic method based on **Marching-Cubes algorithm**

![Spine after reconstruction](https://github.com/AymericFerreira/spineReconstruction/blob/master/resultExamples/MAX_spine_9_segmentedImage.png)


### Optimisation
After reconstruction the mesh can be noisy and not optimised (isolated vertices, duplicated faces, too long or
too short segments). This script consist of some methods to get the best mesh. I am not aiming at giving a 
good looking mesh (aka smoothing), only to fit well from segmented images.

### Metrics
Some metrics to analyse meshes :

    - Center of the base of the mesh    
    - Gravity center
    - Surface
    - Volume
    - Open angle between the vertices and the normal of length
    - Average distance between the base of the mesh and all vertices

![Spine length](https://github.com/AymericFerreira/spineReconstruction/blob/master/resultExamples/spine_length.png)
![Surface](https://github.com/AymericFerreira/spineReconstruction/blob/master/resultExamples/surface.png)
![Volume](https://github.com/AymericFerreira/spineReconstruction/blob/master/resultExamples/volume.png)
![Connectivity](https://github.com/AymericFerreira/spineReconstruction/blob/master/resultExamples/connectivity.png)
![Open angle](https://github.com/AymericFerreira/spineReconstruction/blob/master/resultExamples/open_angle.png)
![Average distance](https://github.com/AymericFerreira/spineReconstruction/blob/master/resultExamples/average_distance.png)
![Gaussian curvature](https://github.com/AymericFerreira/spineReconstruction/blob/master/resultExamples/gauss_curv.png)
![Mean curvature](https://github.com/AymericFerreira/spineReconstruction/blob/master/resultExamples/mean_curv.png)


## Conclusion
I use this collection of script to extract dendritic spines from confocal images and reconstruct the shape
 of the spine in 3 dimensions. I assumed this technique can be used for other 