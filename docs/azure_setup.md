# Azure Setup Guide

## Overview
This document describes the Azure resources and setup required for the Olist Data Warehouse project.

## Prerequisites
- Azure subscription
- Azure CLI installed
- Appropriate permissions to create resources

## Azure Resources

### 1. Resource Group
Create a resource group to contain all project resources:

```bash
az group create --name rg-olist-datawarehouse --location eastus
```

### 2. Azure Blob Storage
Create a storage account for the Bronze layer:

```bash
az storage account create \
  --name stolistdatawarehouse \
  --resource-group rg-olist-datawarehouse \
  --location eastus \
  --sku Standard_LRS \
  --kind StorageV2
```

Create containers for each data layer:
- `bronze` - Raw data from Kaggle CSV files
- `silver` - Cleaned and validated data
- `gold` - Aggregated business-ready data

### 3. Azure Data Factory
Create an Azure Data Factory instance for data ingestion and orchestration:

```bash
az datafactory create \
  --resource-group rg-olist-datawarehouse \
  --factory-name adf-olist-datawarehouse \
  --location eastus
```

### 4. Azure Synapse Analytics
Create a Synapse workspace for data transformation and analytics:

```bash
az synapse workspace create \
  --name synapse-olist-datawarehouse \
  --resource-group rg-olist-datawarehouse \
  --storage-account stolistdatawarehouse \
  --file-system synapse \
  --sql-admin-login-user sqladmin \
  --sql-admin-login-password <your-secure-password> \
  --location eastus
```

## Configuration

### Linked Services
Configure the following linked services in Azure Data Factory:
1. **Azure Blob Storage** - Connection to storage account
2. **Azure Synapse** - Connection to Synapse workspace

### Datasets
Create datasets for:
1. Source CSV files (Bronze layer)
2. Parquet files (Silver/Gold layers)
3. Synapse tables

### Security
1. Enable managed identity for ADF
2. Grant appropriate RBAC roles
3. Configure firewall rules
4. Enable encryption at rest

## Monitoring
- Enable diagnostic logging
- Set up Azure Monitor alerts
- Configure Log Analytics workspace
