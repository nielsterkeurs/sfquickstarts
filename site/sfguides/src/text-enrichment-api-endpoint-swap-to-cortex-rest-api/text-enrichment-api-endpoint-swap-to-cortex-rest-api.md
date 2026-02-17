author: Niels ter Keurs  
id: text-enrichment-api-endpoint-swap-to-cortex-rest-api  
language: en  
summary: Swap an existing Text Enrichment API implementation to use Snowflake Cortex REST API as the backend with minimal changes to your client-facing contract.  
categories: snowflake-site:taxonomy/solution-center/certification/quickstart  
environments: web  
status: Published  
feedback link: https://github.com/Snowflake-Labs/sfguides/issues  
fork repo link: https://github.com/nielsterkeurs/Text-Enrichment-API---Endpoint-Swap-to-Cortex-REST-API  
open in snowflake: <optional – add deeplink into your Snowflake account or demo environment>  

# Text Enrichment API: Endpoint Swap to Cortex REST API

This lab walks you through taking an existing **Text Enrichment API** implementation and swapping its backend endpoint to **Snowflake Cortex REST API**, while keeping the client-facing API as stable as possible.

You will start from the reference implementation in the GitHub repository:

- **Repo**: https://github.com/nielsterkeurs/Text-Enrichment-API---Endpoint-Swap-to-Cortex-REST-API

By the end of the lab you will have a working text enrichment service that calls Cortex REST API for all enrichment logic.

---

## Overview

Use this lab to understand and implement a safe, incremental migration from a legacy text enrichment service to Snowflake Cortex REST API.

The focus is on:

- Identifying the **swap boundary** between your existing enrichment endpoint and Cortex REST API.
- Updating code and configuration at that boundary.
- Preserving your existing **input/output contract** as much as possible.

### Prerequisites

- Familiarity with:
  - REST APIs (HTTP methods, headers, JSON payloads).
  - Basic Snowflake concepts (account, role, warehouse).
  - The primary language and framework used in the lab repository (for example Python / Node.js, depending on your implementation).
- Access to:
  - A **Snowflake account** with **Cortex** features enabled.
  - A role and warehouse that can run Cortex workloads.
  - The GitHub repository:  
    `https://github.com/nielsterkeurs/Text-Enrichment-API---Endpoint-Swap-to-Cortex-REST-API`
- Local tooling:
  - Git installed.
  - A modern code editor such as VS Code.
  - Ability to run the sample service locally (for example via `python`, `npm`, or Docker, as defined in the repo).

### What You’ll Learn

- How to review and understand an existing **Text Enrichment API** implementation.
- How to identify where to **swap** the enrichment backend to Cortex REST API.
- How to configure and call **Cortex REST API** from application code.
- How to normalize Cortex responses so that they match your existing API contract.
- How to test and validate the new integration.

### What You’ll Need

- A [GitHub](https://github.com/) account with access to the lab repository.
- [VS Code](https://code.visualstudio.com/download) or your preferred editor.
- Credentials for:
  - Your Snowflake account (user, password or keypair, role, warehouse).
  - Any auth mechanism used for Cortex REST API in your environment (for example OAuth).
- Optional:
  - An API client such as `curl`, Postman, or a browser extension to exercise the text enrichment endpoint.

### What You’ll Build

By the end of this lab you will have:

- A running **Text Enrichment API** service that:
  - Accepts raw text as input.
  - Calls **Snowflake Cortex REST API** behind the scenes.
  - Returns enriched data (for example entities, topics, summaries, or other derived attributes).
- A minimal, well-documented code change set that you can apply to other services to adopt Cortex REST API.

---

## Step 1 – Clone the Lab and Explore the Project

In this step you will clone the reference repo and explore its structure so you understand where the current enrichment logic lives.

### 1.1 Clone the repository

Clone the lab repo to your local machine:
