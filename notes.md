# Earth and Environmental Sciences

Index

* [Spatial Data Model](#spatial-data-model)
* [Spatial Statistics](#spatial-statistics)

## Spatial Data Model

### Distances
There are different ways of getting a distance between two points, Euclidean and Non-euclidean geometry.

|Flat | Curved|
|---|---|
|Lines perpendicular to the same line are parallel | Line perperdicular to the same line can intersect
| Sum of the angles of a triangle is $180^o$ | Sum of the angles of a triangle does not igual $180^o$
| Pythagorean Theorem holds | Pythagorean Theorem does not hold
| Circumference of a circle is $C=2\pi R$ | On a sphere $C<2\pi R$
| A finite area must have a boundary | A surface can have a finite area without any boundary (for example, a sphere)
| Shortest distance between two points is a straight line | Shortest distance is a *geodesic*

### Data types

- *Raster Images*. Made of pixels, or tiny dots that use color and tone to produce the image. Pixels appear like little squares on graph paper when the image is zoomed in or enlarged.  These images are created by digital cameras, by scanning images into a computer or with raster-based software. Each image can only contain a fixed number of pixels; the amount of pixels determines the quality of the image. This is known as resolution. More pixels results in better quality at the same or larger sizes of the original, but this also increases the size of the file and the amount of space it takes to store the file. The lower the number of pixels, the lower the resolution. Resolution limits the size the image can be scaled up without being able to see pixels. However, a high resolution image printed at a small size will cause the pixels to "cram" together and will make the image look as unprofessional as not having enough pixels in a large image.

- *Vector Images*. Also known as scalable vector graphics (SVG). These graphics consist of anchored dots and connected by lines and curves. Because these graphics are not based on pixels, they are known as resolution independent, which makes them infinitely scalable. Their lines are sharp, without any loss in quality or detail, no matter what their size. These graphics are also device-independent, which means their quality doesn't depend on the number of dots available on a printer or the number of pixels on a screen. Because they consist of lines and anchor points, the size of the files are relatively small.



### Coordinate Systems
If we want to describe a place on the Earth, we can use two different systems
- *Geographic Coordinate System*. Based on a spheroid and represented in angular units like degrees.

<p align="center">
<img align="center" src="https://www.ibm.com/docs/en/SSEPEK_11.0.0/spatl/src/art/0sbp5004.gif" alt='mapprogeographiccoordinatesystemjections' width="60%">
</p>

- *Projected coordinate system*. Based on a plane and utilize linear units like feets and meters.

    Map projections are a systematic rendering of locations from the curved Earth surface onto a flat map. Because some areas will be compressed and others will be streched, distortions are unavoidable   
    <p align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c1/Comparison_of_cartography_surface_development.svg/1920px-Comparison_of_cartography_surface_development.svg.png" alt='mapprojections' width="60%" >
    </p>
    
    Some common cylindrical projections
    <p align="center">
    <img src="https://cdn.britannica.com/55/109155-050-2886F564/transformation-Mercator-navigation-projection.jpg" alt='mercator' width="60%" >
    </p>

    The most commonly use is the Universal Transverse Mercator (UTM)
    <p align="center">
    <img src="https://www.oc.nps.edu/oc2902w/c_mtutor/images/utmdiagm.gif" alt='UTM1' width="38%" > &nbsp; &nbsp; &nbsp; &nbsp; <img src="https://2.bp.blogspot.com/-b_rq_J2SmlU/VgAUxnhBsBI/AAAAAAAAAQU/lvsPpgHDhCI/s1600/GMT_utm_zones.png" alt='UTM2' width="42%">
    </p>

## Spatial Statistics

- The objective of spatial statistics is to estimate a value at a certain point in space, as well as the uncertainty in this estimate.
- We aim to have better results than interpolation, whether this is linear, polynomial or spline.

### Nearest Neighbour

There are techniques related to the Nearest Neighbour algorithm that can be used in spatial statistics.

- Voronoi diagram. 

    Partition of a plane into regions close to each of a given set of objects. In the simplest case, these objects are just finitely many points in the plane (called seeds, sites, or generators). For each seed there is a corresponding region, called a Voronoi cell, consisting of all points of the plane closer to that seed than to any other. The line segments of the Voronoi diagram are all the points in the plane that are equidistant to the two nearest sites. The Voronoi vertices (nodes) are the points equidistant to three (or more) sites. Is worth noticing that the Voronoi diagrams can change in shape if we use different metrics.

    <p align="center">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/54/Euclidean_Voronoi_diagram.svg/330px-Euclidean_Voronoi_diagram.svg.png" alt='voronoi' width="60%" >
    </p>

    The Voronoi diagrams create Thiessen Polygons, these are the areas that define the nearest neighbour region of a known point.

### Inverse distance weighting
