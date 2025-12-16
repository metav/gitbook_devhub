# Datahub Endpoints

These are the APIs provided by **OORT Datahub** for your plugin to call. Use these to report status, upload results, and manage file transfers.

## Base URL
`https://datahub.oortech.com` (Production)

---

## File Operations

### 1. Initialize Upload
**POST** `/api/task/upload/init`

Request a presigned URL to upload a file (e.g., task results).

#### Request Body
```json
{
  "task_id": "task_abc123",
  "filename": "result.zip",
  "file_size": 1048576
}
```

#### Response
Returns a `upload_url` and `file_id`.

### 2. Complete Upload
**POST** `/api/task/upload/complete`

Notify Datahub that the file upload to the presigned URL is finished.

#### Request Body
```json
{
  "task_id": "task_abc123",
  "file_id": "file_xyz789",
  "status": "success"
}
```

### 3. Get Download URL
**GET** `/api/task/download/presign`

Get a temporary URL to download a task input or resource file.

#### Parameters
*   `file_id`: The ID of the file to download.

---

## Task Management

### 4. Update Task Status
**POST** `/api/task/update_status`

Report the current status of a task.

#### Request Body
```json
{
  "task_id": "task_abc123",
  "status": "RUNNING",
  "progress": 50,
  "message": "Processing data..."
}
```

### 5. Task Heartbeat
**POST** `/api/task/heartbeat`

Send periodic heartbeats for long-running tasks to prevent timeouts.

#### Request Body
```json
{
  "task_id": "task_abc123"
}
```

### 6. Report Task Result
**POST** `/api/task/result`

Submit the final result of a task.

#### Request Body
```json
{
  "task_id": "task_abc123",
  "result_data": { ... },
  "file_ids": ["file_xyz789"]
}
```

### 7. Notify / Query
**GET** `/api/task/notify`

Long-polling endpoint to check for updates or configuration changes for a task.
