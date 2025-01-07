# Device Management API Documentation

## Table of Contents
1. [Overview](#overview)
2. [Base URL](#base-url)
3. [Authentication](#authentication)
4. [Endpoints](#endpoints)
    - [Fetch Device Info](#fetch-device-info)
5. [Request Parameters](#request-parameters)
6. [Response Structure](#response-structure)
    - [Success Response (200)](#success-response-200)
    - [Not Found Response (404)](#not-found-response-404)
    - [Validation Error Response (422)](#validation-error-response-422)
    - [Unauthorized Response (401)](#unauthorized-response-401)
7. [Usage Examples](#usage-examples)

---

## Overview

The **Device Management API** allows clients to retrieve detailed information about devices based on the tenant identifier and the device's serial number

---

## Base URL

https://staging.cms.healthmonitor.com/api/v1/pronto/device

---

## Authentication

The API utilizes **Bearer Token** authentication to secure its endpoints. Each request must include a valid JWT token in the `Authorization` header.

**Authentication Header Format:**

Authorization: Bearer YOUR_BEARER_TOKEN


*Ensure that the Bearer token is valid and has not expired.*

---

## Endpoints

### Fetch Device Info

**Endpoint:**

GET https://staging.cms.healthmonitor.com/api/v1/pronto/device?tenant=tenant_name&serial_number=000000


**Description:**
Retrieves device details based on the provided tenant identifier and device serial number.

---

## Request Parameters

### Body Parameters

| Parameter       | Type   | Required | Description                                                  |
|-----------------|--------|----------|--------------------------------------------------------------|
| `tenant`        | string | Yes      | The tenant name identifier.                                  |
| `serial_number` | string | Yes      | The serial number of the device to retrieve information for. |


**Response Structure**

All responses are in JSON format and follow a standardized structure for consistency and ease of parsing.

### Success Response (200) ###

Description:
The request was successful, and device details have been retrieved.

Response Body:
```json
{
  "status": "SUCCESS 200",
  "message": "Device details retrieved successfully. Used New API",
  "data": {
    "deviceId": "igsseries-909C117810",
    "state": {
      "adbEnabled": false,
      // etc...
      },
      "version": "",
      "volume": 0,
      "webViewVersionCode": 609919301,
      "webViewVersionName": "120.0.6099.193",
      "webViewVersionPackage": "com.google.android.webview",
      "wifiSignal": 4,
      "wifiSsid": "LCR-Guest 2"
    },
    "config": {
      "adbEnabled": false,
      // etc....
    },
    "deviceKey": "5fe203120ced46f3bdb26b8e3dc84db8",
    "name": "Low Country Rheumatology-Summerville : Gary Fink",
    "location": "150212 - Summerville, SC",
    "labelIds": [],
    "playerState": { 
      // Player state Info
    },
    // ... additional device details
    }
}
```

### Not Found Response (404)

Description:
The specified device does not exist in the system.

Response Body:

```json
{
    "status": 404,
    "error": {
      "code": "ERROR 404",
      "message": "Could not find and return device using specified Serial Number",
    }
}
```

### Validation Error Response (422)

Description:
The request failed validation due to missing or invalid parameters.

Response Body:

```json
{
    "status": 422,
    "error": {
        "code": "VALIDATION_ERROR",
        "message": "Validation failed.",
        "details": {
            "serial_number": [
                "The serial_number parameter is required."
            ],
            "tenant": [
                "The tenant name is required."
            ]
        }
    }
}
```

### Unauthorized Response (401)

Description:
Authentication failed due to missing or invalid JWT token.

Response Body:
```json
{
    "status": 401,
    "error": {
        "code": "UNAUTHORIZED",
        "message": "Authentication failed."
    }
}
```

## Usage Examples

https://staging.cms.healthmonitor.com/api/v1/pronto/device?tenant=hm_production&serial_number=909C117810
