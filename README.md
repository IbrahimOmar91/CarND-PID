# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---
In this project we need to set the p, i and d Terma of the PID controller to control the steering angle
To solve this problem i decided to adjust the parmeters manually
Starting with the D only, i tried setting it to:
### P:
*  ` 1` >> the car just "rotated" around till it got out of the road
* `-1` >> the car started to move and moved a little but when the road started ot curve the responce was way to much so it stuck again
so it looks like the "kp" should br negative and > -1
* `-0.5` >> again the car stuck after some distance, but moved longer this time
* `-0.2` >> the same as -0.5 but a little longer
* -0.1 >> KO!, still having the same behavior .. the car can't make it if the road curves alot, so still need to lower the value
* `-0.05` >> Things are getting better this time, the car moved through some curves well then eventually it came to stop, we still not there yet
* `-0.02` >> WOW!, this time the change of the steering was too slow to handle the curves to the car got out of the road, try a little bit higher value this time
* `-0.03` >> things went better this time, the car went longer distance but still can't handle large curvetures
* `-0.04` >> again the car got stuck, its time to add some "ki"
### P and I:
* `-0.04,1` >> 1 seems to be a very large value, again i will try small negative values
* `-0.04,-0.05` >> it was very bad but still in the right direction, i think it should be lower still
* `-0.04,-0.005` >> this is even worse may be wee need to lower the p term
* `-0.04,-0.001` >> again seems the same may be adding the d term will help !
### P, I and D:
* `-0.04, -0.001, -1` >> Awesome !! it is way better than ever, tha car can now finish the track more than once, but still gets on the yellow lines sometimes, so still need some modifications, i will try larger p value to make the steering angle larger
* `-0.05, -0.001, -1` >> things are getting better now, may be it needs alittle bit more of p
* `-0.07, -0.001, -1` >> ok, may be alittle more again
* `-0.11, -0.001, -1` >> ok, may be alittle more again i hope for the last time
* `-0.13, -0.001, -1` >> Thats it, Here we go ^_^

## Conclusion
The p term is about how much should i steer depending on the current error it is the present time-wise.<br>
The I term is the integration of the past error of the system so it can be good in decreasing hardware issues in the control cycle.<br>
The D term is about predecting what the next step will be and decrease the error which decreases the oscillation of the system.

* in the imgs folder i added some images of the car stopping because of wrong values
---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

Fellow students have put together a guide to Windows set-up for the project [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/files/Kidnapped_Vehicle_Windows_Setup.pdf) if the environment you have set up for the Sensor Fusion projects does not work for this project. There's also an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3).

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

## Editor Settings

We've purposefully kept editor configuration files out of this repo in order to
keep it as simple and environment agnostic as possible. However, we recommend
using the following settings:

* indent using spaces
* set tab width to 2 spaces (keeps the matrices in source code aligned)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).

## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!

More information is only accessible by people who are already enrolled in Term 2
of CarND. If you are enrolled, see [the project page](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/f1820894-8322-4bb3-81aa-b26b3c6dcbaf/lessons/e8235395-22dd-4b87-88e0-d108c5e5bbf4/concepts/6a4d8d42-6a04-4aa6-b284-1697c0fd6562)
for instructions and the project rubric.

## Hints!

* You don't have to follow this directory structure, but if you do, your work
  will span all of the .cpp files here. Keep an eye out for TODOs.

## Call for IDE Profiles Pull Requests

Help your fellow students!

We decided to create Makefiles with cmake to keep this project as platform
agnostic as possible. Similarly, we omitted IDE profiles in order to we ensure
that students don't feel pressured to use one IDE or another.

However! I'd love to help people get up and running with their IDEs of choice.
If you've created a profile for an IDE that you think other students would
appreciate, we'd love to have you add the requisite profile files and
instructions to ide_profiles/. For example if you wanted to add a VS Code
profile, you'd add:

* /ide_profiles/vscode/.vscode
* /ide_profiles/vscode/README.md

The README should explain what the profile does, how to take advantage of it,
and how to install it.

Frankly, I've never been involved in a project with multiple IDE profiles
before. I believe the best way to handle this would be to keep them out of the
repo root to avoid clutter. My expectation is that most profiles will include
instructions to copy files to a new location to get picked up by the IDE, but
that's just a guess.

One last note here: regardless of the IDE used, every submitted project must
still be compilable with cmake and make./

## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).

