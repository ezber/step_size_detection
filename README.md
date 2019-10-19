# step size detection using machine learning

In this notebook, I am going to use machine learning to detect spots in images obtained via high resolution flourescent microscopy. The tiff image files used here belong to motor protein dynein.

- Detection of the flourescently labeled motor proteins under the microscope is tricky and it requires precise spot tracking. The image is usually very noisy due to the inaccuracies arising from quantifying the number of detected photons in each pixel and follows a gaussian distribution around the flourescently labeled proteins (GFP in this notebook). Here I train a regression algorithm to detect spot centers and obtain the overall trajectory of the protein.

- Analysis of the step size (motor proteins have two "legs" and take steps with a varying step size distribution especially for dynein), is an important characteristics in understanding how a motor protein works. Dwell time; time passing between two consecutive steps is another important feature of these proteins. I hand-fit a trace by investigating where the steps occur initially and use a Logistic Regression algorithm to detect the steps automatically.

- I use feature creation to generate new features from the trajectory (position versus time(frame)) data. The features I created for my ML algorithm depend on the positional difference between the current position or preciding or next positions in the movie, and they are as follows:

pos: the position of the protein (y coordinate).<br>
slope: difference between the current position and the previous position.<br>
second_slope: difference between the current position and position two frames ago.<br>
third_slope: difference between the current position and position three frames ago.<br>
fourth_slope: difference between the current position and position four frames ago.<br>
forward_slope: difference between the current position and the next position.<br>
tanhx: tanh of the difference between the previous position and the next position.<br>
tanhx2: tanh of the difference between the two previous position and the second next position.<br>
sinx: sinx of the difference between the previous position and the next position.<br>
<br>
Other types of features are also necessary for the detection of the backward steps, this notebook only covers the detection in the forward direction. Dynein's stepping pattern is highly irregular compared to for instance kinesin, but majority of the steps are still in the forward direction; as it needs to move towards the minus-end of the Microtubules (molecular tracks) to perform its celular functions.
<br><br>
This repository consists of following files that make up the whole project:<br>
single_spot_detection.ipynb : uses wavelet forms to clean the noise and detect single spots.<br>
linear_regression_for_spot_detection.ipynb : feeds the spot locations (target) and pixel intensities (features) to train a Linear Regression Model for spot detection.<br>
trajectory_extraction_and_step_detection.ipynb : extracts the overall trajectory using the 2nd notebook and demostrates how step detection is performed to generate data for the next notebook.<br>
feature_creation_and_logistic_regression.ipynb : creates new features from the overall trajectory for step detection and uses logistic regression on a new trace to extract features belonging to motor protein.
