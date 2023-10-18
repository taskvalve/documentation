---
title: CLI Application
layout: default
nav_order: 2
---

# CLI Application Documentation

This documentation provides a comprehensive guide on how to use the `taskvalve` Command Line Interface (CLI). The CLI allows you to manage and deploy your functions as well as view logs.

## Table of Contents

1. [Login](#login)
2. [Functions](#functions)
3. [Secrets](#secrets)

## Login

Before performing any operations, you need to login:

```bash
npx taskvalve login
```

You'll be prompted to enter your credentials. Upon successful login, you will be authenticated to execute other commands.

## Functions

Functions are the main units of execution within the `taskvalve` environment. Here's how you can manage them:

#### List All Functions:

```bash
npx taskvalve functions list
```

This command displays a list of all your existing functions.

### Create a New Function:

```bash
npx taskvalve functions new <name>
```

Replace `<name>` with your desired function name.

### Deploy a Function:

After writing your function, you'll need to deploy it:

```bash
npx taskvalve functions deploy <name>
```

### Remove a Function:

To delete a function:

```bash
npx taskvalve functions remove <name>
```

### Execute a Function:

You can run a function with optional arguments:

```bash
npx taskvalve functions run <name> <arg1> <arg2> ...
```

### Authentication for Function Endpoint:

Toggle authentication for a function's endpoint:

```bash
npx taskvalve functions authentication <name> <true|false>
```

`<true|false>` will either enable or disable authentication.

### View Function Logs:

Check logs for debugging or monitoring:

```bash
npx taskvalve functions logs [-n 10] [-f]
```

- `-n 10` will display the last 10 logs. Replace 10 with any other number as required.
- `-f` enables you to tail or follow the logs in real-time.

### View Function Executions:

Inspect previous executions:

```bash
npx taskvalve functions executions [-n 10] [-f]
```

## Secrets

Secrets allow you to store sensitive data securely:

### List All Secrets:

```bash
npx taskvalve secrets list
```

### Set a Secret:

Store a new secret or update an existing one:

```bash
npx taskvalve secrets set <key> <value>
```

### Remove a Secret:

If a secret is no longer needed:

```bash
npx taskvalve secrets remove <key>
```
