# step size detection using machine learning

In this notebook, I am going to use machine learning to detect spots in high reolution flourescent microscopy. The tiff image files used belong to motor protein dynein.

- Detection of the flouresenctly labeled motor proteins under the microscope is tricky and it requires precise spot tracking. The image is usually very noisy due to the inaccuracies arising from quantifying the number of detected photons in each pixels and follows a gaussian distribution around a flourescently labeled proteins (GFP in this notebook). Here I train a regressian algorithm to detect spot centers and obtain the overall trajectory of the protein.

- Analysis of the step size (motor proteins have two "legs" and take steps with a varying step size distribution especially for dynein), is an important characteristics in understanding how a motor protein works. Dwell time; time passing between two consecutive steps is nother important feature of these proteins. I hand-fit a trace by investigating where the steps occur initially and use a Logistic Regression algorithm to detect the steps automatically.

- I use feature creation to generate new features from the trajectory (position versus time(frame)) data. The features I created for my ML algorithm depend on the positional difference between the current position or preciding or next positions in the movie, and they are as follows:

pos: the position of the protein (y coordinate).<br>
slope: difference between the current position and the previous position.
second_slope: difference between the current position and position two frames ago.
third_slope: difference between the current position and position three frames ago.
fourth_slope: difference between the current position and position four frames ago.
forward_slope: difference between the current position and the next position.
tanhx: tanh of the difference between the previous position and the next position.
tanhx2: tanh of the difference between the two previous position and the second next position.
sinx: sinx of the difference between the previous position and the next position.

Other types of features are also necessary for the detection of the backward steps, this notebook only covers the detection in the forward direction. Dynein's stepping pattern is highly irregular compared to for instance kinesin, but majority of the steps are still in the forward direction; as it needs to move towards the minus-end of the Microtubules (molecular tracks) to perform its celular functions.
