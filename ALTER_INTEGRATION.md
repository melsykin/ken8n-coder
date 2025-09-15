# Alter API Integration for ken8n-coder

This guide explains how to integrate Alter's API gateway with ken8n-coder to access multiple AI models through a single API endpoint.

## What is Alter?

[Alter](https://alterhq.com) is an AI assistant that provides an OpenAI-compatible API gateway, allowing you to access multiple AI providers (OpenAI, Anthropic, Google, etc.) through a single endpoint with centralized billing.

## Setup Instructions

### 1. Get Your Alter API Key

1. Install and set up Alter on your Mac
2. Go to **Settings > Router** in Alter
3. Generate your API key
4. Copy the endpoint URL: `https://alterhq.com/api`

### 2. Add Alter Credentials to ken8n-coder

Run the following command to add your Alter API key:

```bash
ken8n-coder-dev auth login
```

1. Select **Other** from the provider list
2. Enter `alter` as the provider ID
3. Enter your Alter API key when prompted

### 3. Configure Alter in ken8n-coder

Create a `ken8n-coder.json` file in your project directory with the following configuration:

```json
{
  "$schema": "https://ken8n-coder.ai/config.json",
  "provider": {
    "alter": {
      "options": {
        "baseURL": "https://alterhq.com/api"
      }
    }
  },
  "models": {
    "alter": {
      "OpenAI#gpt-4o-mini": {
        "maxTokens": 128000
      },
      "OpenAI#gpt-4o": {
        "maxTokens": 128000
      },
      "Claude#Claude-3-5-Sonnet-20240620": {
        "maxTokens": 200000
      },
      "Claude#Claude-3-5-Sonnet-latest": {
        "maxTokens": 200000
      },
      "Gemini#gemini-1.5-pro": {
        "maxTokens": 1000000
      },
      "Gemini#gemini-1.5-flash": {
        "maxTokens": 1000000
      }
    }
  }
}
```

### 4. Available Models

Alter supports models from multiple providers using the format `Provider#Model-name`:

#### OpenAI Models
- `OpenAI#gpt-4o-mini`
- `OpenAI#gpt-4o`
- `OpenAI#gpt-4-turbo`

#### Anthropic Models
- `Claude#Claude-3-5-Sonnet-20240620`
- `Claude#Claude-3-5-Sonnet-latest`
- `Claude#Claude-3-7-Sonnet-latest`

#### Google Models
- `Gemini#gemini-1.5-pro`
- `Gemini#gemini-1.5-flash`
- `Gemini#gemini-2.0-flash-001`

#### Other Providers
- `Mistral#mistral-large-latest`
- And many more...

### 5. Usage

Once configured, you can use Alter models in ken8n-coder by specifying the full model name:

```bash
ken8n-coder-dev run --model "OpenAI#gpt-4o-mini" "Write a hello world program"
```

## Benefits

- **Centralized Billing**: Pay for all models through your Alter account
- **Single API Key**: No need to manage multiple provider API keys
- **Model Switching**: Easy access to models from different providers
- **Cost Management**: Alter provides usage tracking and cost controls

## Troubleshooting

### Models Not Listed
If your application doesn't automatically list available models, manually specify the model using the `Provider#Model-name` format.

### Authentication Errors
- Verify your API key is correctly entered
- Ensure you're using the correct endpoint URL: `https://alterhq.com/api`
- Check that your Alter account is active and in good standing

### Connection Issues
- Check if the application supports OpenAI-compatible endpoints
- Ensure you're using the latest version of ken8n-coder

## More Information

- [Alter Documentation](https://alterhq.com/docs#api-gateway)
- [Alter API Gateway Overview](https://alterhq.com/docs#api-gateway)
- [Model Naming Convention](https://alterhq.com/docs#model-naming-convention)
