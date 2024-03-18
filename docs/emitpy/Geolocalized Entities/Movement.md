A Movement is an abstract container for the displacement of a vehicle

- either an aircraft through a flight,
- or a ground support equipment providing a service.

It is a list of successive positions with movement-related information at each position (speeds, etc.) Positions are location where the movement changes, like turns, or change of speed, or sometimes a particular event of the movement like «touch-down».

![[flight-movement2.png]]
## Movement Building

During the construction of the movement, performances of the vehicle is taken into account to determine speed at vertices. In all cases, to simplify, linear acceleration and deceleration is used.
(I.e. there is no "force" computed from vehicle trust and varying vehicle mass (since it burns fuel), etc. just simple realistic kinematics.)
Movement is created using Système International of unit. However, some values may be displayed in more commonly used imperial or aeronautical units like flight level.

## Movement Mark

Movement contain a list of remarkable points called *Marks*. A Mark in a movement is a named point in time of the movement. For example, for a flight, there is a Mark for each flight phase: Off-Block, take-off hold, take-off, top of climb...
The most important data for a Mark is its time relative to the start of the movement. (Each mark name should be unique for the movement, otherwise only the first one encountered is kept.)

## Movement Time

The movement always start at relative time zero. All times of a movement is relative to its start. Each Mark in the movement will have a time of occurrence relative to the start of the movement.

When a Movement is created, its positions can be [[Emit, Schedule, Format|broadcast]].