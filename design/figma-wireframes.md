# Figma Wireframes - Ink Perp DEX

## Overview

This document provides detailed wireframe specifications for creating Figma designs that combine Lighter's clean simplicity with Axiom Pro's advanced features. Each wireframe includes specific measurements, component details, and interaction states.

## Design System

### Color Palette
- **Primary**: #00D4AA (Lighter green)
- **Secondary**: #1A1A1A (Dark background)
- **Accent**: #FF6B6B (Axiom red for sells)
- **Success**: #00D4AA (Lighter green)
- **Warning**: #FFA500 (Orange)
- **Error**: #FF4757 (Red)
- **Text Primary**: #FFFFFF
- **Text Secondary**: #A0A0A0
- **Background**: #0F0F0F
- **Surface**: #1A1A1A
- **Border**: #2A2A2A

### Typography
- **Headings**: Inter Bold (24px, 20px, 18px, 16px)
- **Body**: Inter Regular (14px, 12px)
- **Monospace**: JetBrains Mono (for numbers/prices)

### Spacing
- **Base Unit**: 8px
- **Small**: 4px, 8px
- **Medium**: 16px, 24px
- **Large**: 32px, 48px

## Wireframe Specifications

### 1. Main Trading Interface

#### Frame: Desktop Trading Dashboard (1920x1080)

**Header Section (1920x64px)**
```
┌─────────────────────────────────────────────────────────────────────────────────┐
│ [Logo] Ink Perp DEX    [Markets] [Portfolio] [History] [Settings] [Connect Wallet] │
└─────────────────────────────────────────────────────────────────────────────────┘
```

**Left Sidebar (280x1016px)**
```
┌─────────────────┐
│ MARKETS         │
│ ┌─────────────┐ │
│ │ BTC/USD     │ │
│ │ ETH/USD     │ │
│ │ SOL/USD     │ │
│ │ AVAX/USD    │ │
│ └─────────────┘ │
│                 │
│ PORTFOLIO       │
│ ┌─────────────┐ │
│ │ Balance     │ │
│ │ $10,000.00  │ │
│ │             │ │
│ │ Margin Used │ │
│ │ $2,500.00   │ │
│ │             │ │
│ │ Available   │ │
│ │ $7,500.00   │ │
│ └─────────────┘ │
│                 │
│ POSITIONS       │
│ ┌─────────────┐ │
│ │ BTC Long    │ │
│ │ +$250.00    │ │
│ │             │ │
│ │ ETH Short   │ │
│ │ -$125.00    │ │
│ └─────────────┘ │
└─────────────────┘
```

**Main Content Area (1640x1016px)**

**Top Row: Order Book + Chart (820x400px each)**
```
┌─────────────────────────────────┐  ┌─────────────────────────────────┐
│ ORDER BOOK                      │  │ TRADING CHART                   │
│                                 │  │                                 │
│ BID    SIZE    PRICE    ASK     │  │                                 │
│ 0.5    1.2     43250.5  0.3     │  │                                 │
│ 0.8    2.1     43250.0  0.7     │  │                                 │
│ 1.2    0.9     43249.5  1.1     │  │                                 │
│ 0.6    1.5     43249.0  0.9     │  │                                 │
│ 0.4    2.3     43248.5  0.5     │  │                                 │
│                                 │  │                                 │
│ ─────────────────────────────── │  │                                 │
│ 0.3    0.5     43250.5  0.8     │  │                                 │
│ 0.7    1.1     43251.0  0.6     │  │                                 │
│ 1.1    0.8     43251.5  1.2     │  │                                 │
│ 0.9    1.4     43252.0  0.4     │  │                                 │
│ 0.5    2.0     43252.5  0.9     │  │                                 │
│                                 │  │                                 │
│ RECENT TRADES                   │  │                                 │
│ 43250.5  0.3  Long  2m ago     │  │                                 │
│ 43249.0  0.8  Short 3m ago     │  │                                 │
│ 43251.2  1.1  Long  4m ago     │  │                                 │
└─────────────────────────────────┘  └─────────────────────────────────┘
```

**Bottom Row: Order Panel + Positions (820x616px each)**
```
┌─────────────────────────────────┐  ┌─────────────────────────────────┐
│ ORDER PLACEMENT                 │  │ OPEN POSITIONS                  │
│                                 │  │                                 │
│ [Market] [Limit] [Stop]         │  │ Symbol    Side   Size   P&L     │
│                                 │  │ ─────────────────────────────── │
│ [Long] [Short]                  │  │ BTC/USD   Long   0.5    +$250   │
│                                 │  │ ETH/USD   Short  1.2    -$125   │
│ Leverage: [10x] [25x] [50x]     │  │ SOL/USD   Long   2.0    +$75    │
│                                 │  │                                 │
│ Size: [0.5] BTC                 │  │ OPEN ORDERS                     │
│ Price: [43250.5] USD            │  │ ─────────────────────────────── │
│                                 │  │ BTC/USD   Limit  0.3    $43000  │
│ [Place Order]                   │  │ ETH/USD   Stop   0.8    $3200   │
│                                 │  │                                 │
│ MARGIN INFO                     │  │ [Close All] [Cancel All]        │
│ ─────────────────────────────── │  │                                 │
│ Used: $2,500.00                 │  │                                 │
│ Available: $7,500.00            │  │                                 │
│ Leverage: 10x                   │  │                                 │
│ Liquidation: $38,500.00         │  │                                 │
└─────────────────────────────────┘  └─────────────────────────────────┘
```

### 2. Mobile Trading Interface

#### Frame: Mobile Trading Dashboard (375x812px)

**Header (375x60px)**
```
┌─────────────────────────────────┐
│ [☰] Ink Perp DEX    [Wallet] [⚙] │
└─────────────────────────────────┘
```

**Tab Navigation (375x50px)**
```
┌─────────────────────────────────┐
│ [Trade] [Positions] [Orders] [Chart] │
└─────────────────────────────────┘
```

**Trading Panel (375x400px)**
```
┌─────────────────────────────────┐
│ BTC/USD    $43,250.50  +2.5%   │
│                                 │
│ [Long] [Short]                  │
│                                 │
│ Leverage: [10x] [25x] [50x]     │
│                                 │
│ Size: [0.5] BTC                 │
│ Price: [43250.5] USD            │
│                                 │
│ [Place Order]                   │
│                                 │
│ Margin Used: $2,500.00          │
│ Available: $7,500.00            │
└─────────────────────────────────┘
```

**Order Book (375x200px)**
```
┌─────────────────────────────────┐
│ BID    SIZE    PRICE    ASK     │
│ 0.5    1.2     43250.5  0.3     │
│ 0.8    2.1     43250.0  0.7     │
│ 1.2    0.9     43249.5  1.1     │
│ 0.6    1.5     43249.0  0.9     │
│ 0.4    2.3     43248.5  0.5     │
│ ─────────────────────────────── │
│ 0.3    0.5     43250.5  0.8     │
│ 0.7    1.1     43251.0  0.6     │
│ 1.1    0.8     43251.5  1.2     │
│ 0.9    1.4     43252.0  0.4     │
│ 0.5    2.0     43252.5  0.9     │
└─────────────────────────────────┘
```

### 3. Landing Page

#### Frame: Landing Page (1920x1080px)

**Hero Section (1920x600px)**
```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                                                                                 │
│                           Ink Perp DEX                                          │
│                    Next-Gen Perpetual Trading                                   │
│                                                                                 │
│              Built on Kraken's Ink Blockchain                                   │
│                                                                                 │
│              [Start Trading] [Learn More]                                       │
│                                                                                 │
│                                                                                 │
│              Features:                                                          │
│              • Sub-second transactions                                          │
│              • Ultra-low fees                                                   │
│              • Up to 100x leverage                                              │
│              • Professional tools                                               │
│                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────┘
```

**Features Section (1920x480px)**
```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                                                                                 │
│              [Trading] [Charts] [Risk Management] [Mobile]                      │
│                                                                                 │
│              Advanced Trading Tools                                             │
│              Professional-grade interface combining                             │
│              simplicity with power                                              │
│                                                                                 │
│              [Screenshot of trading interface]                                  │
│                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────┘
```

### 4. Portfolio Dashboard

#### Frame: Portfolio Dashboard (1920x1080px)

**Header (1920x64px)**
```
┌─────────────────────────────────────────────────────────────────────────────────┐
│ [Logo] Ink Perp DEX    [Markets] [Portfolio] [History] [Settings] [Connect Wallet] │
└─────────────────────────────────────────────────────────────────────────────────┘
```

**Main Content (1920x1016px)**
```
┌─────────────────────────────────────────────────────────────────────────────────┐
│ PORTFOLIO OVERVIEW                                                              │
│                                                                                 │
│ Total Balance: $10,000.00    P&L: +$1,250.00 (+12.5%)                         │
│                                                                                 │
│ ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐                  │
│ │ Available       │  │ Margin Used     │  │ Total Value     │                  │
│ │ $7,500.00       │  │ $2,500.00       │  │ $10,000.00      │                  │
│ └─────────────────┘  └─────────────────┘  └─────────────────┘                  │
│                                                                                 │
│ OPEN POSITIONS                                                                  │
│ ┌─────────────────────────────────────────────────────────────────────────────┐ │
│ │ Symbol    Side   Size    Entry Price  Mark Price  P&L      Margin          │ │
│ │ ────────────────────────────────────────────────────────────────────────── │ │
│ │ BTC/USD   Long   0.5     $42,000     $43,250    +$625     $2,100          │ │
│ │ ETH/USD   Short  1.2     $3,200      $3,150     +$60      $1,280          │ │
│ │ SOL/USD   Long   2.0     $95         $98        +$60      $190            │ │
│ └─────────────────────────────────────────────────────────────────────────────┘ │
│                                                                                 │
│ ORDER HISTORY                                                                   │
│ ┌─────────────────────────────────────────────────────────────────────────────┐ │
│ │ Time        Symbol    Type    Side   Size    Price    Status               │ │
│ │ ────────────────────────────────────────────────────────────────────────── │ │
│ │ 14:32:15    BTC/USD   Market  Long   0.5     $42,000  Filled              │ │
│ │ 14:28:42    ETH/USD   Limit   Short  1.2     $3,200   Filled              │ │
│ │ 14:25:18    SOL/USD   Market  Long   2.0     $95      Filled              │ │
│ └─────────────────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────────────────┘
```

### 5. Settings Page

#### Frame: Settings Page (1920x1080px)

**Header (1920x64px)**
```
┌─────────────────────────────────────────────────────────────────────────────────┐
│ [Logo] Ink Perp DEX    [Markets] [Portfolio] [History] [Settings] [Connect Wallet] │
└─────────────────────────────────────────────────────────────────────────────────┘
```

**Settings Content (1920x1016px)**
```
┌─────────────────────────────────────────────────────────────────────────────────┐
│ SETTINGS                                                                        │
│                                                                                 │
│ ┌─────────────────┐  ┌─────────────────────────────────────────────────────┐  │
│ │ Navigation      │  │ Account Settings                                     │  │
│ │                 │  │                                                      │  │
│ │ Account         │  │ Username: trader_123                                 │  │
│ │ Trading         │  │ Email: user@example.com                              │  │
│ │ Notifications   │  │ 2FA: [Enabled] [Disable]                             │  │
│ │ Security        │  │                                                      │  │
│ │ Appearance      │  │ Trading Preferences                                  │  │
│ │ Advanced        │  │ ─────────────────────────────────────────────────── │  │
│ │                 │  │ Default Leverage: [10x]                              │  │
│ │                 │  │ Order Confirmation: [✓]                              │  │
│ │                 │  │ Auto-close on liquidation: [✓]                       │  │
│ │                 │  │ Show P&L in USD: [✓]                                 │  │
│ └─────────────────┘  └─────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────────────┘
```

## Component Specifications

### Button Components

#### Primary Button
- **Size**: 120x40px
- **Background**: #00D4AA
- **Text**: #FFFFFF, Inter Medium 14px
- **Border Radius**: 8px
- **Hover**: Background #00B894
- **Active**: Background #00A085

#### Secondary Button
- **Size**: 120x40px
- **Background**: Transparent
- **Border**: 1px solid #2A2A2A
- **Text**: #FFFFFF, Inter Medium 14px
- **Border Radius**: 8px
- **Hover**: Border #00D4AA

#### Danger Button
- **Size**: 120x40px
- **Background**: #FF4757
- **Text**: #FFFFFF, Inter Medium 14px
- **Border Radius**: 8px
- **Hover**: Background #FF3742

### Input Components

#### Text Input
- **Size**: 200x40px
- **Background**: #1A1A1A
- **Border**: 1px solid #2A2A2A
- **Text**: #FFFFFF, Inter Regular 14px
- **Placeholder**: #A0A0A0
- **Border Radius**: 8px
- **Focus**: Border #00D4AA

#### Number Input
- **Size**: 120x40px
- **Background**: #1A1A1A
- **Border**: 1px solid #2A2A2A
- **Text**: #FFFFFF, JetBrains Mono 14px
- **Border Radius**: 8px
- **Focus**: Border #00D4AA

### Card Components

#### Trading Card
- **Background**: #1A1A1A
- **Border**: 1px solid #2A2A2A
- **Border Radius**: 12px
- **Padding**: 16px
- **Shadow**: 0 4px 12px rgba(0, 0, 0, 0.3)

#### Position Card
- **Background**: #1A1A1A
- **Border**: 1px solid #2A2A2A
- **Border Radius**: 8px
- **Padding**: 12px
- **Hover**: Border #00D4AA

## Interaction States

### Hover States
- **Buttons**: Background color change
- **Cards**: Border color change
- **Inputs**: Border color change
- **Links**: Text color change

### Active States
- **Buttons**: Pressed appearance
- **Inputs**: Focus ring
- **Tabs**: Underline indicator

### Loading States
- **Buttons**: Spinner animation
- **Cards**: Skeleton loading
- **Charts**: Loading overlay

### Error States
- **Inputs**: Red border and error message
- **Buttons**: Disabled appearance
- **Cards**: Error icon and message

## Responsive Breakpoints

- **Mobile**: 375px - 767px
- **Tablet**: 768px - 1023px
- **Desktop**: 1024px - 1439px
- **Large Desktop**: 1440px+

## Animation Specifications

### Micro-interactions
- **Button Hover**: 0.2s ease-in-out
- **Card Hover**: 0.3s ease-in-out
- **Input Focus**: 0.15s ease-in-out
- **Tab Switch**: 0.2s ease-in-out

### Page Transitions
- **Route Change**: 0.3s ease-in-out
- **Modal Open**: 0.2s ease-out
- **Modal Close**: 0.15s ease-in

### Data Updates
- **Price Changes**: 0.1s ease-out
- **Order Updates**: 0.2s ease-out
- **Position Updates**: 0.3s ease-out

## Accessibility Guidelines

### Color Contrast
- **Text on Background**: Minimum 4.5:1 ratio
- **Interactive Elements**: Minimum 3:1 ratio
- **Error States**: High contrast for visibility

### Keyboard Navigation
- **Tab Order**: Logical flow through interface
- **Focus Indicators**: Clear visual focus states
- **Keyboard Shortcuts**: Common trading shortcuts

### Screen Reader Support
- **Alt Text**: Descriptive text for images
- **ARIA Labels**: Proper labeling for interactive elements
- **Semantic HTML**: Proper heading structure

## Implementation Notes

### Figma Setup
1. Create master components for all reusable elements
2. Use auto-layout for responsive components
3. Set up proper text styles and color styles
4. Create component variants for different states
5. Use constraints for responsive behavior

### Development Handoff
1. Export assets at 2x resolution for retina displays
2. Provide exact measurements and spacing
3. Include all interaction states and animations
4. Document color codes and typography specifications
5. Create style guide for consistent implementation

This wireframe specification provides a comprehensive foundation for creating the Figma designs. Each component and layout is detailed with specific measurements, colors, and interaction states to ensure consistent implementation across the platform.

