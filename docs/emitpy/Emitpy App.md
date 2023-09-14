
# Steps for each do_ function

(do_flight, do_service, do_flight_services, do_mission)

1. Collect data
3. Create flight/mission/service...
4. Create move
5. (save move?)
6. Create emit
7. Schedule emit
8. (save emit?)
9. Schedule messages
10. (save messages?)
11. Create format + format
12. (save format?)
13. Format messages
14. (save format messages)
15. Enqueue positions
16. Enqueue messages
17. Done + summary

# Steps for each re-Schedule function

1. Create ReEmit (this will also create ReMessages)
2. Schedule emit
3. (save emit?)
4. Schedule messages
5. (save messages?)
6. Create format + format
7. (save format?)
8. Format messages
9. (save format messages)
10. Enqueue positions (this will remove old emissions)
11. Enqueue messages (this will remove old messages)
12. Done + summary
