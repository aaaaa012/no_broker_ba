# NoBroker - Rental Marketplace Platform

[![Industry](https://img.shields.io/badge/Industry-Real%20Estate-green)](https://github.com/topics/real-estate)
[![Stack](https://img.shields.io/badge/Stack-React%20|%20Node-blue)](https://github.com/topics/react)

## 📌 Executive Summary

**NoBroker (Kathmandu Edition)** is a disruptive rental marketplace connecting tenants directly with property owners, eliminating the middleman. This project targets the inefficiencies in the Kathmandu rental market, focusing on transparency, verified listings, and direct communication.

**Problem Solved:**
*   Eliminates hefty brokerage fees (often 1 month's rent).
*   Reduces spam/fake listings through strict verification.
*   Provides a digital agreement and payment trail.

---

## 📂 Repository Structure

The documentation is split for clarity. Please review the specific sections below:

*   **[Full Documentation](./FULL_DOCUMENTATION.md)**: The Master document containing all specifications.
*   **[Diagrams](./diagrams/)**: Visual workflows and ERD.

---

## 🛠️ Technology Stack

*   **Frontend**: React (TypeScript), Tailwind CSS
*   **Backend**: Node.js, Express
*   **Database**: PostgreSQL
*   **Auth**: JWT & OTP Validation

---

## 🔄 User Journey: Tenant

```mermaid
journey
    title Tenant Experience
    section Discovery
      Search Properties: 5: Tenant
      Filter by Location/Price: 5: Tenant
      View Virtual Tour: 4: Tenant
    section Connection
      Request Contact: 5: Tenant
      Owner Verification: 3: System
      Receive Owner Details: 5: Tenant
    section Closure
      Schedule Visit: 4: Tenant
      Sign Digital Agreement: 5: Tenant, Owner
```
