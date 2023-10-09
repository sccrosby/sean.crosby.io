---
title:       "Ocean wave transformation with ray-path tracing"
subtitle:    "Given ocean bathymetry we can calculate wave speed and then rapidly estimate ocean wave transformation"
description: ""
date:        2021-10-17
author:      "Sean C. Crosby"
image:       ""
tags:        ["Oceanography", "Repositories"]
categories:  []
draft:       false
---

<script type="text/javascript"
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

### Ray tracing

Ray-tracing is a common tool in many fields from Magnetic resonance imaging (MRI) to ocean acoustics. In fact ocean acoustics are frequently employed to study whale and porpoise populations as well as detect boats or submarines. The concept is relatively simple, a wave traveling through a medium will bend or refract as its speed in the medium changes. And this is true for ocean waves, the ones you commonly see arriving at the shoreline. Just as light "bends" as it travels through glass or water, these waves bend as their speed is influences by the water depth and the wave frequency or period. In shallow water wave speed is influenced primarily by the depth, such that

$$ c = \sqrt{gH} $$

where the speed, c, is a function of depth, H, scaled by the gravitational constant, g (9.81 m/s). In deeper and intermediate waters, the wave frequency plays an important role (lower frequency waves tend to travel faster) and the relation becomes a little more complicated as is known in the literature as the dispersion relation. I will refer the reader to the [wiki](https://en.wikipedia.org/wiki/Dispersion_(water_waves)) for further detail. However, the concept is the same, if you can estimate the wave speed of the medium, you can determine the trajectory of the wave.

### Wave transformation

Since the early 1960s this concept was applied to ocean waves to predict wave energy transformation at the shoreline. In the absence of significant wind-wave generation, or other non-linear wave-wave interactions, ray-tracing provides a relatively simple, and rapid approach to predicting wave transformation in the nearshore. This approach was central to my PhD research were the relatively simple transformation estimates were used to invert for offshore wave conditions. This was developed in sourthern California where complex bathymetry leads to interesting wave propagation and patterns of wave focusing and sheltering. A paper I wrote several years ago shows that predictions from rays are similar to typically employed numerical wave models and in some cases may be more accurate ([paper](https://journals.ametsoc.org/view/journals/atot/36/2/jtech-d-18-0123.1.xml))

In effort to make the approach more accessible I have started a repository for my ray tracing code, https://github.com/sccrosby/RayTracer. The approach traces wave trajectories backwards, from the shore to deep water. It is this backwards approach that turns out to be far more intuitive, providing the offshore directions and locations where waves will come from. The illustration below shows how some incoming wave directions are simply blocked (red) while others are open (green) to wave energy incoming from the Pacific Ocean. The code utilizes a 4th order runga-kutta scheme to integrate along the ray-path. The tracing is performed in spherical coordinates assuming the earth to be an ellipsoid. While the scripts and functions are in Matlab, I am considering converting to python as there is a need to improve speed by moving some components to fortran or other compiled language. However, the inefficiencies only become significant when examine many hundreds of thousands of locations and wave frequencies. 


![Example image](/img/ray_tracing.gif)
