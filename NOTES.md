

```markdown
# 🚀 JsonPowerDB - Complete Guide

<p align="center">
  <img src="https://github.com/user-attachments/assets/32902351-d8e2-4165-bc63-cd2edbd0f5fd" alt="JsonPowerDB Dashboard" width="800"/>
</p>

![JPDB](https://img.shields.io/badge/Database-JsonPowerDB-blue.svg)
![REST API](https://img.shields.io/badge/API-REST-green.svg)
![Serverless](https://img.shields.io/badge/Architecture-Serverless-orange.svg)
![Real-time](https://img.shields.io/badge/Performance-Real--time-red.svg)

---

## 📖 What is JsonPowerDB?

**JsonPowerDB (JPDB)** is a **real-time, high-performance, lightweight, serverless** database management system designed for modern application development [web:18][web:45]. It eliminates the complexity of traditional database setup and management, allowing developers to build applications faster with minimal configuration.

### 🎯 Core Features

- **Multi-Mode DBMS**: Functions as Document DB, RDBMS, Key-Value DB, GeoSpatial DB, and Time-Series DB [web:18]
- **REST API Based**: Simple HTTP interfaces for all database operations [web:5]
- **JSON-Centric**: Native JSON data storage and manipulation [web:3]
- **Serverless Architecture**: No installation, configuration, or server management required [web:46]
- **Real-Time Analytics**: Best suited for real-time application data analytics [web:50]
- **High Performance**: Proprietary PowerIndeX algorithm delivers blazing-fast operations [web:18]

<p align="center">
  <img src="https://github.com/user-attachments/assets/ef5a1f05-ae68-4f14-ab03-9b969826bfd6" alt="JsonPowerDB Features" width="800"/>
</p>

---

## 🛠️ JPDB Commons JS Library

### Overview

To make JsonPowerDB integration even **easier and faster**, developers can use the **jpdb-commons.js** JavaScript library [web:14]. This library provides pre-built functions for common database operations, eliminating the need to manually construct JSON requests.

### 📥 Installation

Include the library in your HTML file:

```html
<script src="https://login2explore.com/jpdb/resources/js/0.0.4/jpdb-commons.js"></script>
```

**Documentation**: [JPDB Commons JS - JavaScript Library for Developers](https://careers.login2explore.com/mod/page/view.php?id=136)

### 🔧 Available Helper Functions

The library provides simplified functions for creating JPDB requests [web:14]:

#### Create Requests

| Function | Purpose | Usage |
|----------|---------|-------|
| `createGET_BY_KEYRequest()` | Retrieve record by key | `createGET_BY_KEYRequest(token, dbName, relName, jsonObj)` |
| `createPUTRequest()` | Insert single record | `createPUTRequest(token, jsonObj, dbName, relName)` |
| `createUPDATERecordRequest()` | Update existing record | `createUPDATERecordRequest(token, jsonObj, dbName, relName, recNo)` |
| `createREMOVERecordRequest()` | Delete record | `createREMOVERecordRequest(token, dbName, relName, recNo)` |

#### Execute Commands

```javascript
// Execute at given base URL
executeCommandAtGivenBaseUrl(reqString, baseUrl, endpoint);

// Execute command (uses default base URL)
executeCommand(reqString, endpoint);
```

### 💡 Example Usage

**Without jpdb-commons.js (Manual approach):**
```javascript
const request = {
    token: "your-token",
    cmd: "GET_BY_KEY",
    dbName: "Student",
    rel: "Student-Rel",
    jsonStr: {
        "id": "1"
    }
};
```

**With jpdb-commons.js (Simplified approach):**
```javascript
const request = createGET_BY_KEYRequest(
    token, 
    "Student", 
    "Student-Rel", 
    { "id": "1" }
);
```

**Benefits**: Less code, fewer errors, faster development [web:14][web:2].

---

## 📡 API Reference

### Base Configuration

| Parameter | Value |
|-----------|-------|
| **HTTP Method** | `POST` |
| **Base URL** | `http://api.login2explore.com:5577` |
| **IML Endpoint** | `/api/iml` (Insert, Update, Delete) |
| **IRL Endpoint** | `/api/irl` (Retrieve) |

---

## 📝 IML Commands (Index Manipulation Language)

*For Insert, Update, and Delete operations*

### 1️⃣ PUT - Insert Single Record

**Purpose**: Insert a single record into the database

**Request Structure**:
```json
{
    "token": "<connection-token>",
    "cmd": "PUT",
    "dbName": "<database-name>",
    "rel": "<relation-name>",
    "colsAutoIndex": <boolean>,  // Optional: auto-index new columns (default: true)
    "templateStr": <json-template>,  // Optional
    "jsonStr": <json-data>
}
```

**Example**:
```json
{
    "token": "-1935843913|3223940520357615501|-1935843909",
    "cmd": "PUT",
    "dbName": "Student",
    "rel": "Student-Rel",
    "jsonStr": {
        "id": "1",
        "name": "Soniya",
        "email": "soniya@gmail.com",
        "mobileno": "9967825671"
    }
}
```

---

### 2️⃣ PUT_ALL - Insert Multiple Records

**Purpose**: Insert multiple records in a single request

**Use Case**: Bulk data import, batch processing

---

### 3️⃣ UPDATE - Update Records

**Purpose**: Update multiple records or add new columns to existing records

**Use Case**: Modify student information, add new fields to existing data

---

### 4️⃣ SET - Insert or Update

**Purpose**: Insert new record OR update existing record based on primary key

**Behavior**: Smart operation that checks if record exists before deciding action

---

### 5️⃣ SET_ALL - Bulk Insert/Update

**Purpose**: Insert and update multiple records based on primary key

**Use Case**: Synchronizing data from external sources

---

### 6️⃣ REMOVE - Delete Records

**Purpose**: Remove records from the database

**Use Case**: Delete graduated students, archive old data

---

## 🔍 IRL Commands (Index Retrieval Language)

*For Retrieve operations*

### 1️⃣ GET_BY_KEY - Retrieve by Indexed Column ⭐

**Purpose**: Retrieve single record using indexed column value

**Request Structure**:
```json
{
    "token": "<connection-token>",
    "cmd": "GET_BY_KEY",
    "dbName": "<database-name>",
    "rel": "<relation-name>",
    "createTime": <boolean>,  // Optional: include creation timestamp
    "updateTime": <boolean>,  // Optional: include update timestamp
    "jsonStr": {
        "<column-name>": "<column-value>"
    }
}
```

**Important Notes**:
- ✅ Works **only with indexed columns**
- ✅ Returns **first matching record**
- ✅ Replaces deprecated `GET` command

**Example**:
```json
{
    "token": "your-token",
    "cmd": "GET_BY_KEY",
    "dbName": "Student",
    "rel": "Student-Rel",
    "jsonStr": {
        "id": "1"
    }
}
```

**Using jpdb-commons.js**:
```javascript
const request = createGET_BY_KEYRequest(
    token,
    "Student",
    "Student-Rel",
    { "id": "1" }
);
```

---

### 2️⃣ GET_BY_RECORD - Retrieve by Record Number

**Purpose**: Retrieve single record using its unique record number

**Request Structure**:
```json
{
    "token": "<connection-token>",
    "cmd": "GET_BY_RECORD",
    "dbName": "<database-name>",
    "rel": "<relation-name>",
    "record": <record-number>,
    "createTime": <boolean>,  // Optional
    "updateTime": <boolean>   // Optional
}
```

**Use Case**: Update operations where you know the record number from previous GET operation

---

### ⚠️ Deprecated Commands

| Command | Status | Replacement |
|---------|--------|-------------|
| `GET` | ❌ Deprecated | Use `GET_BY_KEY` instead |

**Migration**: Replace all `GET` commands with `GET_BY_KEY` for better performance and clarity [web:3].

---

## 📚 Complete Command Reference

### IML Commands Summary

| Command | Operation | Records Affected | Primary Use |
|---------|-----------|------------------|-------------|
| `PUT` | Insert | Single | Add new student |
| `PUT_ALL` | Insert | Multiple | Bulk enrollment |
| `UPDATE` | Modify | Multiple | Update student info |
| `SET` | Insert/Update | Single | Smart save |
| `SET_ALL` | Insert/Update | Multiple | Sync data |
| `REMOVE` | Delete | Multiple | Remove records |

### IRL Commands Summary

| Command | Operation | Returns | Index Required |
|---------|-----------|---------|----------------|
| `GET_BY_KEY` | Retrieve | First match | ✅ Yes |
| `GET_BY_RECORD` | Retrieve | Exact record | ❌ No |

---

## 🎓 Learning Resources

### Official Documentation
- 📖 [Complete JPDB Documentation](http://login2explore.com/jpdb/docs.html)
- 🔧 [JPDB Command Reference](http://login2explore.com/jpdb/docs.html#jpdb-command-request)
- 💻 [JPDB Commons JS Library Guide](https://careers.login2explore.com/mod/page/view.php?id=136)

### Quick Links
- 🌐 [Login2Xplore Platform](https://login2explore.com)
- 🔑 [Get Your API Token](http://api.login2explore.com:5577)
- 💬 [Community Support](https://login2xplore.com/ask/)

---

## 🚀 Quick Start Guide

1. **Register** at [JsonPowerDB](http://api.login2explore.com:5577/user/register_dev.html)
2. **Generate** your connection token
3. **Include** jpdb-commons.js in your project
4. **Start coding** with simplified API calls!

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://login2explore.com/jpdb/resources/js/0.0.4/jpdb-commons.js"></script>
</head>
<body>
    <script>
        const token = "YOUR-TOKEN-HERE";
        const request = createPUTRequest(
            token,
            { name: "John", age: 25 },
            "TestDB",
            "Users"
        );
        // Execute request...
    </script>
</body>
</html>
```

---

## 💡 Best Practices

✅ **DO**:
- Use `GET_BY_KEY` instead of deprecated `GET`
- Include jpdb-commons.js for easier development
- Index frequently queried columns
- Use `SET` for insert-or-update operations

❌ **DON'T**:
- Use deprecated `GET` command
- Hardcode tokens in public repositories
- Skip error handling in AJAX calls

---

## 📞 Support

- 📧 **Email**: support@login2explore.com
- 💬 **Community Forum**: [Login2Xplore Ask](https://login2xplore.com/ask/)
- 📺 **YouTube Tutorials**: [Login2Xplore Channel](https://www.youtube.com/channel/UCKTwUS9bXqEJnN-TLYje1Sg)

---

<p align="center">
  <strong>⭐ Start building real-time applications with JsonPowerDB today! ⭐</strong>
</p>
```

This enhanced version includes:
- ✨ Professional badges and icons
- 📊 Well-organized tables for better readability
- 🎨 Proper code syntax highlighting
- 📝 Clear section headers with emojis
- 💡 Comprehensive jpdb-commons.js information
- 🔗 All relevant links and resources
- 📚 Learning resources section
- ⚡ Quick start guide
- ✅ Best practices section

The markdown is now much more visually appealing and easier to navigate![1][2][3][4]

[1](https://github.com/MandeepDalavi/JsonPowerDB)
[2](https://www.youtube.com/watch?v=eMBDrrZ0I1Y)
[3](https://github.com/Bhavitejareddy/Login2exploreinternship)
[4](https://www.linkedin.com/pulse/feature-jsonpowerdb-vishwajeet-kumar)
