---
title: REST API
layout: default
nav_order: 5
---

# TaskValve API Documentation

## Table of Contents

- [Authentication](#authentication)
- [User Settings](#user-settings)
- [Workflows](#workflows)
  - [Retrieve Workflows](#retrieve-workflows)
- [Activities](#activities)
  - [Retrieve Activities](#retrieve-activities)
- [Selecting](#selecting)
  - [Including](#including)
  - [Excluding](#excluding)
- [Filtering](#filtering)
  - [eq](#eq)
  - [neq](#neq)
  - [gt](#gt)
  - [gte](#gte)
  - [lt](#lt)
  - [lte](#lte)
  - [like](#like)
  - [ilike](#ilike)
- [Ordering](#ordering)
- [Limit](#limit)
- [Range Limiting](#range-limiting)
- [Retrieve as CSV](#retrieve-as-csv)

## Authentication

Authenticate with email and password:

```bash
curl -X POST 'https://api.taskvalve.com/auth/v1/token?grant_type=password' \
-H "apikey: PUBLIC_API_KEY" \
-H "Content-Type: application/json" \
-d '{
  "email": "your_email@example.com",
  "password": "your_password"
}'
```

Auth Response

```json
{
  "access_token": "YOUR_ACCESS_TOKEN",
  "token_type": "bearer",
  "expires_in": 3600,
  ...
}
```

## User Settings

Retrieve user settings:

```bash
curl 'https://api.taskvalve.com/rest/v1/user_settings?select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

Settings Response

```json
[
  {
    "user_id": "YOUR_USER_ID",
    "notify_failed_workflows": false
    "notify_failed_activities": false,
  }
]
```

Update user settings:

```
curl -X PATCH 'https://api.taskvalve.com/rest/v1/user_settings?user_id=eq.YOUR_USER_ID' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
-H "Content-Type: application/json" \
-d '{
    "notify_failed_workflows": "true",
}'
```

## Workflows

### Retrieve Workflows

Get workflows using the `/workflows` endpoint:

```bash
curl 'https://api.taskvalve.com/rest/v1/workflows?select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

## Activities

### Retrieve Activities

Fetch a list of activities:

```bash
curl 'https://api.taskvalve.com/rest/v1/activities?select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

## Selecting

### Including

Retrieve only the id and creation time of workflows:

```
curl 'https://api.taskvalve.com/rest/v1/workflows?select=workflow_id,created_at' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

### Excluding

Retrieve activities without the output:

```
curl 'https://api.taskvalve.com/rest/v1/activities?select=-output' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

## Filtering

### eq

Retrieve activities with a specific status:

```bash
curl 'https://api.taskvalve.com/rest/v1/activities?status=eq.failed&select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

### neq

Retrieve workflows excluding a specific status:

```bash
curl 'https://api.taskvalve.com/rest/v1/workflows?status=neq.completed&select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

### gt

Retrieve activities that started after a certain time:

```bash
curl 'https://api.taskvalve.com/rest/v1/activities?start_time=gt.2023-09-01T00:00:00Z&select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

### gte

Retrieve workflows created on or after a certain date:

```bash
curl 'https://api.taskvalve.com/rest/v1/workflows?created_at=gte.2023-09-01T00:00:00Z&select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

### lt

Retrieve activities that ended before a certain time:

```bash
curl 'https://api.taskvalve.com/rest/v1/activities?end_time=lt.2023-09-01T00:00:00Z&select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

### lte

Retrieve workflows created on or before a certain date:

```bash
curl 'https://api.taskvalve.com/rest/v1/workflows?created_at=lte.2023-08-31T00:00:00Z&select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

### like

Search for an activity by name (case-sensitive):

```bash
curl 'https://api.taskvalve.com/rest/v1/activities?name=like.*coding*&select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

### ilike

Search for an activity by name (case-insensitive):

```bash
curl 'https://api.taskvalve.com/rest/v1/activities?name=ilike.*coding*&select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

## Ordering

Order activities by start time in ascending order:

```bash
curl 'https://api.taskvalve.com/rest/v1/activities?order_by=start_time.asc&select=*' \
-H "

apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

## Limit

Limit the number of retrieved activities to 5:

```bash
curl 'https://api.taskvalve.com/rest/v1/activities?limit=5&select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

## Range Limiting

Retrieve activities within a specific range:

```bash
curl 'https://api.taskvalve.com/rest/v1/activities?select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
-H "Range: 0-9"
```

## Retrieve as CSV

Retrieve activities in CSV format:

```bash
curl 'https://api.taskvalve.com/rest/v1/activities?select=*' \
-H "apikey: PUBLIC_API_KEY" \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN"
-H "Accept: text/csv"
```
