# UI Component Specifications - Ink Perp DEX

## Overview

This document provides detailed specifications for all UI components used in the Ink Perp DEX, combining the clean simplicity of Lighter with the advanced features of Axiom Pro.

## Design System

### Color Palette
```css
:root {
  /* Primary Colors */
  --primary: #00D4AA;
  --primary-hover: #00B894;
  --primary-active: #00A085;
  
  /* Secondary Colors */
  --secondary: #1A1A1A;
  --secondary-hover: #2A2A2A;
  --secondary-active: #3A3A3A;
  
  /* Accent Colors */
  --accent-buy: #00D4AA;
  --accent-sell: #FF6B6B;
  --accent-warning: #FFA500;
  --accent-error: #FF4757;
  
  /* Background Colors */
  --bg-primary: #0F0F0F;
  --bg-secondary: #1A1A1A;
  --bg-tertiary: #2A2A2A;
  
  /* Text Colors */
  --text-primary: #FFFFFF;
  --text-secondary: #A0A0A0;
  --text-muted: #666666;
  
  /* Border Colors */
  --border-primary: #2A2A2A;
  --border-secondary: #3A3A3A;
  --border-focus: #00D4AA;
  
  /* Status Colors */
  --success: #00D4AA;
  --warning: #FFA500;
  --error: #FF4757;
  --info: #3498DB;
}
```

### Typography
```css
/* Font Families */
--font-primary: 'Inter', sans-serif;
--font-mono: 'JetBrains Mono', monospace;

/* Font Sizes */
--text-xs: 0.75rem;    /* 12px */
--text-sm: 0.875rem;   /* 14px */
--text-base: 1rem;     /* 16px */
--text-lg: 1.125rem;   /* 18px */
--text-xl: 1.25rem;    /* 20px */
--text-2xl: 1.5rem;    /* 24px */
--text-3xl: 1.875rem;  /* 30px */

/* Font Weights */
--font-normal: 400;
--font-medium: 500;
--font-semibold: 600;
--font-bold: 700;
```

### Spacing
```css
/* Spacing Scale */
--space-1: 0.25rem;   /* 4px */
--space-2: 0.5rem;    /* 8px */
--space-3: 0.75rem;   /* 12px */
--space-4: 1rem;      /* 16px */
--space-5: 1.25rem;   /* 20px */
--space-6: 1.5rem;     /* 24px */
--space-8: 2rem;      /* 32px */
--space-10: 2.5rem;   /* 40px */
--space-12: 3rem;     /* 48px */
```

## Base Components

### Button Component

#### Primary Button
```typescript
interface PrimaryButtonProps {
  children: React.ReactNode;
  onClick: () => void;
  disabled?: boolean;
  loading?: boolean;
  size?: 'sm' | 'md' | 'lg';
  fullWidth?: boolean;
}

// Styles
.primary-button {
  background: var(--primary);
  color: var(--text-primary);
  border: none;
  border-radius: 8px;
  font-family: var(--font-primary);
  font-weight: var(--font-medium);
  cursor: pointer;
  transition: all 0.2s ease-in-out;
  
  &:hover:not(:disabled) {
    background: var(--primary-hover);
    transform: translateY(-1px);
  }
  
  &:active:not(:disabled) {
    background: var(--primary-active);
    transform: translateY(0);
  }
  
  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
  
  &.loading {
    position: relative;
    color: transparent;
    
    &::after {
      content: '';
      position: absolute;
      top: 50%;
      left: 50%;
      width: 16px;
      height: 16px;
      margin: -8px 0 0 -8px;
      border: 2px solid transparent;
      border-top: 2px solid var(--text-primary);
      border-radius: 50%;
      animation: spin 1s linear infinite;
    }
  }
}

// Sizes
.primary-button--sm {
  padding: var(--space-2) var(--space-4);
  font-size: var(--text-sm);
  height: 32px;
}

.primary-button--md {
  padding: var(--space-3) var(--space-6);
  font-size: var(--text-base);
  height: 40px;
}

.primary-button--lg {
  padding: var(--space-4) var(--space-8);
  font-size: var(--text-lg);
  height: 48px;
}
```

#### Secondary Button
```typescript
interface SecondaryButtonProps {
  children: React.ReactNode;
  onClick: () => void;
  disabled?: boolean;
  size?: 'sm' | 'md' | 'lg';
  fullWidth?: boolean;
}

// Styles
.secondary-button {
  background: transparent;
  color: var(--text-primary);
  border: 1px solid var(--border-primary);
  border-radius: 8px;
  font-family: var(--font-primary);
  font-weight: var(--font-medium);
  cursor: pointer;
  transition: all 0.2s ease-in-out;
  
  &:hover:not(:disabled) {
    border-color: var(--primary);
    color: var(--primary);
  }
  
  &:active:not(:disabled) {
    background: var(--primary);
    color: var(--text-primary);
  }
  
  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
}
```

#### Danger Button
```typescript
interface DangerButtonProps {
  children: React.ReactNode;
  onClick: () => void;
  disabled?: boolean;
  size?: 'sm' | 'md' | 'lg';
  fullWidth?: boolean;
}

// Styles
.danger-button {
  background: var(--accent-error);
  color: var(--text-primary);
  border: none;
  border-radius: 8px;
  font-family: var(--font-primary);
  font-weight: var(--font-medium);
  cursor: pointer;
  transition: all 0.2s ease-in-out;
  
  &:hover:not(:disabled) {
    background: #FF3742;
    transform: translateY(-1px);
  }
  
  &:active:not(:disabled) {
    background: #E74C3C;
    transform: translateY(0);
  }
  
  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
}
```

### Input Component

#### Text Input
```typescript
interface TextInputProps {
  value: string;
  onChange: (value: string) => void;
  placeholder?: string;
  disabled?: boolean;
  error?: string;
  label?: string;
  type?: 'text' | 'email' | 'password';
  size?: 'sm' | 'md' | 'lg';
}

// Styles
.text-input {
  background: var(--bg-secondary);
  border: 1px solid var(--border-primary);
  border-radius: 8px;
  color: var(--text-primary);
  font-family: var(--font-primary);
  font-size: var(--text-base);
  padding: var(--space-3) var(--space-4);
  transition: all 0.2s ease-in-out;
  width: 100%;
  
  &:focus {
    outline: none;
    border-color: var(--border-focus);
    box-shadow: 0 0 0 3px rgba(0, 212, 170, 0.1);
  }
  
  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
  
  &::placeholder {
    color: var(--text-muted);
  }
  
  &.error {
    border-color: var(--accent-error);
  }
}

.text-input--sm {
  padding: var(--space-2) var(--space-3);
  font-size: var(--text-sm);
  height: 32px;
}

.text-input--md {
  padding: var(--space-3) var(--space-4);
  font-size: var(--text-base);
  height: 40px;
}

.text-input--lg {
  padding: var(--space-4) var(--space-5);
  font-size: var(--text-lg);
  height: 48px;
}
```

#### Number Input
```typescript
interface NumberInputProps {
  value: string;
  onChange: (value: string) => void;
  placeholder?: string;
  disabled?: boolean;
  error?: string;
  label?: string;
  min?: number;
  max?: number;
  step?: number;
  precision?: number;
}

// Styles
.number-input {
  background: var(--bg-secondary);
  border: 1px solid var(--border-primary);
  border-radius: 8px;
  color: var(--text-primary);
  font-family: var(--font-mono);
  font-size: var(--text-base);
  padding: var(--space-3) var(--space-4);
  transition: all 0.2s ease-in-out;
  width: 100%;
  text-align: right;
  
  &:focus {
    outline: none;
    border-color: var(--border-focus);
    box-shadow: 0 0 0 3px rgba(0, 212, 170, 0.1);
  }
  
  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
  
  &::placeholder {
    color: var(--text-muted);
  }
  
  &.error {
    border-color: var(--accent-error);
  }
}
```

### Card Component

#### Base Card
```typescript
interface CardProps {
  children: React.ReactNode;
  className?: string;
  padding?: 'sm' | 'md' | 'lg';
  hover?: boolean;
  clickable?: boolean;
}

// Styles
.card {
  background: var(--bg-secondary);
  border: 1px solid var(--border-primary);
  border-radius: 12px;
  transition: all 0.2s ease-in-out;
  
  &.hover:hover {
    border-color: var(--primary);
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
  }
  
  &.clickable {
    cursor: pointer;
    
    &:active {
      transform: translateY(0);
    }
  }
}

.card--sm {
  padding: var(--space-4);
}

.card--md {
  padding: var(--space-6);
}

.card--lg {
  padding: var(--space-8);
}
```

#### Trading Card
```typescript
interface TradingCardProps {
  title: string;
  children: React.ReactNode;
  actions?: React.ReactNode;
  status?: 'active' | 'inactive' | 'warning' | 'error';
}

// Styles
.trading-card {
  background: var(--bg-secondary);
  border: 1px solid var(--border-primary);
  border-radius: 12px;
  padding: var(--space-6);
  transition: all 0.2s ease-in-out;
  
  &.status-active {
    border-color: var(--success);
  }
  
  &.status-warning {
    border-color: var(--warning);
  }
  
  &.status-error {
    border-color: var(--error);
  }
  
  .trading-card__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: var(--space-4);
    
    .trading-card__title {
      font-size: var(--text-lg);
      font-weight: var(--font-semibold);
      color: var(--text-primary);
    }
    
    .trading-card__actions {
      display: flex;
      gap: var(--space-2);
    }
  }
  
  .trading-card__content {
    color: var(--text-secondary);
  }
}
```

## Trading Components

### Order Panel Component

```typescript
interface OrderPanelProps {
  selectedMarket: string;
  onOrderSubmit: (order: OrderData) => void;
  onOrderCancel: () => void;
  isConnected: boolean;
  userBalance: number;
  positions: Position[];
}

interface OrderData {
  side: 'long' | 'short';
  size: string;
  price: string;
  orderType: 'market' | 'limit' | 'stop';
  leverage: number;
}

// Component Structure
const OrderPanel: React.FC<OrderPanelProps> = ({
  selectedMarket,
  onOrderSubmit,
  onOrderCancel,
  isConnected,
  userBalance,
  positions
}) => {
  const [side, setSide] = useState<'long' | 'short'>('long');
  const [size, setSize] = useState('');
  const [price, setPrice] = useState('');
  const [orderType, setOrderType] = useState<'market' | 'limit' | 'stop'>('market');
  const [leverage, setLeverage] = useState(10);
  
  return (
    <div className="order-panel">
      <div className="order-panel__header">
        <h3>Place Order</h3>
        <div className="order-panel__market">
          {selectedMarket}
        </div>
      </div>
      
      <div className="order-panel__tabs">
        <button 
          className={`order-panel__tab ${side === 'long' ? 'active' : ''}`}
          onClick={() => setSide('long')}
        >
          Long
        </button>
        <button 
          className={`order-panel__tab ${side === 'short' ? 'active' : ''}`}
          onClick={() => setSide('short')}
        >
          Short
        </button>
      </div>
      
      <div className="order-panel__order-type">
        <button 
          className={`order-panel__order-type-btn ${orderType === 'market' ? 'active' : ''}`}
          onClick={() => setOrderType('market')}
        >
          Market
        </button>
        <button 
          className={`order-panel__order-type-btn ${orderType === 'limit' ? 'active' : ''}`}
          onClick={() => setOrderType('limit')}
        >
          Limit
        </button>
        <button 
          className={`order-panel__order-type-btn ${orderType === 'stop' ? 'active' : ''}`}
          onClick={() => setOrderType('stop')}
        >
          Stop
        </button>
      </div>
      
      <div className="order-panel__leverage">
        <label>Leverage</label>
        <div className="order-panel__leverage-buttons">
          <button onClick={() => setLeverage(1)}>1x</button>
          <button onClick={() => setLeverage(5)}>5x</button>
          <button onClick={() => setLeverage(10)}>10x</button>
          <button onClick={() => setLeverage(25)}>25x</button>
          <button onClick={() => setLeverage(50)}>50x</button>
          <button onClick={() => setLeverage(100)}>100x</button>
        </div>
        <input
          type="number"
          value={leverage}
          onChange={(e) => setLeverage(Number(e.target.value))}
          min="1"
          max="100"
        />
      </div>
      
      <div className="order-panel__size">
        <label>Size</label>
        <NumberInput
          value={size}
          onChange={setSize}
          placeholder="0.00"
          precision={8}
        />
        <div className="order-panel__size-actions">
          <button onClick={() => setSize('25%')}>25%</button>
          <button onClick={() => setSize('50%')}>50%</button>
          <button onClick={() => setSize('75%')}>75%</button>
          <button onClick={() => setSize('100%')}>100%</button>
        </div>
      </div>
      
      {orderType !== 'market' && (
        <div className="order-panel__price">
          <label>Price</label>
          <NumberInput
            value={price}
            onChange={setPrice}
            placeholder="0.00"
            precision={2}
          />
        </div>
      )}
      
      <div className="order-panel__actions">
        <PrimaryButton
          onClick={() => onOrderSubmit({ side, size, price, orderType, leverage })}
          disabled={!isConnected || !size}
          fullWidth
        >
          {side === 'long' ? 'Buy Long' : 'Sell Short'}
        </PrimaryButton>
        
        <SecondaryButton
          onClick={onOrderCancel}
          disabled={!isConnected}
          fullWidth
        >
          Cancel All
        </SecondaryButton>
      </div>
      
      <div className="order-panel__margin-info">
        <div className="margin-info__item">
          <span>Available Margin</span>
          <span>${userBalance.toFixed(2)}</span>
        </div>
        <div className="margin-info__item">
          <span>Required Margin</span>
          <span>${(Number(size) * leverage).toFixed(2)}</span>
        </div>
      </div>
    </div>
  );
};

// Styles
.order-panel {
  background: var(--bg-secondary);
  border: 1px solid var(--border-primary);
  border-radius: 12px;
  padding: var(--space-6);
  
  .order-panel__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: var(--space-4);
    
    h3 {
      font-size: var(--text-lg);
      font-weight: var(--font-semibold);
      color: var(--text-primary);
    }
    
    .order-panel__market {
      font-size: var(--text-sm);
      color: var(--text-secondary);
      background: var(--bg-tertiary);
      padding: var(--space-2) var(--space-3);
      border-radius: 6px;
    }
  }
  
  .order-panel__tabs {
    display: flex;
    margin-bottom: var(--space-4);
    
    .order-panel__tab {
      flex: 1;
      padding: var(--space-3) var(--space-4);
      background: transparent;
      border: 1px solid var(--border-primary);
      border-radius: 8px 0 0 8px;
      color: var(--text-secondary);
      cursor: pointer;
      transition: all 0.2s ease-in-out;
      
      &:last-child {
        border-radius: 0 8px 8px 0;
        border-left: none;
      }
      
      &.active {
        background: var(--primary);
        color: var(--text-primary);
        border-color: var(--primary);
      }
      
      &:hover:not(.active) {
        background: var(--bg-tertiary);
        color: var(--text-primary);
      }
    }
  }
  
  .order-panel__order-type {
    display: flex;
    gap: var(--space-2);
    margin-bottom: var(--space-4);
    
    .order-panel__order-type-btn {
      flex: 1;
      padding: var(--space-2) var(--space-3);
      background: transparent;
      border: 1px solid var(--border-primary);
      border-radius: 6px;
      color: var(--text-secondary);
      cursor: pointer;
      transition: all 0.2s ease-in-out;
      
      &.active {
        background: var(--primary);
        color: var(--text-primary);
        border-color: var(--primary);
      }
      
      &:hover:not(.active) {
        background: var(--bg-tertiary);
        color: var(--text-primary);
      }
    }
  }
  
  .order-panel__leverage {
    margin-bottom: var(--space-4);
    
    label {
      display: block;
      font-size: var(--text-sm);
      font-weight: var(--font-medium);
      color: var(--text-secondary);
      margin-bottom: var(--space-2);
    }
    
    .order-panel__leverage-buttons {
      display: flex;
      gap: var(--space-2);
      margin-bottom: var(--space-2);
      
      button {
        flex: 1;
        padding: var(--space-2) var(--space-3);
        background: transparent;
        border: 1px solid var(--border-primary);
        border-radius: 6px;
        color: var(--text-secondary);
        cursor: pointer;
        transition: all 0.2s ease-in-out;
        
        &:hover {
          background: var(--bg-tertiary);
          color: var(--text-primary);
        }
      }
    }
    
    input {
      width: 100%;
      padding: var(--space-2) var(--space-3);
      background: var(--bg-tertiary);
      border: 1px solid var(--border-primary);
      border-radius: 6px;
      color: var(--text-primary);
      text-align: center;
      
      &:focus {
        outline: none;
        border-color: var(--border-focus);
      }
    }
  }
  
  .order-panel__size {
    margin-bottom: var(--space-4);
    
    label {
      display: block;
      font-size: var(--text-sm);
      font-weight: var(--font-medium);
      color: var(--text-secondary);
      margin-bottom: var(--space-2);
    }
    
    .order-panel__size-actions {
      display: flex;
      gap: var(--space-2);
      margin-top: var(--space-2);
      
      button {
        flex: 1;
        padding: var(--space-2) var(--space-3);
        background: transparent;
        border: 1px solid var(--border-primary);
        border-radius: 6px;
        color: var(--text-secondary);
        cursor: pointer;
        transition: all 0.2s ease-in-out;
        
        &:hover {
          background: var(--bg-tertiary);
          color: var(--text-primary);
        }
      }
    }
  }
  
  .order-panel__price {
    margin-bottom: var(--space-4);
    
    label {
      display: block;
      font-size: var(--text-sm);
      font-weight: var(--font-medium);
      color: var(--text-secondary);
      margin-bottom: var(--space-2);
    }
  }
  
  .order-panel__actions {
    display: flex;
    flex-direction: column;
    gap: var(--space-3);
    margin-bottom: var(--space-4);
  }
  
  .order-panel__margin-info {
    border-top: 1px solid var(--border-primary);
    padding-top: var(--space-4);
    
    .margin-info__item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: var(--space-2);
      
      span:first-child {
        font-size: var(--text-sm);
        color: var(--text-secondary);
      }
      
      span:last-child {
        font-size: var(--text-sm);
        font-weight: var(--font-medium);
        color: var(--text-primary);
      }
    }
  }
}
```

### Order Book Component

```typescript
interface OrderBookProps {
  market: string;
  bids: OrderBookLevel[];
  asks: OrderBookLevel[];
  onLevelClick: (price: string, side: 'bid' | 'ask') => void;
}

interface OrderBookLevel {
  price: string;
  size: string;
  total: string;
}

// Component Structure
const OrderBook: React.FC<OrderBookProps> = ({
  market,
  bids,
  asks,
  onLevelClick
}) => {
  return (
    <div className="order-book">
      <div className="order-book__header">
        <h3>Order Book</h3>
        <div className="order-book__market">{market}</div>
      </div>
      
      <div className="order-book__content">
        <div className="order-book__asks">
          <div className="order-book__header-row">
            <span>Size</span>
            <span>Price</span>
          </div>
          {asks.map((ask, index) => (
            <div 
              key={index}
              className="order-book__level order-book__level--ask"
              onClick={() => onLevelClick(ask.price, 'ask')}
            >
              <span className="order-book__size">{ask.size}</span>
              <span className="order-book__price">{ask.price}</span>
            </div>
          ))}
        </div>
        
        <div className="order-book__spread">
          <span>Spread: {calculateSpread(bids[0]?.price, asks[0]?.price)}</span>
        </div>
        
        <div className="order-book__bids">
          {bids.map((bid, index) => (
            <div 
              key={index}
              className="order-book__level order-book__level--bid"
              onClick={() => onLevelClick(bid.price, 'bid')}
            >
              <span className="order-book__size">{bid.size}</span>
              <span className="order-book__price">{bid.price}</span>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};

// Styles
.order-book {
  background: var(--bg-secondary);
  border: 1px solid var(--border-primary);
  border-radius: 12px;
  padding: var(--space-4);
  
  .order-book__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: var(--space-4);
    
    h3 {
      font-size: var(--text-lg);
      font-weight: var(--font-semibold);
      color: var(--text-primary);
    }
    
    .order-book__market {
      font-size: var(--text-sm);
      color: var(--text-secondary);
      background: var(--bg-tertiary);
      padding: var(--space-2) var(--space-3);
      border-radius: 6px;
    }
  }
  
  .order-book__content {
    .order-book__header-row {
      display: flex;
      justify-content: space-between;
      padding: var(--space-2) 0;
      font-size: var(--text-xs);
      font-weight: var(--font-medium);
      color: var(--text-muted);
      border-bottom: 1px solid var(--border-primary);
    }
    
    .order-book__level {
      display: flex;
      justify-content: space-between;
      padding: var(--space-2) 0;
      cursor: pointer;
      transition: all 0.2s ease-in-out;
      
      &:hover {
        background: var(--bg-tertiary);
      }
      
      .order-book__size {
        font-family: var(--font-mono);
        font-size: var(--text-sm);
        color: var(--text-secondary);
      }
      
      .order-book__price {
        font-family: var(--font-mono);
        font-size: var(--text-sm);
        font-weight: var(--font-medium);
      }
      
      &.order-book__level--ask .order-book__price {
        color: var(--accent-sell);
      }
      
      &.order-book__level--bid .order-book__price {
        color: var(--accent-buy);
      }
    }
    
    .order-book__spread {
      text-align: center;
      padding: var(--space-2) 0;
      font-size: var(--text-xs);
      color: var(--text-muted);
      border-top: 1px solid var(--border-primary);
      border-bottom: 1px solid var(--border-primary);
    }
  }
}
```

### Positions Component

```typescript
interface PositionsProps {
  positions: Position[];
  onClosePosition: (positionId: string) => void;
  onModifyPosition: (positionId: string, newSize: string, newLeverage: number) => void;
}

interface Position {
  id: string;
  market: string;
  side: 'long' | 'short';
  size: string;
  entryPrice: string;
  markPrice: string;
  pnl: string;
  margin: string;
  leverage: number;
  liquidationPrice: string;
}

// Component Structure
const Positions: React.FC<PositionsProps> = ({
  positions,
  onClosePosition,
  onModifyPosition
}) => {
  return (
    <div className="positions">
      <div className="positions__header">
        <h3>Open Positions</h3>
        <div className="positions__count">{positions.length}</div>
      </div>
      
      <div className="positions__content">
        {positions.length === 0 ? (
          <div className="positions__empty">
            <p>No open positions</p>
          </div>
        ) : (
          <div className="positions__table">
            <div className="positions__table-header">
              <span>Market</span>
              <span>Side</span>
              <span>Size</span>
              <span>Entry Price</span>
              <span>Mark Price</span>
              <span>P&L</span>
              <span>Margin</span>
              <span>Actions</span>
            </div>
            
            {positions.map((position) => (
              <div key={position.id} className="positions__table-row">
                <span className="positions__market">{position.market}</span>
                <span className={`positions__side positions__side--${position.side}`}>
                  {position.side.toUpperCase()}
                </span>
                <span className="positions__size">{position.size}</span>
                <span className="positions__entry-price">{position.entryPrice}</span>
                <span className="positions__mark-price">{position.markPrice}</span>
                <span className={`positions__pnl ${Number(position.pnl) >= 0 ? 'positive' : 'negative'}`}>
                  {Number(position.pnl) >= 0 ? '+' : ''}{position.pnl}
                </span>
                <span className="positions__margin">{position.margin}</span>
                <div className="positions__actions">
                  <button 
                    className="positions__action-btn"
                    onClick={() => onModifyPosition(position.id, position.size, position.leverage)}
                  >
                    Modify
                  </button>
                  <button 
                    className="positions__action-btn positions__action-btn--danger"
                    onClick={() => onClosePosition(position.id)}
                  >
                    Close
                  </button>
                </div>
              </div>
            ))}
          </div>
        )}
      </div>
    </div>
  );
};

// Styles
.positions {
  background: var(--bg-secondary);
  border: 1px solid var(--border-primary);
  border-radius: 12px;
  padding: var(--space-6);
  
  .positions__header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: var(--space-4);
    
    h3 {
      font-size: var(--text-lg);
      font-weight: var(--font-semibold);
      color: var(--text-primary);
    }
    
    .positions__count {
      background: var(--bg-tertiary);
      color: var(--text-secondary);
      padding: var(--space-2) var(--space-3);
      border-radius: 6px;
      font-size: var(--text-sm);
    }
  }
  
  .positions__content {
    .positions__empty {
      text-align: center;
      padding: var(--space-8) 0;
      color: var(--text-muted);
    }
    
    .positions__table {
      .positions__table-header {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
        gap: var(--space-4);
        padding: var(--space-3) 0;
        border-bottom: 1px solid var(--border-primary);
        font-size: var(--text-sm);
        font-weight: var(--font-medium);
        color: var(--text-muted);
      }
      
      .positions__table-row {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
        gap: var(--space-4);
        padding: var(--space-3) 0;
        border-bottom: 1px solid var(--border-primary);
        align-items: center;
        transition: all 0.2s ease-in-out;
        
        &:hover {
          background: var(--bg-tertiary);
        }
        
        .positions__market {
          font-weight: var(--font-medium);
          color: var(--text-primary);
        }
        
        .positions__side {
          font-weight: var(--font-medium);
          text-transform: uppercase;
          font-size: var(--text-sm);
          
          &.positions__side--long {
            color: var(--accent-buy);
          }
          
          &.positions__side--short {
            color: var(--accent-sell);
          }
        }
        
        .positions__size,
        .positions__entry-price,
        .positions__mark-price,
        .positions__margin {
          font-family: var(--font-mono);
          font-size: var(--text-sm);
          color: var(--text-secondary);
        }
        
        .positions__pnl {
          font-family: var(--font-mono);
          font-size: var(--text-sm);
          font-weight: var(--font-medium);
          
          &.positive {
            color: var(--accent-buy);
          }
          
          &.negative {
            color: var(--accent-sell);
          }
        }
        
        .positions__actions {
          display: flex;
          gap: var(--space-2);
          
          .positions__action-btn {
            padding: var(--space-2) var(--space-3);
            background: transparent;
            border: 1px solid var(--border-primary);
            border-radius: 6px;
            color: var(--text-secondary);
            cursor: pointer;
            transition: all 0.2s ease-in-out;
            font-size: var(--text-xs);
            
            &:hover {
              background: var(--bg-tertiary);
              color: var(--text-primary);
            }
            
            &.positions__action-btn--danger {
              border-color: var(--accent-error);
              color: var(--accent-error);
              
              &:hover {
                background: var(--accent-error);
                color: var(--text-primary);
              }
            }
          }
        }
      }
    }
  }
}
```

## Layout Components

### Header Component

```typescript
interface HeaderProps {
  isConnected: boolean;
  userAddress?: string;
  userBalance?: number;
  onConnect: () => void;
  onDisconnect: () => void;
  onSettings: () => void;
}

// Component Structure
const Header: React.FC<HeaderProps> = ({
  isConnected,
  userAddress,
  userBalance,
  onConnect,
  onDisconnect,
  onSettings
}) => {
  return (
    <header className="header">
      <div className="header__left">
        <div className="header__logo">
          <img src="/logo.svg" alt="Ink Perp DEX" />
          <span>Ink Perp DEX</span>
        </div>
        
        <nav className="header__nav">
          <a href="/markets" className="header__nav-link">Markets</a>
          <a href="/portfolio" className="header__nav-link">Portfolio</a>
          <a href="/history" className="header__nav-link">History</a>
        </nav>
      </div>
      
      <div className="header__right">
        {isConnected ? (
          <div className="header__user">
            <div className="header__balance">
              ${userBalance?.toFixed(2) || '0.00'}
            </div>
            <div className="header__address">
              {userAddress?.slice(0, 6)}...{userAddress?.slice(-4)}
            </div>
            <button 
              className="header__disconnect"
              onClick={onDisconnect}
            >
              Disconnect
            </button>
          </div>
        ) : (
          <button 
            className="header__connect"
            onClick={onConnect}
          >
            Connect Wallet
          </button>
        )}
        
        <button 
          className="header__settings"
          onClick={onSettings}
        >
          <SettingsIcon />
        </button>
      </div>
    </header>
  );
};

// Styles
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: var(--space-4) var(--space-6);
  background: var(--bg-secondary);
  border-bottom: 1px solid var(--border-primary);
  
  .header__left {
    display: flex;
    align-items: center;
    gap: var(--space-8);
    
    .header__logo {
      display: flex;
      align-items: center;
      gap: var(--space-3);
      
      img {
        width: 32px;
        height: 32px;
      }
      
      span {
        font-size: var(--text-xl);
        font-weight: var(--font-bold);
        color: var(--text-primary);
      }
    }
    
    .header__nav {
      display: flex;
      gap: var(--space-6);
      
      .header__nav-link {
        color: var(--text-secondary);
        text-decoration: none;
        font-weight: var(--font-medium);
        transition: color 0.2s ease-in-out;
        
        &:hover {
          color: var(--text-primary);
        }
      }
    }
  }
  
  .header__right {
    display: flex;
    align-items: center;
    gap: var(--space-4);
    
    .header__user {
      display: flex;
      align-items: center;
      gap: var(--space-3);
      background: var(--bg-tertiary);
      padding: var(--space-2) var(--space-4);
      border-radius: 8px;
      
      .header__balance {
        font-size: var(--text-sm);
        font-weight: var(--font-medium);
        color: var(--text-primary);
      }
      
      .header__address {
        font-size: var(--text-xs);
        color: var(--text-secondary);
        font-family: var(--font-mono);
      }
      
      .header__disconnect {
        padding: var(--space-1) var(--space-2);
        background: transparent;
        border: 1px solid var(--border-primary);
        border-radius: 4px;
        color: var(--text-secondary);
        cursor: pointer;
        font-size: var(--text-xs);
        transition: all 0.2s ease-in-out;
        
        &:hover {
          background: var(--accent-error);
          color: var(--text-primary);
          border-color: var(--accent-error);
        }
      }
    }
    
    .header__connect {
      padding: var(--space-3) var(--space-6);
      background: var(--primary);
      border: none;
      border-radius: 8px;
      color: var(--text-primary);
      font-weight: var(--font-medium);
      cursor: pointer;
      transition: all 0.2s ease-in-out;
      
      &:hover {
        background: var(--primary-hover);
        transform: translateY(-1px);
      }
    }
    
    .header__settings {
      padding: var(--space-2);
      background: transparent;
      border: 1px solid var(--border-primary);
      border-radius: 6px;
      color: var(--text-secondary);
      cursor: pointer;
      transition: all 0.2s ease-in-out;
      
      &:hover {
        background: var(--bg-tertiary);
        color: var(--text-primary);
      }
    }
  }
}
```

## Responsive Design

### Mobile Breakpoints
```css
@media (max-width: 768px) {
  .order-panel {
    padding: var(--space-4);
    
    .order-panel__leverage-buttons {
      flex-wrap: wrap;
      
      button {
        flex: 1 1 calc(50% - var(--space-1));
      }
    }
  }
  
  .order-book {
    .order-book__content {
      .order-book__level {
        font-size: var(--text-xs);
      }
    }
  }
  
  .positions {
    .positions__table {
      .positions__table-header,
      .positions__table-row {
        grid-template-columns: 1fr 1fr 1fr;
        gap: var(--space-2);
      }
    }
  }
  
  .header {
    padding: var(--space-3) var(--space-4);
    
    .header__left {
      gap: var(--space-4);
      
      .header__nav {
        display: none;
      }
    }
    
    .header__right {
      gap: var(--space-2);
    }
  }
}
```

### Tablet Breakpoints
```css
@media (max-width: 1024px) {
  .order-panel {
    .order-panel__leverage-buttons {
      button {
        flex: 1 1 calc(33.333% - var(--space-1));
      }
    }
  }
  
  .positions {
    .positions__table {
      .positions__table-header,
      .positions__table-row {
        grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
        gap: var(--space-3);
      }
    }
  }
}
```

## Animation Specifications

### Micro-interactions
```css
/* Button hover animations */
.primary-button,
.secondary-button,
.danger-button {
  transition: all 0.2s ease-in-out;
}

.primary-button:hover {
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(0, 212, 170, 0.3);
}

/* Card hover animations */
.card.hover:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
}

/* Input focus animations */
.text-input:focus,
.number-input:focus {
  box-shadow: 0 0 0 3px rgba(0, 212, 170, 0.1);
}

/* Loading animations */
@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}

.loading {
  animation: pulse 1.5s ease-in-out infinite;
}
```

### Page Transitions
```css
/* Route transitions */
.page-enter {
  opacity: 0;
  transform: translateY(20px);
}

.page-enter-active {
  opacity: 1;
  transform: translateY(0);
  transition: opacity 0.3s ease-in-out, transform 0.3s ease-in-out;
}

.page-exit {
  opacity: 1;
  transform: translateY(0);
}

.page-exit-active {
  opacity: 0;
  transform: translateY(-20px);
  transition: opacity 0.3s ease-in-out, transform 0.3s ease-in-out;
}
```

This comprehensive UI component specification provides a solid foundation for building the Ink Perp DEX interface. Each component is designed to be reusable, accessible, and consistent with the overall design system while maintaining the perfect balance between Lighter's simplicity and Axiom Pro's advanced features.

