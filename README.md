# Udacity-RoboND-Rover-Project

# Notebook Analysis

### find_rocks()

the rocks color spectrum was found to be above 100 for red, and green, while the blue had a limit of 50. the find_rocks() function is simply a copy of color_thresh() with a different RGB threshold = [110,110,50] and adjustment to the Boolean array for blue to be less than 50. To mark the world map with the rocks position I performed coordinate transforms then applied them to the world map. The rocks are highlighted white at magnitude of 250. 

## Obstacle location

To highlight the obstacles in the world map I inverted the binary output of the color_thresh() function. The obstacle location is applied to the world map using the same coordinate transforms steps as the path terrain. 

To increase the accuracy of the world map. I set the obstacle pixel magnitude +1 red, and the path pixels to +10 blue. as the rover does multiple passes over the same area one of colors will begin to exceed the other. a check will occur if one color exceeds the other the lesser will be set to zero. by adding these steps my world map accuracy went from 61% to 97%. 

# Autonomous Navigation and Mapping

## perception_step()
the perception_step() was filled using the same methods as the process_image() function in the test notebook. a few modifications were made access the Rover class, as well as add two new statements Rover.nav_dists, and Rover.nav_angles. the statements saved the mean distance and mean angle of the rover polar coordinates. these statements are used to direct the rover’s movement and identify when approaching obstacles. 

## decision_step()
I began by replacing the angle array length in the if statements to Rover.nav_dists, and set Rover.stop_foward, and Rover.go_forward statements to 28, and 50. with the if statement changed the rover would no longer approach an obvious dead end or obstacle. I found 28 to be the ideal distance to map out the area without unnecessary overlap. the next issue was identifying a clear path for the rover when turning around. I created a boundary condition only allowing angles between +-30 degrees and a Rover.nav.dist exceeding 50. this ensured a clear traversable path ahead of ahead of the rover. previously the rover could be caught on the edge of an obstacle that it perceived as passable.

## Possible Improvements

pitch and roll are an issue at when turning and braking. I would add additional steps to slow the braking and turning rate. 
there are a few places on the map the rover can’t identify perfectly. I would create a process for the rover to identify edges in the terrain and identify already mapped out areas. the rover would be able to complete the terrain mapping.  
