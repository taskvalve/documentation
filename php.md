---
title: PHP Library
layout: default
nav_order: 3
---

# PHP Library Documentation

The `Functions` library provides a convenient way to run TypeScript functions in the cloud directly from your Laravel PHP workflows. This ensures a seamless integration between your PHP backend and TypeScript cloud functions.

## Table of Contents

1. [Installation](#installation)
2. [Configuration](#configuration)
3. [Usage](#usage)
4. [Examples](#examples)

## Installation

To get started, install the `taskvalve/functions` package using composer:

```bash
composer require taskvalve/functions
```

## Configuration

For the library to function correctly, it requires an API key. You should set this up in two places: 

### `config/services.php`

Add the TaskValve configuration to your `services.php`:

```php
'taskvalve' => [
    'api_key' => env('TASKVALVE_API_KEY'),
],
```

### `.env`

Set the API key in your environment file:

```
TASKVALVE_API_KEY=[YOUR_API_KEY]
```

## Usage

Using the `CloudFunction` in your Laravel workflows is straightforward. Here's a simple example:

```php
use TaskValve\CloudFunction;
use Workflow\ActivityStub;
use Workflow\Workflow;
use Workflow\WorkflowStub;

class MyWorkflow extends Workflow
{
    public function execute()
    {
        return yield ActivityStub::make(CloudFunction::class, 'my-function');
    }
}
```

This method triggers the TypeScript function in the cloud and returnst the response from the cloud function in JSON format.

## Examples

The TypeScript cloud functions need to be constructed to handle HTTP requests and responses. Here's an example of a TypeScript function that returns a simple JSON response:

### Return JSON

```typescript
export default async (request) => {
    return new Response(JSON.stringify({ data: ['test'] }), { 
        headers: { 'content-type': 'application/json' }
    });
}
```

For more details on handling requests and responses with cloud functions, refer to the [Fetch API documentation](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).
