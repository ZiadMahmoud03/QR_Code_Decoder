<!-- Much thanks to https://github.com/othneildrew/Best-README-Template for the template -->
<!-- And to https://github.com/alexandresanlim/Badges4-README.md-Profile for the badges -->
<img id="top" src="https://i.imgur.com/iW7JeHC.png" width="200" align="right" />




# QR Code Decoder


###### This project is for **CSE483 - Computer Vision** course in the Faculty of Engineering, Ain Shams University; for Spring 2022.

<details>
  <summary><b>Table of Contents</b></summary>
	<ol>
		<li><a href="#foreword">Foreword</a></li>
    <li><a href="#phase-one-details-and-requirements">Phase One Details and Requirements</a></li>
    <li><a href="#phase-two-details-and-requirements">Phase Two Details and Requirements</a></li>
		<li><a href="#getting-started">Getting Started</a></li>
		<li><a href="#usage">Usage</a></li>
		<li><a href="#contributing">Contributing</a></li>
		<li><a href="#acknowledgments">Acknowledgments</a></li>
	</ol>
</details>

## Foreword
A [QR code](https://en.wikipedia.org/wiki/QR_code) (quick-response code) is a type of two-dimensional matrix barcode, invented in 1994, by Japanese company Denso Wave for labelling automobile parts.[1][2] A QR code consists of black squares arranged in a square grid on a white background, including some fiducial markers, which can be read by an imaging device, such as a camera, and processed using Reed–Solomon error correction until the image can be appropriately interpreted. The required data are then extracted from patterns that are present in both the horizontal and the vertical components of the QR image.

The aim of this project is to create a generic preprocessing pipeline for 16 QR codes. After all the test cases pass through the pipeline they get decoded using Salma's algorithm. 

###### Built With

[![Python][python-shield]][python-url]
[![OpenCV][opencv-shield]][opencv-url]
[![Numpy][numpy-shield]][numpy-url]
[![Jupyter Notebooks][jupyter-shield]][jupyter-url]
[![Google Colab][colab-shield]][colab-url]
<!-- [![Pandas][pandas-shield]][pandas-url] -->

## Phase One Details and Requirements

![01-Getting-started](https://github.com/ZiadMahmoud03/QR_Code_Decoder/assets/91632042/17b6dc7a-e8df-4603-b9ff-a9f73517bb24)

During this phase we had 3 tasks:
<ol>
  <li>Preprocessing of the captured image</li>
  <li>QR code outer frame detection</li>
  <li>Straightening into a square</li>
</ol>

We'll give a brief example of how we tackled this phase with one of the test cases provided to us.

<h3>Task 1: Preprocessing of the QR Code</h3>
For the preprocessing, we were required to create a generic pipeline. How will this pipeline work? This pipeline will test for various conditions/issues to detect in the QR Code, if the condition is met then the QR Code will be modified depending on what the issue is. Let's say for example that we have a very small QR Code that is placed on a banana and, the QR Code is tilted. First, we'll convert the image to grayscale so we get rid of all the unnecessary banana yellow from the image, then we'll binarize the image and get the hough transform of the image. Getting the hough transform will help us locate the largest contour (the QR Code) in the image without having any other larger contours in the image ruinung the output. This brings us to the next task in this phase, QR Code outer frame detection.

<h3>Task 2: QR Code outer frame detection</h3>
Using the hough transform and getting the largest counter, we were able to detect the outer frame of the QR Code. We did that by finding all the square contours in the image. We managed to get the square contours by checking the aspect ratio of each contour, if the aspect ratio is close to 1 then the contour is a square, and then we checked if the width and height are similar, if they were than we got ourselves a square contour. After getting all the square contours we sorted them by size to get the largest square contour. Thanks to output we got from the hough transform we were able to detect the QR code as the largest contour, otherwise, the image frame would've been detected as the largest square contour. 

<h3>Task 3: Straightening into a square</h3>
Some test cases didn't need straightening into a square but for our very special and unique banana test case we needed to straighten it into a sqaure, how did we do this you might ask? Well, we used the same logic we did with the outerframe detection, but this time we were searching for 3 square contours instead of one. These 3 squaure contours are the locator boxes of the QR Code, and to our luck these locator boxes are the same size. We used the information we had and modified the code so that after getting all the square contours and sorting them from largest to smallest, we checked if 3 consecutive square contours had the same dimensions. But, that wasn't enough, when checking for the dimensions we had to add a ± 5 pixel tolerance in case there was something wrong with the image. After successfuly getting these loactor boxes we drew a right angle triangle connecting the 3 locator boxes and used it to check for tilt/issues with orientation. We already know how the correct orientation of a QR Code so we just applied a very simple algorithm to check the orientation of that triangle. After successfuly doing that, we now have a beautiful QR Code ready for decoding.

<p align="right">(<a href="#top">back to top</a>)</p>



## Phase Two Details and Requirements

During this phase we had one task which was decoding the QR Code we received from the preprocessing pipeline. This phase required a lot of research so that we can fully understand how QR Codes actually work. After intense research our team member Salma Nasreldin developed Salma's algorithm which helped us out a lot during this phase. All research papers we used will be added at the bottom of this readme. 


## Getting Started

### Prepare the environment

Before you start, you need to install the following libraries:

* NumPy
  ```sh
  pip install numpy
  ```
* OpenCV
  ```sh
  pip install opencv-python
  ```
* Matplotlib
  ```sh
  pip install matplotlib
  ```
* SciPy
  ```sh
  pip install scipy
  ``` 




<p align="right">(<a href="#top">back to top</a>)</p> 

## FlowChart

This flowchart is a visual representation of what each test case will go through inside our pipeline.

![image](https://github.com/ZiadMahmoud03/QR_Code_Decoder/assets/91632042/389397cb-6b33-41c6-a791-0bcd4cb250f4)


<p align="right">(<a href="#top">back to top</a>)</p>

## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.
If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#top">back to top</a>)</p>

## Acknowledgments
* **Course Instructor:** [Prof. Dr. Mahmoud Khalil](https://eng.asu.edu.eg/public/staff/mahmoud.khalil)
* **Course Teaching Assistant:** [Eng. Ahmed Salama](https://github.com/vadrif-draco)

<p align="right">(<a href="#top">back to top</a>)</p>


## References

https://www.kaggle.com/code/muhammadahmed26/image-processing-with-python
https://www.kaggle.com/code/viratkothari/computer-vision-image-processing-part-i
https://www.kaggle.com/code/viratkothari/computer-vision-image-processing-part-ii
https://www.kaggle.com/code/shresthapriya/computer-vision-and-image-processing-tutorial-1
https://www.kaggle.com/code/shresthapriya/introduction-to-image-processing-edge-detection
https://ahmedibrahimcv.blogspot.com/
https://ahmedibrahimcv.blogspot.com/2022/12/computer-vision-image-histograms-and.html
https://docs.opencv.org/4.x/d2/df0/tutorial_js_table_of_contents_imgproc.html
https://www.youtube.com/watch?v=KA8hDldvfv0&list=PLnkRJhIMg_vD2FWQkLTB2crPKdGFUhYBA&index=4
https://www.qrcode.com/en/about/


<p align="right">(<a href="#top">back to top</a>)</p>

[contributors-shield]: https://img.shields.io/github/contributors/vadrif-draco/asufecse483project-simpleperceptionstack.svg?style=for-the-badge
[contributors-url]: https://github.com/ZiadMahmoud03/QR_Code_Decoder/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/vadrif-draco/asufecse483project-simpleperceptionstack.svg?style=for-the-badge
[forks-url]: https://github.com/ZiadMahmoud03/QR_Code_Decoder/forks
[stars-shield]: https://img.shields.io/github/stars/vadrif-draco/asufecse483project-simpleperceptionstack.svg?style=for-the-badge
[stars-url]: https://github.com/ZiadMahmoud03/QR_Code_Decoder/stargazers
[issues-shield]: https://img.shields.io/github/issues/vadrif-draco/asufecse483project-simpleperceptionstack.svg?style=for-the-badge
[issues-url]: https://github.com/ZiadMahmoud03/QR_Code_Decoder/issues

[python-shield]: https://img.shields.io/badge/Python-FFD43B?style=for-the-badge&logo=python&logoColor=blue
[python-url]: https://www.python.org/
[opencv-shield]: https://img.shields.io/badge/OpenCV-27338e?style=for-the-badge&logo=OpenCV&logoColor=white
[opencv-url]: https://opencv.org/
[numpy-shield]: https://img.shields.io/badge/Numpy-777BB4?style=for-the-badge&logo=numpy&logoColor=white
[numpy-url]: https://numpy.org/
[pandas-shield]: https://img.shields.io/badge/Pandas-2C2D72?style=for-the-badge&logo=pandas&logoColor=white
[pandas-url]: https://pandas.pydata.org/
[jupyter-shield]:	https://img.shields.io/badge/Jupyter-e46e32.svg?&style=for-the-badge&logo=Jupyter&logoColor=white
[jupyter-url]: https://jupyter.org/
[colab-shield]: https://img.shields.io/badge/Colab-F9AB00?style=for-the-badge&logo=googlecolab&color=525252
[colab-url]: https://colab.research.google.com/

[before-vision]: assets/test_images/test5.jpg
