
# Notification Center

A centralized notification delivery platform that allows applications to send and manage user notifications through a unified API.

## Overview

Notification Center provides a common interface for sending notifications through different channels, such as Email and Telegram.

Instead of implementing notification logic separately in every application, developers can integrate with Notification Center and delegate notification delivery to it.

## Goals

- Provide a unified API for sending notifications.
- Support asynchronous notification processing.
- Track notification and delivery status.
- Implement retry and failure handling.
- Provide a foundation for learning and practicing DevOps and DevSecOps.

## MVP Scope

The first version will focus on:

- Application registration and API key authentication.
- Sending notifications through an API.
- Asynchronous notification processing.
- Supporting Email and Telegram as initial channels.
- Tracking notification and delivery status.
- Basic retry and failure handling.
- API documentation and automated tests.

Features such as Kafka, Kubernetes, advanced analytics, and additional notification channels are outside the initial MVP scope.

## Planned Technology Stack

| Component | Technology |
|---|---|
| Main API | Laravel |
| Notification Worker | Go |
| Database | PostgreSQL |
| Queue / Cache | Redis |
| Containerization | Docker |
| CI/CD | To be determined |
| Infrastructure | To be determined |

The MVP will initially run without Docker. Containerization and deployment automation will be introduced after the MVP is completed.

## High-Level Architecture

```text
Client Application
       |
       | HTTP API
       v
Laravel API
       |
       v
Notification Queue
       |
       v
Go Worker
       |
   +---+---+
   |       |
   v       v
 Email  Telegram
```

## Development Plan

1. Define the MVP and API contracts.
2. Design the initial database schema.
3. Implement the Laravel API.
4. Implement the notification queue and Go worker.
5. Add notification delivery status and retry handling.
6. Add tests and documentation.
7. Containerize the application with Docker.
8. Implement CI/CD.
9. Add monitoring and infrastructure automation.
10. Explore security improvements and DevSecOps practices.

## Repository Structure

The repository structure will be finalized during the initial architecture phase.

## Contribution

All changes should be made through feature branches and Merge Requests.

The `main` branch should remain protected.

## License

To be determined.
