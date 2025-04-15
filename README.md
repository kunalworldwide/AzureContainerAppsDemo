# Beautiful Quotes App

A simple web application that displays random inspirational quotes with a beautiful animated background. Users can change the color theme, toggle emoji mode, and share quotes on social media.


## Features

- Dynamic animated background with customizable color themes
- Random inspirational quotes from an API
- Share quotes on Twitter/X
- Copy quotes to clipboard
- Auto-refresh quotes option
- Emoji mode for a fun experience

## Running Locally

### Prerequisites

- [Docker](https://www.docker.com/get-started) installed on your machine

### Steps to Run Locally

1. Clone this repository or navigate to the project directory
2. Build the Docker image:
   ```bash
   docker build -t beautiful-quotes-app:local .
   ```
3. Run the Docker container:
   ```bash
   docker run -d -p 8080:80 beautiful-quotes-app:local
   ```
4. Open your browser and navigate to [http://localhost:8080](http://localhost:8080)

## Deploying to Azure Container Apps

### Prerequisites

- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) installed
- An active Azure subscription

### Step 1: Install the Container Apps extension for Azure CLI

```bash
# Bash
az extension add --name containerapp --debug
```

```powershell
# PowerShell
az extension add --name containerapp --debug
```

### Step 2: Log in to Azure

```bash
# Bash
az login --use-device-code
```

```powershell
# PowerShell
az login --use-device-code
```

### Step 3: Set your subscription

```bash
# Bash
az account set --subscription "<your-subscription-id>"
```

```powershell
# PowerShell
az account set --subscription "<your-subscription-id>"
```

### Step 4: Create a Resource Group

```bash
# Bash
az group create --name quotes-app-rg --location centralindia
```

```powershell
# PowerShell
az group create --name quotes-app-rg --location centralindia
```

### Step 5: Register the required provider

```bash
# Bash
az provider register -n Microsoft.OperationalInsights --wait
```

```powershell
# PowerShell
az provider register -n Microsoft.OperationalInsights --wait
```

### Step 6: Create Container Apps Environment

```bash
# Bash
az containerapp env create --name quotes-app-env --resource-group quotes-app-rg --location centralindia
```

```powershell
# PowerShell
az containerapp env create --name quotes-app-env --resource-group quotes-app-rg --location centralindia
```

### Step 7: Create the Container App (Basic Version)

```bash
# Bash
az containerapp create \
  --name beautiful-quotes-app \
  --resource-group quotes-app-rg \
  --environment quotes-app-env \
  --image kunalondock/beautiful-quotes-app:v1 \
  --target-port 80 \
  --ingress external \
  --query properties.configuration.ingress.fqdn
```

```powershell
# PowerShell
az containerapp create `
  --name beautiful-quotes-app `
  --resource-group quotes-app-rg `
  --environment quotes-app-env `
  --image kunalondock/beautiful-quotes-app:v1 `
  --target-port 80 `
  --ingress external `
  --query properties.configuration.ingress.fqdn
```

The command will output the fully qualified domain name (FQDN) of your deployed app, which you can use to access the application.

### Step 8: Create the Container App with Auto-scaling (Advanced Version)

```bash
# Bash
az containerapp create \
  --name beautiful-quotes-app \
  --resource-group quotes-app-rg \
  --environment quotes-app-env \
  --image kunalondock/beautiful-quotes-app:v1 \
  --min-replicas 0 \
  --max-replicas 5 \
  --scale-rule-name azure-http-rule \
  --scale-rule-type http \
  --scale-rule-http-concurrency 3 \
  --target-port 80 \
  --ingress external \
  --query properties.configuration.ingress.fqdn
```

```powershell
# PowerShell
az containerapp create `
  --name beautiful-quotes-app `
  --resource-group quotes-app-rg `
  --environment quotes-app-env `
  --image kunalondock/beautiful-quotes-app:v1 `
  --min-replicas 0 `
  --max-replicas 5 `
  --scale-rule-name azure-http-rule `
  --scale-rule-type http `
  --scale-rule-http-concurrency 3 `
  --target-port 80 `
  --ingress external `
  --query properties.configuration.ingress.fqdn
```

This deployment includes:
- Auto-scaling from 0 to 5 replicas
- HTTP scaling rule with concurrency of 3
- External ingress for public access

### Step 9: View the Container App Logs

```bash
# Bash
az containerapp logs show --name beautiful-quotes-app --resource-group quotes-app-rg
```

```powershell
# PowerShell
az containerapp logs show --name beautiful-quotes-app --resource-group quotes-app-rg
```

## Additional Commands

### View all your Azure subscriptions
```bash
# Bash
az account list --output table
```

```powershell
# PowerShell
az account list --output table
```

### Delete the Container App
```bash
# Bash
az containerapp delete --name beautiful-quotes-app --resource-group quotes-app-rg
```

```powershell
# PowerShell
az containerapp delete --name beautiful-quotes-app --resource-group quotes-app-rg
```

### Delete the Resource Group (to clean up all resources)
```bash
# Bash
az group delete --name quotes-app-rg
```

```powershell
# PowerShell
az group delete --name quotes-app-rg
```

## Building Your Own Version

To build and deploy your own version of this app:

1. Modify the index.html file as needed
2. Build your Docker image:
   ```bash
   # Bash
   docker build -t your-username/beautiful-quotes-app:v1 .
   ```
   
   ```powershell
   # PowerShell
   docker build -t your-username/beautiful-quotes-app:v1 .
   ```
3. Push to Docker Hub:
   ```bash
   # Bash
   docker login
   docker push your-username/beautiful-quotes-app:v1
   ```
   
   ```powershell
   # PowerShell
   docker login
   docker push your-username/beautiful-quotes-app:v1
   ```
4. Deploy using the Azure CLI commands above, replacing the image name with your own

## Credits

Developed by Kunal Das - [Profile Links](https://heylink.me/kunaldas/)
