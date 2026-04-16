# Saudi Digital Wallet

## Overview

A full-featured Saudi Digital Wallet & Exchange mobile app built with Expo React Native (frontend) and Express.js (backend) in a pnpm monorepo.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **Mobile**: Expo (SDK 54) + Expo Router v6 + React Native 0.81
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM (provisioned but app uses AsyncStorage for local state)
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **State Management**: React Context + AsyncStorage
- **Build**: esbuild (CJS bundle for server)

## Structure

```text
artifacts-monorepo/
├── artifacts/
│   ├── api-server/        # Express API server
│   └── mobile/            # Expo mobile app (Saudi Digital Wallet)
│       ├── app/
│       │   ├── _layout.tsx               # Root layout with providers
│       │   ├── (tabs)/
│       │   │   ├── _layout.tsx           # Tab layout (NativeTabs + Classic fallback)
│       │   │   ├── index.tsx             # Home dashboard
│       │   │   ├── cards.tsx             # Cards management
│       │   │   ├── exchange.tsx          # Exchange screen
│       │   │   └── history.tsx           # Transaction history
│       │   ├── deposit.tsx               # Deposit modal
│       │   ├── transfer.tsx              # Local bank transfer modal
│       │   ├── crypto-transfer.tsx       # Crypto transfer modal
│       │   ├── add-card.tsx              # Add card modal
│       │   ├── card-detail.tsx           # Card detail modal
│       │   └── exchange.tsx              # Exchange route redirect
│       ├── context/WalletContext.tsx     # Main wallet state context
│       └── constants/colors.ts          # Saudi green + gold theme
├── lib/
│   ├── api-spec/           # OpenAPI spec + Orval codegen
│   ├── api-client-react/   # Generated React Query hooks
│   ├── api-zod/            # Generated Zod schemas
│   └── db/                 # Drizzle ORM schema
└── scripts/                # Utility scripts
```

## Key Features

1. **Dashboard**: SAR balance, total portfolio value, crypto assets, quick actions, recent transactions
2. **Cards**: Multiple virtual/physical cards (Mada, Visa, Mastercard) with carousel view
3. **Exchange**: SAR ↔ BTC/ETH/USDT conversion with live rates
4. **Transfer**: Local Saudi bank transfers (IBAN-based, supports all major Saudi banks)
5. **Deposit**: Multiple funding methods (Bank transfer, STC Pay, Card, Apple Pay)
6. **Crypto Transfer**: Send BTC/ETH/USDT to external wallets
7. **Transaction History**: Filtered history with grouping by date
8. **Arabic/English**: Full bilingual support with RTL awareness
9. **Theme**: Saudi green (#1A7A4A) + Gold (#C9A84C)

## Running

```bash
# Start mobile app
pnpm --filter @workspace/mobile run dev

# Start API server
pnpm --filter @workspace/api-server run dev

# Run codegen
pnpm --filter @workspace/api-spec run codegen

# Push DB schema
pnpm --filter @workspace/db run push
```
