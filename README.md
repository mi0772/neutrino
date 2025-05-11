# Neutrino

Neutrino is a messaging system designed to simplify and accelerate communication between microservices in distributed systems. Built in Go, it provides a lightweight, partitioned, persistent message transport layer with minimal configuration and strong defaults.

## Mission

The goal of Neutrino is to offer a fast, robust, and self-contained communication backbone for modern service-oriented architectures. It is designed to work seamlessly in containerized environments, requiring no centralized brokers, no manual topic setup, and no external dependencies for node discovery or message persistence.

Neutrino aims to reduce operational complexity while maintaining high performance and reliability in event-driven architectures.

## Features

- **Auto-discovery**: Nodes automatically discover each other using a peer-to-peer gossip protocol.
- **Partitioned topics**: Messages are distributed across partitions to enable parallelism and scalability.
- **Durable log-based storage**: Each partition is persisted locally using embedded key-value stores, ensuring recovery after restarts.
- **Simple HTTP/gRPC interfaces**: Easy-to-use interfaces for publishing and consuming messages.
- **Cloud-native by design**: Deployable as a single binary, container-friendly, and requiring minimal configuration.

## Current Prototype

- HTTP-based `/publish` endpoint with dynamic topic handling.
- Message logging to standard output (temporary for initial testing).
- Modular project structure prepared for future storage and discovery layers.

## Planned Components

### Messaging Core
- Internal broker with in-memory routing and queueing
- Partition assignment based on consistent hashing
- Load-balanced message delivery to consumers

### Storage
- Append-only persistent logs per partition
- Message replay support
- Pluggable storage backends (starting with BadgerDB)

### Node Discovery
- Decentralized cluster membership via gossip protocol
- Heartbeat and failure detection
- Dynamic peer list updates

### Interfaces
- REST and gRPC APIs for message production and consumption
- CLI tool for publishing and diagnostics
- Subscription models: at-most-once, at-least-once (future)

### Deployment
- Minimal configuration via environment variables or config file
- Helm chart and Kubernetes manifest
- Native Prometheus metrics endpoint

## Getting Started

```bash
git clone https://github.com/yourname/neutrino.git
cd neutrino
go run cmd/neutrinod/main.go
```

Test publishing a message:

```bash
curl "http://localhost:8080/publish?topic=test&msg=hello"
```

## License

This project is licensed under the MIT License.
