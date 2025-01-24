<h1 align="center">eventsourcing_inmemory</h1>

<div align="center">
  ✨ <strong>In-Memory Event Store Implementation for Eventsourcing</strong> ✨
</div>

<div align="center">
  <a href="https://hex.pm/packages/eventsourcing_inmemory">
    <img src="https://img.shields.io/hexpm/v/eventsourcing_inmemory" alt="Package Version" />
  </a>
  <a href="https://hexdocs.pm/eventsourcing_inmemory">
    <img src="https://img.shields.io/badge/hex-docs-ffaff3" alt="Hex Docs" />
  </a>
</div>

---

## Introduction

`eventsourcing_inmemory` provides an in-memory event store implementation for the [eventsourcing](https://github.com/renatillas/eventsourcing) library.
It's designed for development, testing, and small-scale applications where persistence isn't required.

## Features

- **In-Memory Storage**: Fast, non-persistent event storage
- **Snapshot Support**: Built-in snapshot management for optimizing aggregate rebuilding
- **Concurrent Access**: Safe concurrent access to events and snapshots
- **Error Handling**: Comprehensive error handling with timeouts and process monitoring
- **Zero Configuration**: Ready to use with minimal setup

## Installation

Add to your Gleam project:

```sh
gleam add eventsourcing_inmemory
```

## Usage

### Basic Setup

```Gleam
import eventsourcing
import eventsourcing_inmemory

pub fn main() {
  // Create a new in-memory event store
  let store = eventsourcing_inmemory.new()
  
  // Create an event sourcing instance with the store
  let event_sourcing = eventsourcing.new(
    event_store: store,
    queries: [],
    handle: your_command_handler,
    apply: your_event_applier,
    empty_state: your_empty_state,
  )
  // Enable snapshots (optional)
  |> with_snapshots(
    event_sourcing,
    eventsourcing.SnapshotConfig(100), // Snapshot every 100 events
  )
}
```
