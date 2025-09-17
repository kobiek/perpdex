# Technical Architecture - Ink Perp DEX

## System Overview

The Ink Perp DEX is built as a decentralized perpetual trading platform on Kraken's Ink blockchain, leveraging Layer 2 capabilities for high performance and low costs.

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                        Frontend Layer                          │
├─────────────────────────────────────────────────────────────────┤
│  React App  │  TradingView  │  Web3 Wallet  │  State Management │
│  (TypeScript)│  (Charts)     │  (Wagmi)      │  (Zustand)       │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                      API Gateway Layer                         │
├─────────────────────────────────────────────────────────────────┤
│  REST API  │  WebSocket  │  Rate Limiting  │  Authentication   │
│  (Express)  │  (Socket.io)│  (Redis)        │  (JWT)            │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Smart Contract Layer                        │
├─────────────────────────────────────────────────────────────────┤
│  PerpEngine  │  MarginManager  │  LiquidationEngine  │  Oracle  │
│  (Solidity)   │  (Solidity)     │  (Solidity)         │  (Chainlink) │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Ink Blockchain                            │
├─────────────────────────────────────────────────────────────────┤
│  Layer 2  │  Optimism OP Stack  │  Ethereum Security  │  Fast Finality │
└─────────────────────────────────────────────────────────────────┘
```

## Frontend Architecture

### Technology Stack

#### Core Framework
- **React 18**: Latest React with concurrent features
- **TypeScript**: Type safety and better developer experience
- **Vite**: Fast build tool and development server

#### UI Framework
- **Tailwind CSS**: Utility-first CSS framework
- **Headless UI**: Unstyled, accessible UI components
- **Framer Motion**: Animation library for smooth interactions

#### State Management
- **Zustand**: Lightweight state management
- **React Query**: Server state management and caching
- **Local Storage**: Persistent user preferences

#### Web3 Integration
- **Wagmi**: React hooks for Ethereum
- **Viem**: TypeScript interface for Ethereum
- **RainbowKit**: Wallet connection UI

#### Charting
- **TradingView Charting Library**: Professional trading charts
- **Custom Indicators**: Proprietary technical indicators

### Component Architecture

```
src/
├── components/
│   ├── ui/                    # Base UI components
│   │   ├── Button.tsx
│   │   ├── Input.tsx
│   │   ├── Modal.tsx
│   │   ├── Card.tsx
│   │   └── index.ts
│   ├── trading/               # Trading-specific components
│   │   ├── OrderPanel.tsx
│   │   ├── OrderBook.tsx
│   │   ├── Chart.tsx
│   │   ├── Positions.tsx
│   │   ├── Orders.tsx
│   │   └── index.ts
│   ├── layout/                # Layout components
│   │   ├── Header.tsx
│   │   ├── Sidebar.tsx
│   │   ├── Layout.tsx
│   │   └── index.ts
│   └── common/                # Shared components
│       ├── Loading.tsx
│       ├── ErrorBoundary.tsx
│       └── index.ts
├── hooks/                     # Custom React hooks
│   ├── useTrading.ts
│   ├── usePositions.ts
│   ├── useOrders.ts
│   ├── useWeb3.ts
│   ├── useMarketData.ts
│   └── index.ts
├── stores/                    # State management
│   ├── tradingStore.ts
│   ├── userStore.ts
│   ├── marketStore.ts
│   ├── uiStore.ts
│   └── index.ts
├── services/                  # API services
│   ├── api.ts
│   ├── websocket.ts
│   ├── priceFeed.ts
│   └── index.ts
├── utils/                     # Utility functions
│   ├── calculations.ts
│   ├── formatting.ts
│   ├── validation.ts
│   ├── constants.ts
│   └── index.ts
├── types/                     # TypeScript types
│   ├── trading.ts
│   ├── user.ts
│   ├── market.ts
│   └── index.ts
└── styles/                    # Global styles
    ├── globals.css
    ├── components.css
    └── themes.css
```

### State Management Strategy

#### Global State (Zustand)
```typescript
// tradingStore.ts
interface TradingState {
  selectedMarket: string;
  orderType: 'market' | 'limit' | 'stop';
  side: 'long' | 'short';
  size: string;
  price: string;
  leverage: number;
  positions: Position[];
  orders: Order[];
  setSelectedMarket: (market: string) => void;
  setOrderType: (type: OrderType) => void;
  // ... other actions
}
```

#### Server State (React Query)
```typescript
// Market data fetching
const { data: marketData } = useQuery({
  queryKey: ['marketData', selectedMarket],
  queryFn: () => fetchMarketData(selectedMarket),
  refetchInterval: 1000, // 1 second
});

// Position updates
const { data: positions } = useQuery({
  queryKey: ['positions', userAddress],
  queryFn: () => fetchPositions(userAddress),
  refetchInterval: 5000, // 5 seconds
});
```

## Backend Architecture

### API Gateway

#### REST API (Express.js)
```typescript
// API Routes
app.use('/api/v1', router);

// Trading endpoints
router.post('/orders', createOrder);
router.get('/orders', getOrders);
router.delete('/orders/:id', cancelOrder);

// Position endpoints
router.get('/positions', getPositions);
router.post('/positions/:id/close', closePosition);

// Market data endpoints
router.get('/markets', getMarkets);
router.get('/markets/:symbol/ticker', getTicker);
router.get('/markets/:symbol/orderbook', getOrderBook);
```

#### WebSocket API (Socket.io)
```typescript
// Real-time updates
io.on('connection', (socket) => {
  socket.on('subscribe', (channel) => {
    socket.join(channel);
  });
  
  socket.on('unsubscribe', (channel) => {
    socket.leave(channel);
  });
});

// Broadcasting updates
const broadcastMarketUpdate = (symbol: string, data: any) => {
  io.to(`market:${symbol}`).emit('marketUpdate', data);
};
```

### Data Layer

#### Database Schema (PostgreSQL)
```sql
-- Users table
CREATE TABLE users (
  id UUID PRIMARY KEY,
  address VARCHAR(42) UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Markets table
CREATE TABLE markets (
  id UUID PRIMARY KEY,
  symbol VARCHAR(20) UNIQUE NOT NULL,
  base_asset VARCHAR(10) NOT NULL,
  quote_asset VARCHAR(10) NOT NULL,
  is_active BOOLEAN DEFAULT true,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Positions table
CREATE TABLE positions (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  market_id UUID REFERENCES markets(id),
  side VARCHAR(5) NOT NULL, -- 'long' or 'short'
  size DECIMAL(20,8) NOT NULL,
  entry_price DECIMAL(20,8) NOT NULL,
  mark_price DECIMAL(20,8) NOT NULL,
  margin DECIMAL(20,8) NOT NULL,
  leverage INTEGER NOT NULL,
  pnl DECIMAL(20,8) NOT NULL,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);

-- Orders table
CREATE TABLE orders (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  market_id UUID REFERENCES markets(id),
  type VARCHAR(10) NOT NULL, -- 'market', 'limit', 'stop'
  side VARCHAR(5) NOT NULL,
  size DECIMAL(20,8) NOT NULL,
  price DECIMAL(20,8),
  status VARCHAR(10) DEFAULT 'pending',
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

#### Caching Layer (Redis)
```typescript
// Cache configuration
const redis = new Redis({
  host: process.env.REDIS_HOST,
  port: process.env.REDIS_PORT,
  password: process.env.REDIS_PASSWORD,
});

// Caching strategies
const cacheMarketData = async (symbol: string, data: any) => {
  await redis.setex(`market:${symbol}`, 60, JSON.stringify(data));
};

const getCachedMarketData = async (symbol: string) => {
  const cached = await redis.get(`market:${symbol}`);
  return cached ? JSON.parse(cached) : null;
};
```

## Smart Contract Architecture

### Contract Structure

```
contracts/
├── core/
│   ├── PerpEngine.sol          # Main trading engine
│   ├── MarginManager.sol       # Margin and collateral management
│   ├── LiquidationEngine.sol   # Automated liquidation system
│   └── FeeManager.sol          # Fee collection and distribution
├── oracles/
│   ├── PriceOracle.sol         # Price feed aggregation
│   └── ChainlinkOracle.sol     # Chainlink price feeds
├── risk/
│   ├── InsuranceFund.sol       # Platform insurance
│   ├── RiskManager.sol         # Risk assessment
│   └── CircuitBreaker.sol      # Emergency stops
├── governance/
│   ├── Governance.sol          # Protocol governance
│   ├── Timelock.sol            # Timelock for proposals
│   └── VotingEscrow.sol        # Vote-escrowed tokens
└── interfaces/
    ├── IPerpEngine.sol
    ├── IMarginManager.sol
    └── IPriceOracle.sol
```

### Core Contract Specifications

#### PerpEngine.sol
```solidity
contract PerpEngine is IPerpEngine, ReentrancyGuard, Pausable {
    struct Position {
        address user;
        address market;
        bool isLong;
        uint256 size;
        uint256 entryPrice;
        uint256 margin;
        uint256 leverage;
        uint256 lastUpdateTime;
    }
    
    struct Market {
        address baseToken;
        address quoteToken;
        uint256 maxLeverage;
        uint256 minSize;
        uint256 tickSize;
        bool isActive;
    }
    
    mapping(address => mapping(address => Position)) public positions;
    mapping(address => Market) public markets;
    
    function openPosition(
        address market,
        bool isLong,
        uint256 size,
        uint256 leverage
    ) external nonReentrant whenNotPaused {
        // Position opening logic
    }
    
    function closePosition(
        address market,
        uint256 size
    ) external nonReentrant whenNotPaused {
        // Position closing logic
    }
    
    function liquidatePosition(
        address user,
        address market
    ) external nonReentrant {
        // Liquidation logic
    }
}
```

#### MarginManager.sol
```solidity
contract MarginManager is IMarginManager, ReentrancyGuard {
    struct UserMargin {
        uint256 totalCollateral;
        uint256 usedMargin;
        uint256 availableMargin;
        uint256 unrealizedPnl;
    }
    
    mapping(address => UserMargin) public userMargins;
    mapping(address => mapping(address => uint256)) public marketMargins;
    
    function depositCollateral() external payable {
        // Collateral deposit logic
    }
    
    function withdrawCollateral(uint256 amount) external nonReentrant {
        // Collateral withdrawal logic
    }
    
    function calculateMargin(
        address user,
        address market,
        uint256 size,
        uint256 leverage
    ) external view returns (uint256) {
        // Margin calculation logic
    }
}
```

## Ink Blockchain Integration

### Layer 2 Benefits
- **Fast Finality**: Sub-second transaction confirmation
- **Low Gas Costs**: Significantly reduced transaction fees
- **Ethereum Security**: Inherits security from Ethereum mainnet
- **EVM Compatibility**: Seamless migration from Ethereum

### Deployment Strategy
```typescript
// Ink deployment configuration
const inkConfig = {
  rpcUrl: process.env.INK_RPC_URL,
  chainId: 0x1a4, // Ink chain ID
  gasPrice: '1000000000', // 1 gwei
  gasLimit: '8000000',
};

// Contract deployment
const deployContracts = async () => {
  const perpEngine = await deploy('PerpEngine', inkConfig);
  const marginManager = await deploy('MarginManager', inkConfig);
  const liquidationEngine = await deploy('LiquidationEngine', inkConfig);
  
  // Initialize contracts
  await perpEngine.initialize(marginManager.address, liquidationEngine.address);
  await marginManager.initialize(perpEngine.address);
  await liquidationEngine.initialize(perpEngine.address, marginManager.address);
};
```

### Cross-Chain Considerations
```typescript
// Bridge integration for cross-chain assets
const bridgeConfig = {
  ethereum: {
    rpcUrl: process.env.ETH_RPC_URL,
    bridgeContract: process.env.ETH_BRIDGE_CONTRACT,
  },
  ink: {
    rpcUrl: process.env.INK_RPC_URL,
    bridgeContract: process.env.INK_BRIDGE_CONTRACT,
  },
};

// Asset bridging
const bridgeAsset = async (token: string, amount: string, from: string, to: string) => {
  // Bridge logic for moving assets between chains
};
```

## Security Architecture

### Smart Contract Security
- **Audits**: Comprehensive third-party security audits
- **Formal Verification**: Mathematical proof of critical functions
- **Bug Bounty**: Ongoing security testing program
- **Upgradeability**: Controlled upgrade mechanism

### Frontend Security
- **Input Validation**: All user inputs validated and sanitized
- **Rate Limiting**: API call throttling to prevent abuse
- **CSRF Protection**: Cross-site request forgery prevention
- **XSS Prevention**: Content Security Policy and input sanitization

### Infrastructure Security
- **HTTPS**: All communications encrypted
- **API Keys**: Secure key management
- **Database**: Encrypted at rest and in transit
- **Monitoring**: Real-time security monitoring

## Performance Optimization

### Frontend Optimization
- **Code Splitting**: Lazy loading of components
- **Memoization**: React.memo for expensive components
- **Virtual Scrolling**: Efficient rendering of large lists
- **CDN**: Global content delivery for static assets

### Backend Optimization
- **Caching**: Redis for frequently accessed data
- **Database Indexing**: Optimized database queries
- **Connection Pooling**: Efficient database connections
- **Load Balancing**: Horizontal scaling

### Blockchain Optimization
- **Batch Transactions**: Group multiple operations
- **Gas Optimization**: Efficient smart contract design
- **State Caching**: Local state management for UI responsiveness

## Monitoring and Analytics

### Application Monitoring
- **Error Tracking**: Sentry for error monitoring
- **Performance**: New Relic for performance monitoring
- **Uptime**: Pingdom for availability monitoring
- **Logs**: ELK stack for log aggregation

### Business Analytics
- **User Behavior**: Google Analytics for user tracking
- **Trading Metrics**: Custom analytics for trading data
- **Revenue Tracking**: Revenue and fee analytics
- **A/B Testing**: Feature flagging and experimentation

### Blockchain Monitoring
- **Transaction Monitoring**: Real-time transaction tracking
- **Gas Usage**: Gas consumption analytics
- **Contract Events**: Smart contract event monitoring
- **Network Health**: Blockchain network monitoring

## Deployment Architecture

### Development Environment
```yaml
# docker-compose.dev.yml
version: '3.8'
services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=development
      - REACT_APP_API_URL=http://localhost:8000
  
  backend:
    build: ./backend
    ports:
      - "8000:8000"
    environment:
      - NODE_ENV=development
      - DATABASE_URL=postgresql://user:pass@db:5432/perpdex
      - REDIS_URL=redis://redis:6379
  
  db:
    image: postgres:14
    environment:
      - POSTGRES_DB=perpdex
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
  
  redis:
    image: redis:7
```

### Production Environment
```yaml
# docker-compose.prod.yml
version: '3.8'
services:
  frontend:
    build: ./frontend
    ports:
      - "80:80"
      - "443:443"
    environment:
      - NODE_ENV=production
      - REACT_APP_API_URL=https://api.perpdex.com
  
  backend:
    build: ./backend
    ports:
      - "8000:8000"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=${DATABASE_URL}
      - REDIS_URL=${REDIS_URL}
  
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
      - ./ssl:/etc/nginx/ssl
```

## Scalability Considerations

### Horizontal Scaling
- **Microservices**: Modular service architecture
- **Load Balancing**: Distribute traffic across instances
- **Database Sharding**: Partition data across databases
- **CDN**: Global content delivery

### Vertical Scaling
- **Resource Optimization**: Efficient resource utilization
- **Caching**: Reduce database load
- **Connection Pooling**: Optimize database connections
- **Memory Management**: Efficient memory usage

### Future Enhancements
- **Kubernetes**: Container orchestration
- **Service Mesh**: Istio for service communication
- **Event Streaming**: Kafka for real-time data
- **Machine Learning**: AI-powered features

This technical architecture provides a comprehensive foundation for building a scalable, secure, and performant perpetual DEX on Kraken's Ink blockchain. The modular design ensures maintainability and allows for future enhancements as the platform grows.

