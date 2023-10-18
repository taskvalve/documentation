---
title: TypeScript Library
layout: default
nav_order: 4
---

# TypeScript Library Documentation

This library provides the ability to start and signal workflows from TypeScript.

# Usage

## Configuration

The library encrypts workflow data and queued jobs in order to push them to Laravel and therefore needs access to your `APP_NAME` and `APP_KEY` from your Laravel configuration.

## Models

The library supports stored workflow models in MySQL, Redis, and PostgreSQL.

## Queues

The library supports queues for MySQL, Redis, and PostgreSQL.

## Setup

```typescript
import * as taskvalve from "https://deno.land/x/taskvalve@1.0.4/mod.ts"
import { load } from "https://deno.land/std@0.204.0/dotenv/mod.ts"

const env = await load()

const crypto = new taskvalve.DefaultCrypto(env['APP_NAME'], env['APP_KEY'])
const model = new taskvalve.model.MySQL(crypto, env['DB_HOST'], env['DB_PORT'], env['DB_NAME'], env['DB_USER'], env['DB_PASS'])
const queue = new taskvalve.queue.Redis(crypto, model, env['REDIS_HOST'], env['REDIS_PORT'])

const workflow = new taskvalve.WorkflowStub(queue)
```

## Start Workflow

```typescript
const workflowId = await workflow.start('App\\Workflows\\Simple\\SimpleWorkflow', [])
```

## Signal Workflow

```typescript
await workflow.signal(workflowId, 'setReady', [true])
```

# Database Queue

## MySQL

```typescript
const model = new taskvalve.model.MySQL(crypto, env['DB_HOST'], env['DB_PORT'], env['DB_NAME'], env['DB_USER'], env['DB_PASS'])
const queue = new taskvalve.queue.MySQL(crypto, model, env['DB_HOST'], env['DB_PORT'], env['DB_NAME'], env['DB_USER'], env['DB_PASS'])
```

## PostgreSQL

```typescript
const model = new taskvalve.model.PostgreSQL(crypto, env['DB_HOST'], env['DB_PORT'], env['DB_NAME'], env['DB_USER'], env['DB_PASS'])
const queue = new taskvalve.queue.PostgreSQL(crypto, model, env['DB_HOST'], env['DB_PORT'], env['DB_NAME'], env['DB_USER'], env['DB_PASS'])
```

# Redis Queue

## MySQL

```typescript
const model = new taskvalve.model.MySQL(crypto, env['DB_HOST'], env['DB_PORT'], env['DB_NAME'], env['DB_USER'], env['DB_PASS'])
const queue = new taskvalve.queue.Redis(crypto, model, env['REDIS_HOST'], env['REDIS_PORT'])
```

## PostgreSQL

```typescript
const model = new taskvalve.model.PostgreSQL(crypto, env['DB_HOST'], env['DB_PORT'], env['DB_NAME'], env['DB_USER'], env['DB_PASS'])
const queue = new taskvalve.queue.Redis(crypto, model, env['REDIS_HOST'], env['REDIS_PORT'])
```
