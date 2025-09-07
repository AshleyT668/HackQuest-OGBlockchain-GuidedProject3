<<<<<<< HEAD
# HackQuest-OGBlockchain-GuidedProject3
=======
# 0G Compute TypeScript SDK Starter Kit

A comprehensive REST API implementation for interacting with the 0G Compute Network using TypeScript. This starter kit demonstrates how to integrate decentralized AI services with automatic payment processing, TEE verification, and seamless wallet management.

## 🌟 Features

- **REST API Server** with Express.js and TypeScript
- **Swagger Documentation** at `/docs` for interactive API testing
- **🤖 Web Chat Interface** at `/chat` for easy AI conversations
- **Official 0G AI Services** with verified provider addresses
- **Automatic Ledger Management** with startup initialization
- **TEE Verification** for enhanced trust and security
- **Single-use Authentication** headers for secure requests
- **Comprehensive Test Script** for learning and debugging
- **BigInt Serialization** for blockchain data compatibility
- **Enhanced Error Handling** with troubleshooting guidance

## 🤖 Official 0G AI Services

The starter kit includes pre-configured access to official 0G AI services:

| Model | Provider Address | Description | Verification |
|-------|-----------------|-------------|-------------|
| **llama-3.3-70b-instruct** | `0xf07240Efa67755B5311bc75784a061eDB47165Dd` | State-of-the-art 70B parameter model for general AI tasks | TEE (TeeML) |
| **deepseek-r1-70b** | `0x3feE5a4dd5FDb8a32dDA97Bed899830605dBD9D3` | Advanced reasoning model optimized for complex problem solving | TEE (TeeML) |

## 📁 Repository Structure

```
0g-compute-starter-kit/
├── src/
│   ├── config/
│   │   └── swagger.ts           # Swagger/OpenAPI configuration
│   ├── controllers/
│   │   ├── accountController.ts # Account management endpoints
│   │   └── serviceController.ts # AI service endpoints
│   ├── routes/
│   │   ├── accountRoutes.ts     # Account route definitions
│   │   └── serviceRoutes.ts     # Service route definitions
│   ├── services/
│   │   └── brokerService.ts     # Core 0G broker integration
│   ├── index.ts                 # Express app entry point
│   └── startup.ts               # Application initialization
├── public/
│   └── index.html               # Web chat interface
├── demo-compute-flow.ts         # Comprehensive demo script
├── DEMO_SCRIPT.md              # Demo script documentation
├── package.json                # Project configuration
├── tsconfig.json               # TypeScript configuration
└── README.md                   # This file
```

## 🚀 Quick Start

### Prerequisites

1. **Node.js** 16+ and npm
2. **Testnet ETH** for transactions ([Get from faucet](https://faucet.0g.ai))
3. **Ethereum wallet** with private key

### Installation

1. **Clone the repository:**
```bash
git clone https://github.com/yourusername/0g-compute-starter-kit.git
cd 0g-compute-starter-kit
```

2. **Install dependencies:**
```bash
npm install
```

3. **Set up environment variables:**
```bash
# Create .env file
cp .env.example .env  # if available, or create manually
```

Add your configuration to `.env`:
```env
PRIVATE_KEY=your_private_key_here_without_0x_prefix
PORT=4000
NODE_ENV=development
```

4. **Build the project:**
```bash
npm run build
```

5. **Start the server:**
```bash
npm start
```

6. **Access the API:**
- **REST API**: http://localhost:4000
- **Swagger UI**: http://localhost:4000/docs
- **Web Chat Interface**: http://localhost:4000/chat

## 🤖 Web Chat Interface

The starter kit includes a **Web Chat Interface** that provides an easy way to interact with 0G AI services:

### Features
- **Provider Selection**: Choose from available AI service providers
- **Real-time Chat**: Natural language conversation with AI models
- **Automatic Connection**: One-click provider acknowledgment
- **Status Monitoring**: Real-time connection and response status
- **Error Handling**: Friendly error messages and troubleshooting

### Usage
1. **Select Provider**: Choose an AI service provider from the list
2. **Connect**: Click "Select This Provider" to establish connection
![Provider Selection](img/provider.png)
3. **Start Chat**: Begin your conversation with the AI
![Chat With 0G](img/chat.png)
4. **Monitor Status**: Watch the status bar for connection and response updates

### Supported Models
- **Llama 3.3 70B**: General-purpose AI model
- **DeepSeek R1 70B**: Advanced reasoning model
- **Llama 3.1 8B**: Lightweight instruction model

The chat interface automatically handles provider acknowledgment, payment processing, and response verification.

## 🧪 Run the Complete Flow

Run the comprehensive demo script to see the entire 0G compute workflow:

```bash
npm run demo
```

This script demonstrates:
- Wallet and broker initialization
- Ledger account setup with funding
- Service discovery and provider acknowledgment
- AI query submission with payment processing
- TEE verification and cost tracking

See [DEMO_SCRIPT.md](./DEMO_SCRIPT.md) for detailed documentation.

## 📚 API Endpoints

### Account Management

#### `GET /api/account/info`
Get current account information and ledger balance.

**Response:**
```json
{
  "success": true,
  "accountInfo": {
    "ledgerInfo": ["balance_in_wei"],
    "infers": [],
    "fines": []
  }
}
```

#### `POST /api/account/deposit`
Deposit funds to your ledger account.

**Request:**
```json
{
  "amount": 0.1
}
```

**Response:**
```json
{
  "success": true,
  "message": "Deposit successful"
}
```

#### `POST /api/account/refund`
Request refund for unused funds.

**Request:**
```json
{
  "amount": 0.05
}
```

### AI Services

#### `GET /api/services/list`
List all available AI services with pricing and verification status.

**Response:**
```json
{
  "success": true,
  "services": [
    {
      "provider": "0xf07240Efa67755B5311bc75784a061eDB47165Dd",
      "model": "llama-3.3-70b-instruct",
      "serviceType": "inference",
      "url": "https://...",
      "inputPrice": "1000000000000000",
      "outputPrice": "2000000000000000",
      "verifiability": "TeeML",
      "isOfficial": true,
      "isVerifiable": true
    }
  ]
}
```

#### `POST /api/services/acknowledge-provider`
Acknowledge a provider before using their services (required once per provider).

**Request:**
```json
{
  "providerAddress": "0xf07240Efa67755B5311bc75784a061eDB47165Dd"
}
```

#### `POST /api/services/query`
Send a query to an AI service.

**Request:**
```json
{
  "providerAddress": "0xf07240Efa67755B5311bc75784a061eDB47165Dd",
  "query": "What is the capital of France?",
  "fallbackFee": 0.01
}
```

**Response:**
```json
{
  "success": true,
  "response": {
    "content": "The capital of France is Paris.",
    "metadata": {
      "model": "llama-3.3-70b-instruct",
      "isValid": true,
      "provider": "0xf07240Efa67755B5311bc75784a061eDB47165Dd",
      "chatId": "chatcmpl-..."
    }
  }
}
```

#### `POST /api/services/settle-fee`
Manually settle fees (legacy support for specific error cases).

**Request:**
```json
{
  "providerAddress": "0xf07240Efa67755B5311bc75784a061eDB47165Dd",
  "fee": 0.000001
}
```

## 🔧 Development Scripts

```bash
# Development
npm run dev          # Start development server with hot reload
npm run watch        # Start development server with file watching
npm run serve        # Alternative development command

# Production
npm run build        # Compile TypeScript to JavaScript
npm start           # Start production server

# Testing
npm run demo   # Run comprehensive workflow demo
```

## 🏗️ Core Architecture

### Broker Service
The `brokerService` is a singleton that manages all interactions with the 0G Compute Network:

- **Wallet Management**: Automatic wallet initialization with ethers.js
- **Provider Operations**: Service discovery and provider acknowledgment
- **Query Processing**: AI query submission with authentication
- **Payment Handling**: Automatic micropayments and verification
- **Error Management**: Enhanced error messages with troubleshooting

### Application Initialization
On startup, the application automatically:
1. Checks for existing ledger accounts
2. Creates accounts with initial funding if needed (0.01 ETH default)
3. Logs initialization status
4. Starts the Express server

### Authentication Flow
1. **Provider Acknowledgment**: Required once per provider
2. **Header Generation**: Single-use authentication headers per request
3. **Query Submission**: OpenAI-compatible API calls
4. **Response Processing**: TEE verification and payment settlement

## 🔒 Security Best Practices

1. **Environment Variables**: Store private keys securely in `.env`
2. **Input Validation**: All endpoints validate request parameters
3. **Error Sanitization**: Error messages don't expose sensitive data
4. **Single-use Headers**: Authentication headers prevent replay attacks
5. **Network Validation**: RPC endpoint verification

## 🚨 Error Handling

### Common Issues and Solutions

#### Provider Acknowledgment Required
```bash
curl -X POST http://localhost:4000/api/services/acknowledge-provider \
  -H "Content-Type: application/json" \
  -d '{"providerAddress": "0xf07240Efa67755B5311bc75784a061eDB47165Dd"}'
```

#### Insufficient Balance
```bash
# Check balance
curl http://localhost:4000/api/account/info

# Add funds
curl -X POST http://localhost:4000/api/account/deposit \
  -H "Content-Type: application/json" \
  -d '{"amount": 0.1}'
```

#### Provider Not Responding
Get alternative providers:
```bash
curl http://localhost:4000/api/services/list
```

#### Headers Already Used
The system automatically generates new headers for each request. This error indicates a system issue - retry the request.

### Legacy Error: Unsettled Previous Fee

If you encounter:
```
Error: invalid previousOutputFee: expected 0.00000000000000015900000000000001138, got 0
```

Use the settle-fee endpoint with the exact amount:
```json
{
  "providerAddress": "0x3feE5a4dd5FDb8a32dDA97Bed899830605dBD9D3",
  "fee": 0.00000000000000015900000000000001138
}
```

## 📋 Example Usage

### Complete Workflow with cURL

1. **Check available services:**
```bash
curl http://localhost:4000/api/services/list
```

2. **Check account balance:**
```bash
curl http://localhost:4000/api/account/info
```

3. **Acknowledge a provider:**
```bash
curl -X POST http://localhost:4000/api/services/acknowledge-provider \
  -H "Content-Type: application/json" \
  -d '{"providerAddress": "0xf07240Efa67755B5311bc75784a061eDB47165Dd"}'
```

4. **Send a query:**
```bash
curl -X POST http://localhost:4000/api/services/query \
  -H "Content-Type: application/json" \
  -d '{
    "providerAddress": "0xf07240Efa67755B5311bc75784a061eDB47165Dd",
    "query": "Explain quantum computing in simple terms",
    "fallbackFee": 0.01
  }'
```

### Integration Example

```typescript
import { ethers } from 'ethers';
import { createZGComputeNetworkBroker } from '@0glabs/0g-serving-broker';
import OpenAI from 'openai';

// Initialize broker
const provider = new ethers.JsonRpcProvider('https://evmrpc-testnet.0g.ai');
const wallet = new ethers.Wallet(process.env.PRIVATE_KEY!, provider);
const broker = await createZGComputeNetworkBroker(wallet);

// Fund account
await broker.ledger.addLedger(0.1);

// Acknowledge provider
const providerAddress = '0xf07240Efa67755B5311bc75784a061eDB47165Dd';
await broker.inference.acknowledgeProviderSigner(providerAddress);

// Get service info
const { endpoint, model } = await broker.inference.getServiceMetadata(providerAddress);
const headers = await broker.inference.getRequestHeaders(providerAddress, query);

// Send query
const openai = new OpenAI({ baseURL: endpoint, apiKey: '', defaultHeaders: headers });
const completion = await openai.chat.completions.create({
  messages: [{ role: 'user', content: 'Hello, AI!' }],
  model: model,
});

// Process response
const isValid = await broker.inference.processResponse(
  providerAddress,
  completion.choices[0].message.content,
  completion.id
);
```

## 🌐 Network Configuration

- **Testnet RPC**: `https://evmrpc-testnet.0g.ai`
- **Faucet**: https://faucet.0g.ai
- **Chain ID**: 16600 (0G Testnet)

## 📦 Dependencies

### Core Dependencies
- `@0glabs/0g-serving-broker` - 0G Compute Network SDK
- `ethers` - Ethereum wallet and provider functionality
- `openai` - OpenAI-compatible API client
- `express` - Web framework for REST API
- `dotenv` - Environment variable management
- `crypto-js` - Cryptographic utilities

### Development Dependencies
- `typescript` - TypeScript compiler
- `ts-node` - TypeScript execution for Node.js
- `nodemon` - Development server with hot reload
- `@types/*` - TypeScript type definitions

## 🎯 Use Cases

This starter kit is perfect for:

- **Web Applications** requiring AI integration
- **API Services** with decentralized AI backends
- **Chat Interfaces** for user-friendly AI interactions
- **Prototyping** AI applications with micropayments
- **Learning** 0G Compute Network integration
- **Testing** different AI models and providers

## 🔄 Branch Structure

### Main Branch (Current)
REST API implementation with Express framework and Swagger documentation.

### CLI Branch
Command-line interface implementation:
```bash
git checkout cli-version
```

## 🛠️ Troubleshooting

### Common Setup Issues

1. **Missing Private Key**: Ensure `PRIVATE_KEY` is set in `.env`
2. **Insufficient ETH**: Get testnet ETH from the faucet
3. **Network Issues**: Check connectivity to 0G testnet
4. **Port Conflicts**: Change `PORT` in `.env` if 4000 is in use

### Performance Tips

1. **Provider Selection**: Use official providers for best reliability
2. **Balance Management**: Maintain sufficient OG tokens for queries
3. **Error Handling**: Implement proper retry logic in production
4. **Rate Limiting**: Consider implementing rate limits for public APIs

## 🔗 Additional Resources

- **0G Compute Documentation**: https://docs.0g.ai/build-with-0g/compute-network
- **SDK Examples**: https://github.com/0glabs/compute-examples
- **Discord Support**: https://discord.gg/0glabs
- **Demo Script Guide**: [DEMO_SCRIPT.md](./DEMO_SCRIPT.md)

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

*Ready to build with decentralized AI? Start with `npm run demo` to see the magic happen!* ✨
>>>>>>> e43a8e1 (OG HackQuest Guided Project 3)
