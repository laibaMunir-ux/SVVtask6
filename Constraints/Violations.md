# Task 3: Identify Constraint Violations

## Lab Task 6: Automated Railway Level-Crossing Control System (ARLCCS)

A constraint P → Q is violated exactly when **P is TRUE and Q is FALSE**. The safety-monitoring unit detects this by evaluating each formula every control cycle.

### V1 (violates F1: TP → ¬BO)
- **Scenario:** A timer bug opens the barrier while the train's rear carriages are still in the crossing.
- **State:** TP = TRUE, BO = TRUE
- **How we know:** TP is true and ¬BO is false, so TRUE → FALSE is FALSE. The monitor sees "train present" and "barrier open" together.

### V2 (violates F2: TA → (WA ∧ AL))
- **Scenario:** The approach sensor detects the train, but the warning-light controller does not respond.
- **State:** TA = TRUE, WA = FALSE, AL = TRUE
- **How we know:** WA ∧ AL is false because WA is false. The monitor compares light status feedback against the sensor input.

### V3 (violates F3: Barrier_Lowering → (WA ∧ AL))
- **Scenario:** The control logic sends the lower-barrier command before the alarm turns on.
- **State:** Barrier_Lowering = TRUE, AL = FALSE, WA = TRUE
- **How we know:** The lowering command is active but the alarm is off. The event log shows the barrier command timestamped before alarm activation.

### V4 (violates F4: Barrier_Opening → (TC ∧ ¬TP))
- **Scenario:** The system opens the barrier on a timeout, but the exit sensor never confirmed clearance.
- **State:** Barrier_Opening = TRUE, TC = FALSE
- **How we know:** The open command was issued without the TC flag. The log shows no exit-sensor event before the command.

### V5 (violates F5: (TA ∨ TP) → RR)
- **Scenario:** The traffic-light controller is stuck on green while a train is approaching.
- **State:** TA = TRUE, RR = FALSE
- **How we know:** Signal is green while train detection is active. The monitor compares commanded signal against signal feedback.

### V7 (violates F7: SF → (BC ∧ WA ∧ RR))
- **Scenario:** The entry sensor fails and the system continues normal operation, leaving the barrier open and the signal green.
- **State:** SF = TRUE, BC = FALSE, RR = FALSE
- **How we know:** Self-test flags the sensor fault, but barrier and signal are not in their safe state.

### V8 (violates F8: CL → FS)
- **Scenario:** Communication with the control center drops, but the crossing runs on stale data with the barrier open.
- **State:** CL = TRUE, FS = FALSE, BC = FALSE
- **How we know:** The heartbeat timeout sets CL, but there is no transition to fail-safe mode.

### V9 (violates F9: SC → ¬BO)
- **Scenario:** Sensor 1 reports "track clear" and Sensor 2 reports "train present"; the system trusts Sensor 1 and opens the barrier.
- **State:** SC = TRUE, BO = TRUE
- **How we know:** The sensor cross-check disagrees, which should block opening, yet BO is true.

### V10 (violates F10: BF → (CCA ∧ RR))
- **Scenario:** The barrier motor jams halfway, but no alert is sent and the road signal stays green.
- **State:** BF = TRUE, CCA = FALSE, RR = FALSE
- **How we know:** The motor-current or position fault is detected, but the alert log is empty and the signal is not red.

### V11 (violates F11: EM → (BC ∧ AL ∧ CCA))
- **Scenario:** An emergency stop is triggered (e.g. obstruction on the track), but the barrier stays open and the control center is not notified.
- **State:** EM = TRUE, BC = FALSE, CCA = FALSE
- **How we know:** The emergency input is active, but the position sensor reads open and no alert was transmitted, so the formula fails.

**Total violations:** 10 (requirement: at least 8).
