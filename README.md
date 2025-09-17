# Ink Perp DEX - Onchain Perpetual Exchange

A decentralized perpetual exchange built on Kraken's Ink blockchain, combining the clean simplicity of Lighter with the advanced features of Axiom Pro.

## Overview

This project aims to create a next-generation perpetual DEX that leverages Ink's Layer 2 capabilities to provide:
- Sub-second transaction speeds
- Low gas fees
- Advanced trading features
- Intuitive user interface
- Professional-grade trading tools

## Design Philosophy

The UI design merges two distinct approaches:
- **Lighter's Simplicity**: Clean, uncluttered interface focused on essential trading functions
- **Axiom Pro's Power**: Advanced charting, comprehensive market data, and professional trading tools

## Key Features

### Core Trading
- Perpetual contracts with up to 100x leverage
- Cross-margin and isolated margin modes
- Advanced order types (market, limit, stop-loss, take-profit)
- Real-time price feeds and order book

### Risk Management
- Automated liquidation system
- Insurance fund for platform stability
- Dynamic margin requirements
- Position size limits

### User Experience
- Responsive design for desktop and mobile
- Dark/light theme support
- Customizable dashboard layouts
- Advanced charting with technical indicators

## Technology Stack

- **Blockchain**: Kraken Ink (Optimism OP Stack)
- **Frontend**: React + TypeScript
- **Styling**: Tailwind CSS + Framer Motion
- **Charts**: TradingView Charting Library
- **State Management**: Zustand
- **Web3**: Wagmi + Viem

## Project Structure

```
src/
├── components/          # Reusable UI components
├── pages/              # Application pages
├── hooks/              # Custom React hooks
├── stores/             # State management
├── utils/              # Utility functions
├── contracts/          # Smart contract interfaces
└── styles/             # Global styles and themes
```

## Getting Started

1. Clone the repository
2. Install dependencies: `npm install`
3. Set up environment variables
4. Run development server: `npm run dev`

## Design Files

- [Figma Wireframes](./design/figma-wireframes.md)
- [Component Library](./design/component-library.md)
- [User Flows](./design/user-flows.md)

## License

MIT License - see LICENSE file for details

