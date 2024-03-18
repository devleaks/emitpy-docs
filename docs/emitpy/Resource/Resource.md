A resource is a named entity that maintains a list of usage times (allocations called Reservation).

Emitpy maintain the following resources:
- Runway
- Ramp (or aircraft parking)
- Equipement

(Aircrafts usage are not managed through resources.)

From the collection of existing allocations, it is possible to determine the next time a resource is available.

# Reservation

A Reservation is a time slot. It has a start and an end date/time, or a start time and a duration.