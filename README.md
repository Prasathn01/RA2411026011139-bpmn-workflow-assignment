# Workflow Automation Engineering — BPMN Assignment

Three BPMN 2.0 process models built with **Camunda Desktop Modeler**, one per scenario. Each `.bpmn` file can be opened directly in Camunda Modeler for review or editing.





---

## Scenario 1: Employee Leave Approval

**File:** `diagrams/leave-approval.bpmn`

An employee submits a leave request. The HR system first checks whether the employee has enough leave balance:

- **Insufficient balance** → the system immediately sends an insufficient-balance notification and the process ends.
- **Sufficient balance** → the request goes to the manager for approval.
  - **Manager approves** → the system updates the leave balance and sends an approval notification.
  - **Manager rejects** → the system sends a rejection notification.

The process has three possible outcomes (insufficient balance, approved, rejected), each ending at its own End Event, driven by two Exclusive Gateways: *Balance Sufficient?* and *Manager Approves?*.

## Scenario 2: Online Purchase Order Processing

**File:** `diagrams/purchase-order.bpmn`

A customer places an order. The system checks product availability:

- **Out of stock** → the customer is notified and the process ends immediately.
- **Available** → the system processes payment.
  - **Payment fails** → the customer is notified of the failure and the process ends.
  - **Payment succeeds** → the order is confirmed, the product is prepared, shipped, and a shipping confirmation is sent to the customer before the process ends.

This models three distinct end-to-end paths (out-of-stock, payment-failed, fulfilled) using two Exclusive Gateways: *Product Available?* and *Payment Successful?*.

## Scenario 3: IT Service Request

**File:** `diagrams/it-service-request.bpmn`

An employee reports an IT problem. The request is submitted, registered, and its severity assessed:

- **Low severity** → assigned to a support technician.
- **High severity** → assigned to a senior technician.

Both paths converge and the assigned technician investigates the problem:

- **Resolvable internally** → the technician fixes it directly.
- **Not resolvable internally** → the technician escalates it to the external service provider.

Both paths converge again, after which the help desk updates the request status and the employee receives a resolution notification before the process ends.

This scenario uses two diverging Exclusive Gateways (*Severity Level?*, *Resolvable Internally?*) paired with converging gateways to merge the parallel branches back into a single flow before the final steps — showing multiple alternative paths that all funnel into one End Event.

---

## Notes for evaluation

- All three models use only the basic BPMN building blocks required: **Start Event, Tasks, Exclusive Gateways, End Events**.
- Every gateway branch is labeled (Yes/No, Low/High) so the decision logic is unambiguous.
- Every path in every diagram terminates at an End Event — no dangling flows.
- Models were built and validated in Camunda Desktop Modeler (Camunda 8).
