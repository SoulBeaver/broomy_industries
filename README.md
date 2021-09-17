# The Mars Rovers

Broomy enterprises has recently extended its reach to Mars! Their suite of state-of-the-art Mars rovers will catalogue the various plateaus and relay their groundbreaking scientific discoveries! However, management has decided that their legacy monolith was no longer suitable to control and maintain the integrity of their rovers. A new development team was assembled to re-create the software from the ground up using a DDD approach! 

## The Mission

Two teams were assembled to guide the process of scientific discovery. A crack-team of analysists and physicists, part of the Mars Topology Team, are constantly monitoring Mars and making predictions where the rovers will have the highest likelihood of success. Once a so called "hot-spot" has been identified, they give it a name and make it available to the Mars Rover Team. The MRT are the ones who deploy and command rovers to the most valuable dig sites. From there the rovers will autonomously scan the area and report back with a groundbreaking, revolutionary discovery or a failure.

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
		"rover_location_heading": "1 2",
		"commands": ["L", "M", "L"]
	}

The last part of the command is the movement sequence. “LML” means, ‘turn left, move, turn left’. 

It is possible to move multiple rovers at the same time as well:

	[{
		"hot_spot": "Mawrth Vallis",
		"rover_location_heading": "1 2",
		"commands": ["L", "M", "L"]
	}, {
		"hot_spot": "Evergreen Terrace",
		"rover_location_heading": "3 0",
		"commands": ["M", "M", "R", "M"]
	}]

If a rover went out of bounds, or if two rovers cross paths by moving across the same grid square, then it is stuck and awaiting rescue. A stuck rover cannot accept any other commands until it has been rescued. Another rover that ends its movement adjacent to a downed rover will automatically repair it.

Once a rover has stopped moving, it will report back with its current state, location and heading. It is then open to new movement commands.

## Making a Discovery

Whenever a rover is moved towards the site of a potential scientific discovery, it automatically scans the surrounding area and notifies the Mars Discovery Team that a discovery has been made. In the event of a discovery or failure, it also notifies the Mars Topology service which removes the dig site from the registered hot-spot. Once all registered hot-spots have been identified, the area is designated as "cold" and removed from the search list. 

The success rate of the scan depends on the richness or scarcity of the plateau. A scarce plateau will always have a 50% chance that no discovery was made, but a rich plateau will always result in a discovery. If the site does not contain a potential discovery, no scan attempt is made. 

## Extracting rovers from a cold hot-spot

Once all dig-sites have been identified, the rovers are recalled by the Rover Extraction team. They are notified automatically once a hot-spot has grown cold and send their own special command, "E" for extraction, to the rovers. The command locks the rovers, making them unable to receive or perform any other command. Some time therafter the rovers are picked up and placed back into storage for use in the next hot-spot.