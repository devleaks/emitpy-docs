
At the current stage of development, there is little randomization of parameter selection.
However, there are enough randomization already to prevent exact reproduction execution.

Some randomness is brought by the weather forecast that changes. If historical weather is not found, current weather is used, and weather changes...

Even with constant weather or no weather, randomness is present. If there is no wind, a random direction for takeoff is selected, often, a random SID (towards the overall destination) is also selected. At the arrival, similar random selections occur.

Randomness can also occur when some values cannot be found. For example, if a ramp is not provided for a flight, a random ramp at the airport is selected.

These choice make exact reproduction of generated track almost impossible.

However, experimentally, whenever a failure occurs during track generation, it will more than probably occur again later. By accumulating failing generations, a trend will appear and allow for code adjustment.

# The Future of Randomness

Randomness can be brought at numerous stage in the simulation.

1. Random destination (expand flight routes!)
2. Random delays in all timing: flights, services, etc.
