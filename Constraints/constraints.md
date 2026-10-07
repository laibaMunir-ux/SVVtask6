# Task 1: Identify Constraints

## Lab Task 6: Automated Railway Level-Crossing Control System (ARLCCS)


**C1:** The barrier must not open while a train is present in the crossing.
**Reason:** Road traffic could enter the crossing while the train is passing.

**C2:** When a train is approaching, the warning lights and audible alarm must be active.
**Reason:** Drivers and pedestrians need advance notice to stop and clear the crossing.

**C3:** The barrier may only start lowering after the warning lights and alarm are active.
**Reason:** Vehicles need time to clear the crossing before the barrier closes, otherwise they can be trapped.

**C4:** The barrier may only open after the system has confirmed the train has completely cleared the crossing.
**Reason:** Opening on partial or assumed clearance risks hitting the tail end of a long train.

**C5:** The road traffic signal must be red whenever a train is approaching or present.
**Reason:** It adds a second layer of protection in case drivers ignore the barrier or warnings.

**C6:** Warning lights and alarm must stay on until the barrier is fully open.
**Reason:** Switching them off early gives drivers a false sense of safety while the barrier is still moving.

**C7:** If a train-detection sensor fails, the system must enter a safe state (barrier closed, warnings on, signal red).
**Reason:** A failed sensor cannot prove the track is clear, so the system must assume danger.

**C8:** If communication is lost, the system must enter fail-safe mode.
**Reason:** Without communication, the system cannot trust train status or receive commands.

**C9:** If sensors give conflicting readings, the barrier must not open.
**Reason:** Conflicting data means the train position is uncertain, so the safest assumption is that a train is present.

**C10:** If a barrier fails, the control center must be alerted and the road signal must be red.
**Reason:** A physical failure needs human intervention, and traffic must still be stopped by other means.

**C11:** In an emergency, the barrier must close, the alarm must sound, and the control center must be alerted.
**Reason:** Emergencies need the most restrictive protection and an immediate human response.

**C12:** The barrier cannot report both "open" and "closed" at the same time.
**Reason:** Contradictory states mean a position sensor is faulty or the data is corrupted.
