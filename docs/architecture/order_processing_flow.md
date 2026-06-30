# Order Processing Orchestration Flow

## Architecture Overview

This diagram illustrates the complex orchestration handled by WSO2 Micro Integrator during Order Processing. It utilizes several Enterprise Integration Patterns (EIP):
- **Wire Tap**: Asynchronous audit logging and email notifications.
- **Content-Based Routing**: Routing payments to Stripe vs PayPal based on request details.
- **Saga Compensation**: Rolling back inventory and payment if shipping fails.

```mermaid
sequenceDiagram
    participant Client
    participant WSO2_MI as WSO2 Micro Integrator
    participant Cust as Customer Service
    participant Inv as Inventory Service
    participant Pay as Payment Gateway
    participant Ship as Shipping Service
    participant Audit as Audit Service (Async)
    participant Notif as Notification Service (Async)

    Client->>WSO2_MI: POST /orders
    activate WSO2_MI
    
    WSO2_MI-->>Audit: (Wire Tap) Clone Request for Audit
    
    WSO2_MI->>WSO2_MI: Validate & Transform to Canonical Order
    
    WSO2_MI->>Cust: VerifyCustomerSeq
    Cust-->>WSO2_MI: 200 OK
    
    WSO2_MI->>Inv: ReserveInventorySeq
    Inv-->>WSO2_MI: 200 OK
    
    WSO2_MI->>Pay: ProcessPaymentSeq (Stripe/PayPal)
    Pay-->>WSO2_MI: 200 OK
    
    WSO2_MI->>Ship: CreateShipmentSeq
    alt Shipping Success
        Ship-->>WSO2_MI: 201 Created
        WSO2_MI->>WSO2_MI: GenerateOrderSeq (DB)
        WSO2_MI-->>Notif: (Wire Tap) Send Email Notification
        WSO2_MI-->>Client: 201 Created
    else Shipping Failure / Timeout
        Ship-->>WSO2_MI: 504 Timeout
        WSO2_MI->>WSO2_MI: Trigger Compensation Sequences
        WSO2_MI->>Pay: Void Payment (PaymentCompensationSeq)
        WSO2_MI->>Inv: Release Stock (InventoryCompensationSeq)
        WSO2_MI-->>Client: 500 Internal Server Error (Rollback successful)
    end
    
    deactivate WSO2_MI
```
