# Surface vessel diameter calculated using the full-width at half-max
This repository provides sample data and code that demonstrates how to calculate fluctuations in vessel diameter from the .TIF stacks acquired during two-photon excitation microscopy.

# Instructions
- Analysis code (*DiamCalcSurfaceVesselExample.m*) is available for download at https://github.com/KL-Turner/Surface-Vessel-FWHM-Diameter/blob/master/DiamCalcSurfaceVesselExample.m
- Sample data (*190426_008.TIF*) is available for download at https://drive.google.com/drive/folders/1YKzuRAuJtlcBx3zLxZods0PeUsiUrTlm?usp=sharing

Analysis code is self-contained, with all necessary functions nested in the script. The user places an ROI along a short segment of the vessel along which the diameter is measured. The edges of the ROI parallel to the midline of the vessel need to be far enough away from the vessel such that when the vessel dilates, the vessel does not completely fill the ROI. No other fluorescent objects other than the vessel segment to be measured should be in this ROI.

After this, the user positions a line parallel to the long axis of the vessel. The image stack is motion corrected (Manuel Guizar-Sicairos, Samuel T. Thurman, and James R. Fienup,  "Efficient subpixel image registration algorithms", *Opt. Lett. 33*,156-158 (2008)). This motion correction can remove small x-y axis motion, but cannot deal with z (out of plane) motion.

| Region of interest (ROI) box and parallel line segment | 5X speed movie output |
|:----:|:---:|
| ![](https://user-images.githubusercontent.com/30758521/57501563-07ae7980-72b6-11e9-925d-1d50cb4893f1.png) | ![](https://user-images.githubusercontent.com/30758521/57501494-be5e2a00-72b5-11e9-93ce-2ca7ee5481b0.png) |

A single Radon tranform along the angle of the vessel's long axis is performed for each motion-corrected frame. This is equvalent to rotating the the ROI such that the long axis of the vessel is vertical, and then averaging the intensity of the pixels along each of the columns.  The result of this operation is a vector for each frame that is the average intensity distribution along an axis perpendicular to the vessel's long axis. A full-width at half-maximum (FWHM) for this intensity distribution is calculated for each frame of the image stack, resulting in a vector of diameter measurements.

Using a short segment of vessel to calculate the diameter produces less noisy diameter measures than ones using only a single line scan. However, the segment selected should be of constant diameter and fluorescence intesity, otherwise the FWHM will give erroneous output.

When the script completes, it will output a movie of the .TIF stack (sped up 5X) and a figure of the resulting diameter caluclation obtained from the inputed ROI and parallel line segment.

| FWHM results from sample data and shown ROI |
|:---:|
| ![](https://user-images.githubusercontent.com/30758521/57501885-3f69f100-72b7-11e9-997b-56fe1cc816d8.png)


# Example of code prompts/inputs (Command Window)

**The sampled data is an artery and the objective used was the Nikon CFI75 LWD 16X, [2]**

*Select a single .tif stack from the current directory*
 
*Loading: 190426_008.TIF...*
 
*Which objective was used during this stack? Objective IDs:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*[1] Olympus UMPlanFL N 10X*  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*[2] Nikon CFI75 LWD 16X*  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*[3] Olympus UMPlanFL N 20X (0.50 NA)*  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*[4] Olympus UMPlanFL N 20X (1.00 NA)*  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*[5] Olympus UMPlanFL N 40X*  
*Enter objective ID number [1 2 3 4 5]:* **2**
 
*Is the vessel an artery (A), vein (V), or dural (D) vessel?:* **A**
 
*Is the diameter of the box ok? (y/n):* **y**
 
*Is the line along the diameter axis ok? (y/n):* **y**
 
*Analyzing vessel projections from defined polygons...*
 
*Generating movie (sped-up 5X)...*
 
*Diameter calculation for surface vessel example  - complete.*

If you utilize aspects of this code, please cite: **Huo BX, Gao YR, Drew PJ, (2015) Quantitative separation of arterial and venous cerebral blood volume increases during voluntary locomotion, NeuroImage, 105:369–379, doi: 10.1016/j.neuroimage.2014.10.030**

# Acknowledgements
- Written by Kevin L. Turner and Patrick J. Drew
- Previous code contributions by Yurong Gao and Christina Echagarruga

https://sites.esm.psu.edu/~pjd17/Drew_Lab/Drew_Lab.html
