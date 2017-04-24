---
layout: slide
title: "Image preprocessing"
author: Cristian Perez
date:   2017-02-28 21:01:25 +0200
description: A presentation slide for how to use reveal.js in Jekyll
theme: black
transition: slide
---

<section data-markdown>
# Image preprocessing

Cristian Perez

28 février 2017

</section>

<section data-markdown>

## Anatomy of an image classifier

![](/images/image-preprocessing/image-classification-pipeline.jpg)

Note:

- Many traditional computer vision image classification algorithms follow this pipeline
- Deep Learning based algorithms bypass the feature extraction step completely

</section>

<section data-markdown>
# Preprocessing 

## Deskew

Align an image to a reference assits the classification algorithm 
[1](http://docs.opencv.org/trunk/dd/d3b/tutorial_py_svm_opencv.html),
[2](https://www.learnopencv.com/handwritten-digits-classification-an-opencv-c-python-tutorial/).

![](/images/image-preprocessing/deskew1.jpg)

Note:

Il est possible d'aider l'algorithme d'apprentissage. Pour le cas de
reconnaissance de visage par exemple, aligner les images par rapport par
rapport à la position des yeux améliore les résultats.

Pour le cas de digits, aligner les numéros améliore les résultats.
L'inclination de l'écriture peut être corrigé.  Ainsi l'algorithme ne doit pas
apprendre cette variation entre les chiffres.
</section>

<section data-markdown>
Deskewing simple grayscale images can be achieved using image moments (distance and intensity of pixels). 

```python
def deskew(img):
    m = cv2.moments(img)
    if abs(m['mu02']) < 1e-2:
        # no deskewing needed. 
        return img.copy()
    # Calculate skew based on central momemts. 
    skew = m['mu11']/m['mu02']
    # Calculate affine transform to correct skewness. 
    M = np.float32([[1, skew, -0.5*SZ*skew], [0, 1, 0]])
    # Apply affine transform
    img = cv2.warpAffine(img, M, (SZ, SZ), flags=cv2.WARP_INVERSE_MAP | cv2.INTER_LINEAR)
    return img
```

Note: 

This deskewing of simple grayscale images can be achieved using image moments.
OpenCV has an implementation of moments and it comes in handy while calculating
useful information like centroid, area, skewness of simple images with black
backgrounds.

It turns out that a measure of the skewness is the given by the ratio of the
two central moments ( mu11 / mu02 ). The skewness thus calculated can be used
in calculating an affine transform that deskews the image.
</section>


<section data-markdown data-vertical="^\n--\n$">

Or

^\n--\n$


--

Even

--
 <!--v-->

Vertical

---

Slides

</section>

<section data-markdown data-separator="^\n---\n$" data-vertical="^\n--\n$" data-notes="^Note:">
<script type="text/template">
## Vertical Slides

Or

--

Even

--

Vertical

--

Slides

</script>
</section>