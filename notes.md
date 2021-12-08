# Earth and Environmental Sciences

Index

* [Spatial Data Model](#spatial-data-model)
* [Spatial Statistics](#spatial-statistics)
* [Linear Inverse Theory](#linear-inverse-theory)
* [Tomography](#tomography)

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
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/54/Euclidean_Voronoi_diagram.svg/330px-Euclidean_Voronoi_diagram.svg.png" alt='voronoi' width="40%" >
    </p>

    The Voronoi diagrams create Thiessen Polygons, these are the areas that define the nearest neighbour region of a known point.

### Inverse distance weighting

The IDW technique computes an average value for unsampled locations using values from nearby weighted locations. The weights are proportional to the proximity of the sampled points to the unsampled location and can be specified by the IDW power coefficient. The larger the power coefficient, the stronger the weight of nearby points as can be gleaned from the following equation that estimates the value $Z$ at an unsampled location $j$

$$\hat{z}_j=\frac{\sum_i \frac{Z_i}{d_{ij}^n}}{\sum_i\frac{1}{d_{ij}^n}}$$

The parameter $n$ is the weight parameter that is applied as an exponent to the distance thus amplifying the irrelevance of a point at location $i$ as distance to $j$ increases. So a large $n$ results in nearby points wielding a much greater influence on the unsampled location than a point further away resulting in an interpolated output looking like a Thiessen interpolation. On the other hand, a very small value of $n$ will give all points within the search radius equal weight such that all unsampled locations will represent nothing more than the mean values of all sampled points within the search radius.

### Spatial autocorrelation

Measures of spatial autocorrelation describe the degree two which observations (values) at spatial locations (whether they are points, areas, or raster cells), are similar to each other. So we need two things: observations and locations.

Spatial autocorrelation in a variable can be exogenous (it is caused by another spatially autocorrelated variable, e.g. rainfall) or endogenous (it is caused by the process at play, e.g. the spread of a disease).

A commonly used statistic that describes spatial autocorrelation is Moran’s I. Other indices include Geary’s C and, for binary data, the join-count index. The semi-variogram also expresses the amount of spatial autocorrelation in a data set.

The Moran’s I statistic is the correlation coefficient for the relationship between a variable and its surrounding values.

A **variogram** allows us to see the correlation over the distance.

### Kriging 

It is an advanced geostatic procedure to produce a estimated surface based on $X$, $Y$ data which has a corresponding $Z$ value.

Kriging involves the use of IDW (inverse distance weighted) and the spline method, these are deemed to be deterministic as they are based on surrounding actual data.

[Link to an explanation of Kriging method](https://www.azavea.com/blog/2016/09/12/kriging-spatial-interpolation-desktop-gis/)

### Summary

- Simple interpolation works well for many things were there known controls
- I find most contouring techniques are as good as each other
- Moran test is insensitive
- Never had to use kriging but I like and use variograms

## Time series

- A time series is a series of data points indexed in time order.
- Most commonly, a time series is a sequence taken at  successive equally spaced points in time.
- It is a sequence of discrete-time data.
- The aim of the process is to produce best-fit model with residual error as white noise.
- White noise is a normal distribution with mean zero and the smallest as possible.
- It has several components

    $$y(t)=\text{trend}+\text{season}+AR+MA+e$$

    where 
    * Trend is the secular variation (changes in the Earth's magnetic field on time scales of about a year or more)
    * Season is the year season.
    * AR is autoregressive
    * MA is the moving average
    * e is the residual error

- The trend can be linear, quadratic, cubic, exponential, etc.
- The seasonal component can be obtained in a number of ways, using a fixed cycle for a year, a monthly median, or a Fourier transform
    $$A\cos\left(\frac{\pi m}{6}\right)+B\sin\left(\frac{\pi m}{6}\right)$$

- *Autocorrelation Function (ACF)*. Gives us values of auto-correlation of any series with its lagged values. We plot these values along with the confidence band and have an ACF plot. In simple terms, it describes how well the present value of the series is related with its past values. A time series can have components like trend, seasonality, cyclic and residual. ACF considers all these components while finding correlation. This suggests the **moving average component**.

- *Partial Autocorrelation Function (PACF)*. Instead of finding correlations of present with lags like ACF, it finds correlation of the residuals (which remains after removing the effects which are already explained by the earlier lag(s)) with the next lag value hence "partial" and not "complete" as we remove already found variations before we find the next correlation. So if there is any hidden information in the residual which can be modeled by the next lag, we might get a good correlation and we will keep that next lag as a feature while modeling. Remember while modeling we don’t want to keep too many features which are correlated as that can create multicollinearity issues. Hence we need to retain only the relevant features. This suggests the **autoregressive component**.

### ARIMA

Autoregressive integrated moving average model:

$$ARIMA=(p,q,d)$$

- The **Moving Average** process is difficult to get a physical interpretation.
- Differencing makes the time series stationary
    * Removes trend and seasonality
- Can be fractitional (ARFIMA)
- Can be seasonal (SARIMA)

#### Definition:

Given time series data $X_t$ where $t$ is an integer index and the $X_t$ are real number, the ARMA(p,q) model is given by

$$X_t-\alpha_1X_{t-1}-\dots-\alpha_p X_{t-p}=\epsilon_t+\theta_1\epsilon_{t-1}+\dots+\theta_q\epsilon_{t-q}$$

or equivalently by

$$\left(1-\sum_{i=1}^{p}\alpha_i L^i\right)X_t=\left(1+\sum_{i=1}^q\theta_i L^i\right)\epsilon_t$$

where $L$ is the lag operator, the $\alpha_i$ are the parameters of the autoregressive part of the model, the $\theta_i$ are the parameters of the moving average part and the $\epsilon_t$ are error terms.

An ARIMA(p,d,q) process can be thought as a particar case of an ARMA(p+d,q) process having the autoregresive polynomial with $d$ unit roots.

Examples:

- ARIMA(0,1,0) is simply a random walk.

    $$X_t=X_{t-1}+\epsilon_t$$

- ARIMA(0,0,0) is a white noise model
- ARIMA(0,2,2) model is given by

    $$X_t=2X_{t-1}-X_{t-2}+\left(\alpha+\beta-2\right)\epsilon_{t-1}+\left(1-\alpha\right)\epsilon_{t-2}+\epsilon_t$$

## Linear Inverse Theory

In most branches of physics or science in general, we can design experiments that directly address the questions we want to ask.

In geophysics, there are several issues that make experimentation difficult:

- We are given a fixed experimental setup.
- Many interacting, poorly-understood processes.
- Observations almost entirely at or above Earth's surface.
- Two thirds of Earth's surface covered by water.
- We have $~10^2$ years of records for a system that constant processes operating on timescales up to $~10^9$ years.
- Cannot control when or where transient phenomena (e.g. earthquakes) occur.

#### Noise

Everything in the data that we can't explain. Signals caused by physical processes that we have chosen to ignore, like human or animal activity, or observational uncertainties and fluctuations like temperature, atmospheric pressure, poorly-installed instruments, etc.

What we usually do is model it as a Gaussian random process 

$$d = d_{true} + n$$   
$$n\sim \mathcal{N}(0,\sigma)$$

We can do this because of the central limit theorem, which says that the sum of samples from many random distributions is normally-distributed even if the source distributions aren't.

$$G(x,\mu,\Sigma)=\frac{1}{\sqrt{(2\pi)^N\det\Sigma}}\exp\left[-(x-\mu)^{T}\Sigma^{-1}(x-\mu)\right]$$

#### Representation of the system

An idealised, simplified mathematical description of the thing(s) we're interested in

A representation is a set of assumptions and unknowns. In the case of the Hook's Law, some assumptions we could make is that we don't have dissipation and that Hooke's law holds exactly, and the unknowns would be the mass and the spring constant $k$. In the case of the Earth structure, we may assume that there is a simple attenuation law that describes how energy decays over time, and that as the waves travel through the Earth, everything behaves the same (No anisotropy). The unknowns would be the shear wavespeed, the compressional wavespeed or the density at every point in space.

To represent "every point in space" we can describe a continuous function by introducing a set of basis functions:

$$f(\vec{x})=\sum_{i=1}^N f_i\psi_i(\vec{x})$$

The function is then specified by a vector of coefficients:

$$\vec{f}=(f_1,f_2,\dots,f_N)^T$$

When dealing with the Earth, we may use Spherical Harmonics or grid cells.

The set of basis functions:

- Control the characteristics of the solution (Sharp edges, smooth gradients, discontinuities).
- Control the resolution of the solution (smallest object that can be represented, some structures easier to represent than others).

This implies that the assumptions for the study of Earth are a choice of basis, an the unknown is a set of coeficients.

### Forward theory

- A function $g(\vec{m})$ that describes the observations we would expect to obtain if the system looked like $\vec{m}$.
- Often computationally-expensive, involving numerical solution of differential equations.
- The simulated observations are often referred to as 'synthetic data'.
- Method for solving forward problem often influences/determines the choice of model parameterisation.
- A forward model is said to be linear if 

    $$\vec{g}(\alpha \vec{m}_1+\beta\vec{m}_2)=\alpha \vec{g}(\vec{m}_1)+\beta\vec{g}(\vec{m}_2)$$
- Linear functions can be written using linear algebra.

    $$\vec{g}(\vec{m})=G\vec{m}$$

- Non linear functions can be linearised for small enough perturbations $\delta\vec{m}$

    $$\vec{g}(\vec{m}+\delta\vec{m})\approx \vec{g}(\vec{m})+\sum_i\frac{\partial\vec{g}(m)}{\partial m_i}\delta m_i\approx \vec{g}(\vec{m})+G\ \delta m$$

- We need to have a way of comparing between actual and prediction. A common choice is the squared $L_2$ norm or Euclidiean distance

    $$\phi=||\vec{d}-\vec{g}(\vec{m})||^2_2$$

    where

    $$||\vec{x}||_2=\sqrt{\sum_i x_i^2}=\sqrt{\vec{x}^T\vec{x}}$$

    We often report normalized 'misfit': 

    $$\phi=\frac{||\vec{d}-\vec{g}(\vec{m})||}{||\vec{d}||^2_2}$$

- Some of the questions we may ask are:
    * How well does this model explain the data?
    * What are the uncertainties on my model and how does this affect my interpretation? Propagated noise, systematic errors in observational process, theoretically-incomplete forward model.
    * Are there other models that could fit the data? Would my interpretation change?

- Null space is a big problem. If we have a linear operator $G$, the null space is defined to be the set of all vectors $\vec{v}$ such that

$$G\vec{v}=\vec{0}$$

and hence

$$G\vec{m}=\vec{d}\Rightarrow G(\vec{m}+\vec{v})=\vec{d}$$

## Tomography


