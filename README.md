# IntrusionDetection
### Collaborators
* Zorila Iulian
* Marini Daniele
* Tanzi Giuseppe

The objective of the project is to succesfully detect the intruder within the scene using just python and opencv library.

## Data
<img src="https://github.com/iulianzorila/IntrusionDetection/blob/main/Intruder.jpeg" width="320" height="240"></img>

The video which we have worked on has the following characteristics:
* 12  frame/s  (total  duration is about 41 secs)
* 320x240  pixels
* 8 bit/pixel (256 gray levels)
* The sequence is compressed by the Radius Cinepak CODEC.

Moreover, it is worth pointing out that the scene is static and this is precisely the condition which allows to extract the background via interpolation.

### Description
Essentially in the video, there is just a single person, moving around the room and towards the end, takes an object (a book) and replaces with another.


## Instruments
To accomplish the detection of the intruder different techniques have been employed:
* Background extraction through interpolation (mean or median)
  * The **median** turns out to be more effective for this particular video, as the person is constantly moving, therefore pixel intensities, across the frames, which have high variance won't be picked as eligible values.
* Frame difference with extracted background, trying three distances:
  * [Manhattan distance](https://en.wikipedia.org/wiki/Taxicab_geometry).
  * [Euclidean distance](https://en.wikipedia.org/wiki/Euclidean_distance).
  * [Maximum distance](https://en.wikipedia.org/wiki/Chebyshev_distance).
* Morphology operators to improve the **mask** quality (binary image obtained from difference between frame and background):
  * [Opening](https://docs.opencv.org/4.x/d9/d61/tutorial_py_morphological_ops.html), to get rid of noise, consisting of smaller blobs.
  * [Closing](https://docs.opencv.org/4.x/d9/d61/tutorial_py_morphological_ops.html), to fill holes in the detected intruder.
* Contour extraction:
  * [Find and draw contours](https://docs.opencv.org/3.4/d4/d73/tutorial_py_contours_begin.html)
* Features extraction:
  * [Area](https://docs.opencv.org/4.x/dd/d49/tutorial_py_contour_features.html).
  * [Perimeter](https://docs.opencv.org/4.x/dd/d49/tutorial_py_contour_features.html)
  
## Results
For each frame we plotted three different images to observe the difference and how the final result was influenced by morphology operators:

<table>
 <tbody>
  <tr>
   <td style="border:0">Contours</td>
   <td>Mask</td>
   <td>Mask after morphology operators</td>
  </tr>
  <tr>
   <td style="padding:0"><img src="https://github.com/iulianzorila/IntrusionDetection/blob/main/res.gif" width="320" height="240"></td>
   <td style="padding:0"><img src="https://github.com/iulianzorila/IntrusionDetection/blob/main/mask.gif" width="320" height="240"></td>
   <td style="padding:0"><img src="https://github.com/iulianzorila/IntrusionDetection/blob/main/fmask.gif" width="320" height="240"></td>
  </tr>
 </tbody>
</table>

Finally, a .txt [file](https://github.com/iulianzorila/IntrusionDetection/blob/main/data/results.txt) is generated, including identified objects information:
* Frame number.
* Number of identified objects.
* Identifier, area, perimeter and label of identified object.
<img src="https://github.com/iulianzorila/IntrusionDetection/blob/main/Txt-result.png" height="300">
Labeling process was performed by the means of a area thresholding.
