# MCP Order Management Demo

A .NET demo showing how the Model Context Protocol (MCP) can expose existing application capabilities to AI applications without duplicating business logic or breaking application boundaries.

This project accompanies the talk **"MCP is Not a Magic Word: What It Means for Software Architecture"** at dotNET Conf 2026.

## Overview

MCP provides a standard way for AI applications to discover and interact with tools, resources, and other capabilities exposed by external systems.

However, introducing MCP does not remove the need for good software architecture. Authentication, authorisation, validation, observability, error handling, and application boundaries still matter.

This demo explores how MCP can fit into an existing .NET application by exposing a selected business capability through an MCP server while keeping the business logic inside the application.

## What This Demo Covers

The demo uses a simple order management application to illustrate how an AI application can interact with existing business capabilities through MCP.

The planned example includes

- An existing `OrderService` responsible for order-related business logic.
- An MCP server exposing a `get_order_status` tool.
- An MCP client that discovers and invokes the tool.
- A request flow from the MCP server to the existing application service.
- Basic input validation and error handling.

The MCP server acts as an integration layer. It does not replace the application service or access the database directly.

## Architecture

The intended request flow is

```text
AI Application
      |
      v
  MCP Client
      |
      v
  MCP Server
      |
      v
  OrderService
      |
      v
 Order Repository
```

The `OrderService` remains responsible for the business logic, while the MCP server exposes a narrow interface that an AI application can use.

This approach allows the application to support different consumers without duplicating its core business rules.

## Example Tool

The demo will expose a tool similar to

```text
get_order_status(orderId)
```

The tool accepts an order ID and returns information such as the order status and expected delivery date.

The exact input and output schema will be defined in the implementation.

## Design Principles

This project follows a few simple architectural principles:

- **Reuse existing application services.** Keep business logic in the application layer rather than duplicating it inside MCP tools.
- **Expose narrow capabilities.** Give AI applications access only to the operations they need.
- **Validate all inputs.** A valid MCP request is not automatically a valid business operation.
- **Enforce access controls.** The server must determine whether the caller is allowed to perform the requested operation.
- **Design for failure.** Handle timeouts, unavailable services and invalid requests explicitly.
- **Make tool calls observable.** Ensure requests and failures can be traced through the application.

## Technology

The project is being developed with

- C#
- .NET
- Model Context Protocol (MCP)
- Official MCP C# SDK

Additional dependencies will be documented as the implementation develops.

## Getting Started

Setup and execution instructions will be added once the demo implementation is complete.

## Project Status

This project is currently under development as a conference demonstration for dotNET Conf 2026.

The implementation and documentation may change as the demo is developed and reviewed.

## Talk

**MCP is Not a Magic Word: What It Means for Software Architecture**

The talk explores where MCP fits into an application, how MCP servers relate to traditional APIs and services, and what changes when AI becomes a consumer of application capabilities.

The central idea is that MCP is a protocol, not an architecture. It provides a standard way to connect AI applications to capabilities, but the architecture, security, boundaries and reliability of those capabilities remain the responsibility of the engineering team.
