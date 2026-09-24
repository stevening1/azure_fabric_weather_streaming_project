# Azure & Microsoft Fabric Real-Time Weather Streaming Project

## Overview

An end-to-end real-time weather streaming solution that ingests the
latest weather data for Johannesburg and delivers it to an interactive
Power BI dashboard. The solution combines Azure services and Microsoft
Fabric to demonstrate real-time data ingestion, streaming analytics,
dashboarding, and event-driven alerting.

The pipeline also includes automated email alerts for severe weather
conditions, providing a practical example of how real-time data can be
transformed into actionable insights.

## Problem

The requirement was to build a solution capable of continuously
ingesting the latest Johannesburg weather information and presenting a
detailed, up-to-date weather summary in a business-friendly dashboard.

## Solution

Weather data is retrieved from WeatherAPI.com using both a Databricks
notebook and an Azure Functions Python application. The data is
published to Azure Event Hubs, providing a scalable streaming ingestion
layer.

Microsoft Fabric Eventstream consumes the Event Hub stream and writes
the incoming weather data to a KQL table within a Fabric Eventhouse (KQL
database). Power BI connects to the resulting dataset to provide an
up-to-date weather overview.

For proactive monitoring, a KQL query identifies severe weather
conditions. Fabric Activator monitors the relevant event and triggers an
email notification when an alert condition is detected.

### End-to-End Flow

**WeatherAPI.com → Databricks / Azure Functions → Azure Event Hubs →
Fabric Eventstream → Fabric Eventhouse / KQL → Power BI**

**Severe weather path:** KQL query → Fabric Activator → Email alert

## Technology Stack

-   **Languages:** Python, KQL
-   **Data Engineering:** PySpark, Databricks
-   **Development:** VS Code
-   **Azure:** Azure Functions, Azure Event Hubs, Azure Key Vault
-   **Microsoft Fabric:** Eventstream, Eventhouse (KQL database),
    Activator
-   **Analytics & Visualisation:** Power BI
-   **Data Source:** WeatherAPI.com

## Architecture

![Architecture Diagram](Architecture%20Diagram.png)

The solution retrieves the latest weather data from WeatherAPI.com
through API calls implemented in a Databricks notebook and an Azure
Functions Python application.

The weather data is temporarily streamed through Azure Event Hubs. A
Microsoft Fabric Eventstream consumes the Event Hub stream and persists
the incoming data in a KQL table within a Fabric Eventhouse KQL
database.

Power BI uses the KQL data to present the latest Johannesburg weather
information and recent weather trends.

A KQL query evaluates incoming weather data for severe weather
conditions. When an alert condition is identified, Fabric Activator
triggers an automated email warning.

## Databricks vs Azure Functions Cost Analysis

Weather data ingestion was implemented using both Databricks and Azure
Functions to gain practical experience with two different Azure-based
approaches.

Azure Cost Management was used to investigate the relative cost of the
two implementations. The analysis indicated that Azure Functions was the
more cost-effective option for this workload, particularly because the
first 1 million executions are included at no charge under the
applicable consumption-based offering.

Azure Functions was also a good architectural fit because this use case
involves relatively lightweight API ingestion without significant
aggregation or complex data transformation requirements.

The comparison provided practical experience in evaluating not only
technical implementation options, but also the cost and architectural
trade-offs associated with each approach.

## Power BI Real-Time Weather Overview

![Power BI Weather Dashboard](Weather%20Dashboard.png)

The Power BI dashboard provides a concise overview of the latest
Johannesburg weather conditions, including:

-   Latest data refresh time
-   Severe weather alerts, when applicable
-   Air quality
-   Current conditions, such as sunny or overcast
-   Temperature
-   Feels-like temperature
-   UV index
-   Humidity
-   Wind speed
-   Recent weather trends
-   Three-day weather forecast

The dashboard is designed to provide a clear, business-friendly view of
current weather conditions while demonstrating how streaming data can be
transformed into actionable visual insights.

## Security

Security was considered throughout the solution design.

-   API keys and shared access connection strings are stored securely
    using **Azure Key Vault**.
-   **Managed identities** are used where supported to reduce the need
    for credentials in application code.
-   Access is assigned using **role-based access control (RBAC)** and
    the principle of least privilege.
-   Sensitive configuration is kept separate from application source
    code wherever possible.

## Key Project Outcomes

This project demonstrates practical experience across the modern Azure
and Microsoft Fabric data ecosystem, including:

-   Designing an end-to-end real-time streaming architecture
-   Building Python-based API ingestion solutions
-   Working with Databricks and PySpark
-   Implementing Azure Functions for serverless data ingestion
-   Publishing streaming data through Azure Event Hubs
-   Building streaming pipelines with Microsoft Fabric Eventstream
-   Storing and querying streaming data using KQL and Fabric Eventhouse
-   Developing Power BI dashboards for operational reporting
-   Implementing event-driven alerting with Fabric Activator
-   Evaluating cloud solution costs using Azure Cost Management
-   Applying cloud security principles including Key Vault, managed
    identities, RBAC, and least-privilege access
