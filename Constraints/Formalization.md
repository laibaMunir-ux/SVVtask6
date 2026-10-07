# Task 2: Formalize Constraints

## Lab Task 6: Automated Railway Level-Crossing Control System (ARLCCS)

## Predicates

| Symbol | Meaning |
|---|---|
| TP | Train_Present (in crossing) |
| TA | Train_Approaching |
| TC | Train_Cleared (confirmed by exit sensor) |
| BO | Barrier_Open |
| BC | Barrier_Closed |
| WA | Warning_Light_On |
| AL | Alarm_On |
| RR | Road_Signal_Red |
| SF | Sensor_Fault |
| CL | Comm_Loss |
| SC | Sensor_Conflict |
| BF | Barrier_Fault |
| EM | Emergency |
| CCA | Control_Center_Alerted |
| FS | Fail_Safe_Mode |

**Notation:** ∧ AND, ∨ OR, ¬ NOT, → implies

## Person A

| ID | Constraint | Formal expression |
|---|---|---|
| F1 | C1 | TP → ¬BO |
| F2 | C2 | TA → (WA ∧ AL) |
| F3 | C3 | Barrier_Lowering → (WA ∧ AL) |
| F4 | C4 | Barrier_Opening → (TC ∧ ¬TP) |
| F5 | C5 | (TA ∨ TP) → RR |

