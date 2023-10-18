---
title: CLI Application
layout: default
nav_order: 2
---

# Usage

## Login

```bash
npx taskvalve login
```

## Functions

To list all functions:

```bash
npx taskvalve functions list
```

To create a new function:

```bash
npx taskvalve functions new <name>
```

To deploy a function:

```bash
npx taskvalve functions deploy <name>
```

To remove a function:

```bash
npx taskvalve functions remove <name>
```

To run a function:

```bash
npx taskvalve functions run <name> <arg1> <arg2> ...
```

To set authentication for a function endpoint:

```bash
npx taskvalve functions authentication <name> <true|false>
```

To view function logs:

```bash
npx taskvalve functions logs <-n 10> <-f>
```

To view function executions:

```bash
npx taskvalve functions executions <-n 10> <-f>
```

## Secrets
To list all secrets:

```bash
npx taskvalve secrets list
```

To set a secret:

```bash
npx taskvalve secrets set <key> <value>
```

To remove a secret:

```bash
npx taskvalve secrets remove <key>
```
