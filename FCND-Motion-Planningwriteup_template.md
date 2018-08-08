## Project: 3D Motion Planning
![Quad Image](./misc/enroute.png)

---


# Required Steps for a Passing Submission:

1. Load the 2.5D map in the colliders.csv file describing the
   environment.
2. Discretize the environment into a grid or graph representation.
3. Define the start and goal locations.
4. Perform a search using A* or other search algorithm.
5. Use a collinearity test or ray tracing method (like Bresenham) to
   remove unnecessary waypoints.
6. Return waypoints in local ECEF coordinates (format for
   `self.all_waypoints` is [N, E, altitude, heading], where the
   drone’s start location corresponds to [0, 0, 0, 0].
7. Write it up.
8. Congratulations!  Your Done! 

## [Rubric](https://review.udacity.com/#!/rubrics/1534/view) Points

### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it! Below I describe how I addressed each rubric point
and where in my code each point is handled.

### Explain the Starter Code

#### 1. Explain the functionality of what's provided in `motion_planning.py` and `planning_utils.py`

These scripts contain a [basic planning implementation](./Planner.png) that includes
moving from the origin to a latitude/longitude with some weird
mirroring, avoiding obstacles, and [removing extraneous waypoints](./Flight.png).

### Implementing Your Path Planning Algorithm

#### 1. Set your global home position

The first line of the `colliders.csv` file is read, stripped of
whitespace, split into four fields, and then the 2nd and 4th converted
to floating point numbers. These are used to set the global origin
position of the map, and then to calculate the local origin and grid
locations.

And here is a lovely picture of our downtown San Francisco environment
from above!  ![Map of SF](./misc/map.png)

#### 2. Set your current local position

The local position is read from the drone API and converted to a
global position and used for calculating a path in grid coordinates.

Meanwhile, here's a picture of me flying through the trees!  ![Forest
Flying](./misc/in_the_trees.png)

#### 3. Set grid start position from local position

See #2.

#### 4. Set grid goal position from geodetic coords

The goal position is calculated from the geodetic coordinates, but for
some reason everything is mirrored.

#### 5. Modify A* to include diagonal motion (or replace A* altogether)

Four diagonal directions were added, and the `valid_actions` function
was modified to support them, and to treat the actions as vectors
instead of weird conditionals.

#### 6. Cull waypoints 

Intermediate waypoints collinear within 5m are culled to simplify the
path.

### Execute the flight

####  Does it work?

Plans avoiding obstacles are successfully chosen and flown. The
coordinates seem to have a strange mirroring when converted from
geodetic coordinates in some cases.


