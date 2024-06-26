# PixelFlow: Innovative Flow Simulation from Image Data

<div style="display: flex; flex-direction: row;">
    <img src="figures/original.png" alt="Image 1" style="width: 200px; height: 200px;">
    <img src="figures/porosity.png" alt="Image 1" style="width: 200px; height: 200px;">
    <img src="figures/velocityInFluid.png" alt="Image 2" style="width: 200px; height: 200px;">
</div>

## Overview

This code introduces a novel approach to flow simulation using the new governing equations [1]. By processing pixel data such as images and 2D illustrations, it allows for straightforward execution of flow simulations around objects. 

**Disclaimer: This code is provided for use in Google Colaboratory. The author assumes no responsibility for any damages arising from the use of this code.**

This program is provided "as-is" without any warranty. The author does not guarantee the accuracy, completeness, or suitability of the code and disclaims any liability for any damages or issues resulting from its use.

By using this code, you agree that the author shall not be liable for any direct, indirect, incidental, consequential, or any other damages or losses arising from the use of this code. You use this code at your own risk.

The user is solely responsible for understanding and managing the risks associated with the use of this code. This disclaimer is subject to change without notice.

### Grayscale

Grayscaling can be easily achieved by loading the previously resized image using OpenCV's `IMREAD_GRAYSCALE` function. Here, we explain the process that takes place within the image during the grayscaling process.

Each pixel in the image has a specific RGB (Red, Green, Blue) value, where each color has 256 steps ranging from 0 to 255 (i.e., $2^8$ or $16^2$). By performing the following operations on these RGB values, a grayscale image can be generated. This method follows the "Luminosity Method (ITU-R BT.601)."

$$ \rm{Gray} = Red \times 0.229 + Green \times 0.587 + Blue \times 0.114 $$

The following code block (the greyscale tester) conducts a test to convert an original BGR color (specified by user input) to grayscale by applying custom weights to each channel (B, G, R). Users can set these custom weights through sliders. The resulting grayscale intensity is calculated based on the specified weights, and the original and grayscale images are displayed side by side for visual comparison.

## Outline detection

<div style="display: flex; flex-direction: row;">
    <img src="figures/gray.png" alt="Image 1" style="width: 200px; height: 200px;">
    <img src="figures/outline.png" alt="Image 1" style="width: 200px; height: 200px;">
    <img src="figures/com.png" alt="Image 2" style="width: 200px; height: 200px;">
</div>

Grayscale conversion of the original image enables contour detection through kernel operations. By combining the extracted contours with the original grayscale image, a contour-enhanced image is obtained.

## SDF

<div style="display: flex; flex-direction: row;">
    <img src="figures/phi.png" alt="Image 1" style="width: 200px; height: 160px;">
    <img src="figures/sd.png" alt="Image 1" style="width: 200px; height: 160px;">
    <img src="figures/porosity_image.png" alt="Image 2" style="width: 200px; height: 160px;">
</div>

First, perform binarization to make the interface clear. Then, calculate the Signed Distance Field (SDF) using the Fast Marching Method (FMM), and obtain the porosity distribution by applying the sigmoid function.

## Resize

Resizing is done by the function `resize` of the OpenCV module. This function can scale an image by giving a scale factor. For example, a scale factor of 0.5 on a 100x100 image results in a 50x50 image.

Therefore, in order to convert an image to an arbitrary resolution, it is sufficient to know this scale factor. Let $\rm{(W, H)}$ denote the number of pixels in the original image and $\rm{(W', H')}$ the number of pixels in the converted image. Resolution is the total number of pixels, so if the original resolution is $\rm{R}$, the following equation holds.

$$\rm{R} = WH$$

Here, the number of pixels in the height and width of the converted image $\rm{(W', H')}$ is defined using the scale factor $s( > 0)$ and $\rm{(W, H)}$ as follows.

$$\rm{(W', H')} = (\textit{s}\rm{W}, \textit{s}\rm{H})$$

This allows the transformed resolution $\rm{R'}$ to be expressed as follows.

$$\rm{R'} = W'H' = s^2\rm{WH} $$

Solving this for $s$, we obtain.

$$s = \sqrt{\frac{R'}{WH}} $$

Therefore, given an arbitrary resolution, the coefficient $s$ can be obtained and resizing can be performed. Run the code block below and set the resolution by changing the slider bar of `resolution`. The last value you set will be the resolution used in the following program. The images are stored in the `tmp` folder.

## Links

Solver: [PixelFlow](https://github.com/nobu-n2002/PixelFlow)

## References

[1] Oshima, N., A Novel approach for wall-boundary immersed flow simulation: proposal of modified Navier-Stokes equation, Journal of Fluid Science and Technology. Vol.18, No.4 (2023), 
https://doi.org/10.1299/jfst.2023jfst0034

[2] Oshima, N., A Novel approach for wall-boundary immersed flow simulation (part 2: modeling of wall shear stress), Journal of Fluid Science and Technology. Vol.19, No.3 (2024), https://doi.org/10.1299/jfst.2024jfst0026

[3] Oshima, N., Program for flow simulation immersing wall boundary, Hokkaido university collection of scholarly and academic papers, http://hdl.handle.net/2115/89344
