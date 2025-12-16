# Plugin Endpoints

These are the APIs that **your plugin must implement**. OORT Datahub will call these endpoints to manage tasks and services.

## Base URL
The base URL for these endpoints is configured when you register your plugin (e.g., `https://my-plugin.com`).

---

## 1. Payment Validation (Optional)
**POST** `/api/plugin/payment`

Validates user payment for a service.

### Request Body
```json
{
  "user_address": "0x123...",
  "service_id": "service_123",
  "payment_details": { ... }
}
```

---

## 2. Create Task
**POST** `/api/plugin/create_task`

Initiates a new task in your plugin.

### Request Body
```json
{
  "project_id": "proj_001",
  "task_id": "task_abc123",
  "user_address": "0xUserWallet",
  "task_config": {
    "key": "value",
    "params": "..."
  }
}
```

### Response
```json
{
  "code": 200,
  "msg": "Task created",
  "data": {
    "task_id": "task_abc123"
  }
}
```

---

## 3. Manage Task
**POST** `/api/plugin/manage_task`

Control the lifecycle of a task (Pause, Resume, Cancel).

### Request Body
```json
{
  "task_id": "task_abc123",
  "action": "PAUSE" 
}
```
*   `action`: Can be `PAUSE`, `RESUME`, or `CANCEL`.

---

## 4. Health Check
**GET** `/api/plugin/health`

Used by Datahub to check if your plugin is online.

### Response
```json
{
  "status": "up",
  "version": "1.0.0"
}
```
