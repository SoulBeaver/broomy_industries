# The Mars Rovers

Broomy enterprises has recently extended its reach to Mars! Their suite of state-of-the-art Mars rovers will catalogue the various plateaus and relay their groundbreaking scientific discoveries! However, management has decided that their legacy monolith was no longer suitable to control and maintain the integrity of their rovers. A new development team was assembled to re-create the software from the ground up using a DDD approach! 

## The Mission

Two teams were assembled to guide the process of scientific discovery. A crack-team of analysists and physicists, part of the Mars Topology Team, are constantly monitoring Mars and making predictions where the rovers will have the highest likelihood of success. Once a so called "hot-spot" has been identified, they give it a name and relay that information to the Mars Rover Team who deploy and command their rovers to the most valuable dig sites. From there the rovers will autonomously scan the area and report back with a groundbreaking, revolutionary discovery or a failure.

## Your Task

Your task is to build the software that will allow the Mars Topology team to register hot-spots and enable the the Mars Rover team to deploy and move their rovers towards the dig sites. It should be possible to view all active hot-spots that have rovers deployed, their locations and the remaining dig sites.

## Registering a hot-spot

The Mars Topology team uses another software to scan the surface of Mars in pursuit of hot-spots. Once such an area has been identified, it is registered and catalogued.

Registering a hot-spot

	{
		"hot_spot": "Mawrth Vallis",
		"dimensions": "3 3",
		"yield": "scarce",
		"dig_sites": ["1 2", "3 3"]
	}

A hot-spot will always have a name and dimensions condensed to a x, y coordinate system. In this case, Mawrth Vallis has a width and height of 3. Tagging the area as scarce or rich determines how likely it is for a rover to find something interesting at a dig site. Finally, all following coordinate pairs are interesting dig sites the rover should explore and exhaust.

## Deploying a Mars Rover

After a hot-spot has been designated, a rover is deployed to the area.

	{
		"hot_spot": "Mawrth Vallis",
		"deployment_heading": "1 2 N"
	}

Mawrth Vallis identifies the hot-spot, and “1 2 N” indicates that the rover is to be deployed on grid square 1,2 pointing north. So, if the rover moved, it would move in the direction it was facing, in this case north.

## Moving a Mars Rover

To move a placed rover, it must be identified by the hot-spot and its coordinates, then fed with a chain of commands.

	{
		"hot_spot": "Mawrth Vallis",
		"rover_location_heading": "1 2 N",
		"commands": ["L", "M", "L"]
	}

The last part of the command is the movement sequence. “LML” means, ‘turn left, move, turn left’. 

Additionally, the rover must not drive off the plateau. Should a human error occur, e.g. should an operator try to drive the multi-million-dollar rover off the plateau, the rover should stop and await rescue. Once a rover has stopped moving (and finished its scan), it is open to new movement commands again.

## Making a Discovery

Whenever a rover is moved towards the site of a potential scientific discovery, it automatically scans the surrounding area and returns a message indicating that a discovery has been made or that the scan was inconclusive. The success rate of the scan depends on the richness or scarcity of the plateau. A scarce plateau will always have a 50% chance that no discovery was made, but a rich plateau will always result in a discovery. If the site does not contain a potential discovery, no scan attempt is made. 

## Rescuing a downed rover

If a rover attempted to go out of bounds, then it is stuck and awaiting rescue. Another rover that ends its movement adjacent to a downed rover will automatically repair it.

## An example hot spot

	{
		"hot_spot": "Mawrth Vallis",
		"dimensions": "50 50",
		"yield": "scarce",
		"dig_sites": ["34 19", "1 1", "42 5", "21 27", "19 50", "19 40", "5 10"]
	}