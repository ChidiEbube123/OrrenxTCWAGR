# TCWAGR Developer Documentation

Welcome to the official documentation for the **Centralized West-African Gas Repository (TCWAGR)**.

TCWAGR is a centralized platform for accessing official fuel prices published by Oil Marketing Companies (OMCs) and LPG Marketing Companies (LPGMCs) across West Africa. The platform provides both a web interface and a REST API for developers, businesses, researchers, and logistics companies.

---

# Website

**Production**

https://tcwagr.orrenlogistics.com

---

# API Base URL

```
https://tcwagr.orrenlogistics.com/api/v1/
```

---

# Features

* Latest official fuel prices
* Historical fuel prices
* OMC & LPGMC directory
* National pricing windows
* API usage statistics
* API key management
* Subscription upgrade requests

---

# Authentication

All API requests require an API Key.

Pass your key using the Authorization header.

```
Authorization: Bearer YOUR_API_KEY
```

Example:

```http
GET /api/v1/prices/latest/?country=NG&fuel=PMS

Authorization: Bearer sk_live_xxxxxxxxxxxxxxxxx
```

Requests without a valid API key will return:

```json
{
    "detail": "Authentication credentials were not provided."
}
```

---

# Endpoints

---

## Latest Prices

Returns the latest official prices published by OMCs.

**Endpoint**

```
GET /prices/latest/
```

### Parameters

| Name    | Required | Description                                       |
| ------- | -------- | ------------------------------------------------- |
| country | Yes      | ISO 3166-1 Alpha-2 country code                   |
| fuel    | Yes      | PMS, AGO, LPG or ATK                              |
| omc     | No       | Filter by OMC slug                                |
| limit   | No       | Maximum number of results (Default: 50, Max: 200) |

Example

```
GET /prices/latest/?country=NG&fuel=PMS
```

Example cURL

```bash
curl \
-H "Authorization: Bearer YOUR_API_KEY" \
"https://tcwagr.orrenlogistics.com/api/v1/prices/latest/?country=NG&fuel=PMS"
```

---

## Historical Prices

Returns historical fuel prices across pricing windows.

**Endpoint**

```
GET /prices/history/
```

### Parameters

| Name    | Required | Description              |
| ------- | -------- | ------------------------ |
| country | Yes      | Country Code             |
| fuel    | Yes      | Fuel Type                |
| omc     | No       | OMC Slug                 |
| from    | No       | Start date (YYYY-MM-DD)  |
| to      | No       | End date (YYYY-MM-DD)    |
| limit   | No       | Maximum windows returned |

Example

```
GET /prices/history/?country=GH&fuel=PMS&from=2025-01-01&to=2025-06-01
```

---

## OMC Directory

Returns every Oil Marketing Company and LPG Marketing Company currently available.

**Endpoint**

```
GET /omcs/
```

### Parameters

| Name    | Required | Description       |
| ------- | -------- | ----------------- |
| country | No       | Filter by country |

Example

```
GET /omcs/?country=NG
```

---

## Pricing Windows

Returns available pricing windows.

Pricing windows represent official government or regulatory pricing periods.

**Endpoint**

```
GET /windows/
```

### Parameters

| Name    | Required | Description             |
| ------- | -------- | ----------------------- |
| country | No       | Country                 |
| limit   | No       | Maximum number returned |

Example

```
GET /windows/?country=GH
```

---

## Usage Statistics

Returns API usage information for the authenticated account.

**Endpoint**

```
GET /usage/
```

This endpoint can be used to monitor:

* API requests
* Remaining quota
* Subscription usage

---

## API Keys

Manage API keys for your account.

### List Keys

```
GET /keys/
```

---

### Create New Key

```
POST /keys/
```

---

### Revoke Key

```
DELETE /keys/{key_id}/
```

Example

```
DELETE /keys/12/
```

---

## Upgrade Request

Request access to a higher API plan.

```
POST /keys/upgrade/
```

This endpoint notifies the TCWAGR team that your organization would like to upgrade its subscription.

---

# Country Codes

Examples

| Country       | Code |
| ------------- | ---- |
| Nigeria       | NG   |
| Ghana         | GH   |
| Benin         | BJ   |
| Togo          | TG   |
| Côte d'Ivoire | CI   |

---

# Fuel Types

| Fuel | Description               |
| ---- | ------------------------- |
| PMS  | Premium Motor Spirit      |
| AGO  | Automotive Gas Oil        |
| LPG  | Liquefied Petroleum Gas   |
| ATK  | Aviation Turbine Kerosene |

---

# Error Codes

| Status | Meaning               |
| ------ | --------------------- |
| 200    | Success               |
| 400    | Invalid Request       |
| 401    | Authentication Failed |
| 403    | Permission Denied     |
| 404    | Resource Not Found    |
| 429    | Rate Limit Exceeded   |
| 500    | Internal Server Error |

---

# Python Example

```python
import requests

url = "https://tcwagr.orrenlogistics.com/api/v1/prices/latest/"

headers = {
    "Authorization": "Bearer YOUR_API_KEY"
}

params = {
    "country": "NG",
    "fuel": "PMS"
}

response = requests.get(
    url,
    headers=headers,
    params=params
)

print(response.json())
```

---

# JavaScript Example

```javascript
const response = await fetch(
    "https://tcwagr.orrenlogistics.com/api/v1/prices/latest/?country=NG&fuel=PMS",
    {
        headers: {
            Authorization: "Bearer YOUR_API_KEY"
        }
    }
);

const data = await response.json();

console.log(data);
```

---

# Best Practices

* Always authenticate using your API key.
* Cache responses where appropriate to reduce unnecessary requests.
* Use the History endpoint for trend analysis.
* Use the Latest Prices endpoint for real-time dashboards.
* Store API keys securely and never expose them in client-side applications.

---

# Website Guide

The TCWAGR website provides a user-friendly interface for accessing fuel pricing information.

From the dashboard you can:

* View the latest official fuel prices
* Search by country
* Filter by fuel type
* Compare prices across OMCs
* Browse historical pricing windows
* Manage your API keys
* Monitor API usage
* Upgrade your subscription plan

---

# Support

For technical support, feature requests, or partnership enquiries, please contact the TCWAGR team through the contact information available on the website.

---

# License

Copyright © Orren.

All rights reserved.
