<p align="center">
  <img src="https://img.shields.io/badge/React-18.2-61DAFB?logo=react&logoColor=white" />
  <img src="https://img.shields.io/badge/TypeScript-5.2-3178C6?logo=typescript&logoColor=white" />
  <img src="https://img.shields.io/badge/Vite-5.0-646CFF?logo=vite&logoColor=white" />
  <img src="https://img.shields.io/badge/Supabase-2.39-3ECF8E?logo=supabase&logoColor=white" />
  <img src="https://img.shields.io/badge/TensorFlow.js-4.11-FF6F00?logo=tensorflow&logoColor=white" />
  <img src="https://img.shields.io/badge/License-MIT-green" />
</p>

# 🛍️ Virtual Shopping Experience — A Gamified 2D/3D E-Commerce Platform

> An interactive, avatar-based virtual shopping platform where multiple users simultaneously walk through a 2D store environment, browse products on shelves, chat in real time, receive AI-powered recommendations, and complete end-to-end purchases — all rendered on an HTML5 Canvas with a custom game engine.

---

## Table of Contents

1. [Overview](#overview)
2. [Key Features](#key-features)
3. [System Architecture](#system-architecture)
4. [Tech Stack](#tech-stack)
5. [Project Structure](#project-structure)
6. [Database Schema](#database-schema)
7. [Getting Started](#getting-started)
8. [Usage Guide](#usage-guide)
9. [AI & ML Components](#ai--ml-components)
10. [Real-Time Multiplayer](#real-time-multiplayer)
11. [Store Owner Dashboard](#store-owner-dashboard)
12. [Future Scope](#future-scope)
13. [Contributors](#contributors)
14. [License](#license)

---

## Overview

Traditional e-commerce platforms present products as static listings — there is no sense of presence, exploration, or social interaction. This project bridges that gap by recreating the **physical shopping experience** in a browser-based 2D/3D virtual environment.

Users log in, spawn as animated avatars inside a virtual store, navigate aisles using keyboard controls, interact with products placed on shelves, and make purchases — just like walking through a real retail outlet. Multiple shoppers can be present in the same store simultaneously, seeing each other's avatars move in real time and communicating via live chat.

The platform also incorporates **AI-driven product recommendations** (weighted scoring across order history, cart activity, browsing behavior, and trending data) and a **TensorFlow.js-powered product scanner** that can identify real-world objects via the user's camera and map them to in-store product categories.

---

## Key Features

| Category | Feature | Description |
|---|---|---|
| **Core Shopping** | Avatar Navigation | WASD / Arrow key movement with animated, human-like 2D avatars |
| | Product Browsing | Walk near shelf items to highlight them; click to view full details |
| | Shopping Cart | Add, remove, and adjust quantities with persistent cart state |
| | Checkout Flow | Walk to the checkout counter area to trigger purchase completion |
| | Order History | View all past orders from the user profile page |
| **Multiplayer** | Real-Time Presence | See other shoppers' avatars moving live via Supabase Realtime channels |
| | Live Chat | In-store text chat with all present users, scoped per store |
| | Player Interaction | Click on other players' avatars to view their profiles |
| **AI / ML** | Smart Recommendations | Weighted engine (40% orders, 25% cart, 20% views, 15% trending) |
| | AI Shopping Assistant | Conversational assistant for product discovery and help |
| | Product Scanner | Camera-based object identification using TensorFlow.js + COCO-SSD |
| | Category Mapping | Detected objects auto-mapped to store product categories |
| **Store Management** | Multi-Store Mall | Mall hub page listing all stores; users can enter any store |
| | Store Creation | Any authenticated user can create and configure their own store |
| | Owner Dashboard | Store owners manage products, view orders, and track analytics |
| | Product Admin | Add/edit/delete products with image upload via Supabase Storage |
| **Gamification** | Mini-Games | Fruit Catcher game that awards discount coupons on high scores |
| | NPC Helpers | In-store NPC characters that assist shoppers with dialogue |
| | HUD & Minimap | Heads-up display with minimap for store navigation |
| | Camera Controls | Mouse-look, zoom (scroll wheel), and pointer lock support |

---

## System Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                         CLIENT (Browser)                            │
│                                                                     │
│  ┌──────────────┐  ┌──────────────┐  ┌───────────────────────────┐ │
│  │  React 18 UI │  │  Custom 2D   │  │    TensorFlow.js          │ │
│  │  Components  │◄─┤  Game Engine  │  │    (COCO-SSD Model)       │ │
│  │  (TSX)       │  │  (Canvas API) │  │    Product Scanner        │ │
│  └──────┬───────┘  └──────┬───────┘  └───────────────────────────┘ │
│         │                 │                                         │
│  ┌──────┴─────────────────┴──────┐                                 │
│  │    Zustand (State Management) │                                 │
│  └──────────────┬────────────────┘                                 │
│                 │                                                   │
│  ┌──────────────┴────────────────┐                                 │
│  │  Supabase Client SDK         │                                  │
│  │  • Auth  • DB  • Realtime    │                                  │
│  └──────────────┬────────────────┘                                 │
└─────────────────┼───────────────────────────────────────────────────┘
                  │  WebSocket + REST
                  ▼
┌─────────────────────────────────────────────────────────────────────┐
│                      SUPABASE (Backend-as-a-Service)                │
│                                                                     │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌──────────────┐ │
│  │    Auth     │  │ PostgreSQL │  │  Realtime   │  │   Storage    │ │
│  │ (JWT Auth)  │  │  Database  │  │  (Presence  │  │  (Product    │ │
│  │            │  │  + RLS     │  │   & Chat)   │  │   Images)    │ │
│  └────────────┘  └────────────┘  └────────────┘  └──────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| **Frontend Framework** | React 18 | Component-based UI with hooks |
| **Language** | TypeScript 5.2 | Static typing, interfaces, and type safety |
| **Build Tool** | Vite 5 | Fast HMR, ESM-based dev server |
| **Game Engine** | Custom (HTML5 Canvas API) | 2D rendering, game loop, collision detection, camera system |
| **3D Elements** | Three.js + React Three Fiber | 3D store entrance scenes and mall rendering |
| **State Management** | Zustand | Lightweight global state for game, cart, UI |
| **Backend** | Supabase | PostgreSQL database, JWT authentication, realtime subscriptions, object storage |
| **AI / ML** | TensorFlow.js + COCO-SSD | Client-side real-world object detection via camera |
| **Routing** | React Router v6 | SPA navigation with protected routes |
| **Styling** | CSS Modules | Scoped, modular component styles |

---

## Project Structure

```
├── src/
│   ├── App.tsx                        # Root component — routing & auth provider
│   ├── main.tsx                       # Application entry point
│   │
│   ├── components/                    # Reusable UI components
│   │   ├── AIAssistant.tsx            # Conversational AI shopping helper
│   │   ├── AvatarCustomization.tsx    # Avatar appearance editor
│   │   ├── CameraControls.tsx         # Mouse-look & zoom controls
│   │   ├── CameraStyleAdvisor.tsx     # Camera-based style suggestions
│   │   ├── CartPanel.tsx              # Shopping cart sidebar
│   │   ├── ChatPanel.tsx              # Real-time in-store chat
│   │   ├── CheckoutModal.tsx          # Purchase confirmation dialog
│   │   ├── DialogueSystem.tsx         # NPC conversation system
│   │   ├── EntranceScene.tsx          # 3D store entrance animation
│   │   ├── FruitCatcherGame.tsx       # Mini-game for discount rewards
│   │   ├── HUD.tsx                    # Heads-up display overlay
│   │   ├── LoadingScreen.tsx          # Animated loading state
│   │   ├── Mall3DEntrances.tsx        # 3D mall entrance rendering
│   │   ├── Minimap.tsx                # Store minimap navigator
│   │   ├── NotificationSystem.tsx     # Toast notification handler
│   │   ├── OrderHistory.tsx           # Past purchases viewer
│   │   ├── ProductCardAdmin.tsx       # Admin product card component
│   │   ├── ProductForm.tsx            # Product creation/edit form
│   │   ├── ProductIdentifier.tsx      # Camera-based product scanner UI
│   │   ├── ProductList.tsx            # Product grid display
│   │   ├── ProductModal.tsx           # Product detail modal
│   │   ├── ProductProximityHUD.tsx    # Nearby product indicators
│   │   ├── RecommendationPanel.tsx    # AI recommendation display
│   │   ├── SmartRecommendationPanel.tsx # Enhanced recommendation UI
│   │   ├── Store3D.tsx                # Three.js 3D store renderer
│   │   ├── StoreNpcHelper.tsx         # In-store NPC assistant
│   │   └── StoreOrders.tsx            # Store owner order management
│   │
│   ├── lib/
│   │   ├── ai/                        # AI & ML modules
│   │   │   ├── productVision.ts       # TensorFlow.js COCO-SSD integration
│   │   │   └── categoryMapping.ts     # Object → product category mapper
│   │   │
│   │   ├── auth/
│   │   │   └── AuthProvider.tsx       # Supabase auth context provider
│   │   │
│   │   ├── game/                      # Custom 2D game engine
│   │   │   ├── GameEngine.ts          # Main game loop, update & render cycle
│   │   │   ├── Camera.ts             # Viewport camera with zoom & pan
│   │   │   ├── InputManager.ts        # Keyboard & mouse input handling
│   │   │   ├── Store.ts              # Store layout, shelves, collision bounds
│   │   │   ├── StoreRenderer.ts       # Canvas-based store drawing
│   │   │   ├── dialogueData.ts        # NPC dialogue trees
│   │   │   ├── types.ts              # Shared game type definitions
│   │   │   └── entities/
│   │   │       ├── Avatar.ts          # Base avatar class
│   │   │       ├── PlayerAvatar.ts    # Local player avatar with input
│   │   │       ├── RemoteAvatar.ts    # Interpolated remote player avatar
│   │   │       ├── NPCAvatar.ts       # NPC character entity
│   │   │       └── ProductEntity.ts   # Product shelf item entity
│   │   │
│   │   ├── realtime/
│   │   │   └── PresenceManager.ts     # Supabase Realtime presence & chat
│   │   │
│   │   ├── recommendations/
│   │   │   ├── recommendationEngine.ts # Weighted multi-signal scoring engine
│   │   │   └── types.ts              # Recommendation type definitions
│   │   │
│   │   ├── store/
│   │   │   └── gameStore.ts           # Zustand global state store
│   │   │
│   │   └── supabase/
│   │       ├── client.ts              # Supabase client initialization
│   │       ├── cartService.ts         # Cart CRUD operations
│   │       ├── productStorage.ts      # Product image upload service
│   │       └── types.ts              # Database type definitions
│   │
│   └── pages/                         # Route-level page components
│       ├── LoginPage.tsx              # Authentication page
│       ├── MallPage.tsx               # Store directory / mall hub
│       ├── StorePage.tsx              # Main in-store shopping view
│       ├── AdminPage.tsx              # Product administration panel
│       ├── CreateStorePage.tsx         # New store creation form
│       ├── StoreDashboardPage.tsx      # Store owner analytics dashboard
│       └── ProfilePage.tsx            # User profile & order history
│
├── supabase/                          # Database migration scripts
│   ├── schema.sql                     # Core schema (users, products, cart, orders, chat, presence, activity)
│   ├── ecommerce_migration.sql        # E-commerce feature additions
│   ├── rls_ecommerce_policies.sql     # Row Level Security policies
│   ├── recommendation_tracking.sql    # Recommendation tracking tables
│   └── ...                            # Additional migration & fix scripts
│
├── package.json                       # Dependencies & scripts
├── vite.config.ts                     # Vite build configuration
├── tsconfig.json                      # TypeScript configuration
└── .env.example                       # Environment variable template
```

---

## Database Schema

The application uses **PostgreSQL** (via Supabase) with **Row Level Security (RLS)** enabled on all tables.

```
┌──────────────┐       ┌──────────────┐       ┌──────────────────┐
│    users     │       │   products   │       │    stores        │
├──────────────┤       ├──────────────┤       ├──────────────────┤
│ id (PK, FK)  │       │ id (PK)      │       │ id (PK)          │
│ username     │       │ name         │       │ owner_id (FK)    │
│ avatar_type  │       │ description  │       │ store_name       │
│ created_at   │       │ price        │       │ description      │
│ updated_at   │       │ category     │       │ created_at       │
└──────┬───────┘       │ image_url    │       └──────────────────┘
       │               │ position_x/y │
       │               │ store_id(FK) │
       │               └──────┬───────┘
       │                      │
  ┌────┴──────┐          ┌────┴──────┐       ┌──────────────────┐
  │cart_items  │          │  orders   │       │ user_activity    │
  ├───────────┤          ├──────────┤       ├──────────────────┤
  │ id (PK)   │          │ id (PK)  │       │ id (PK)          │
  │ user_id   │          │ user_id  │       │ user_id (FK)     │
  │ product_id│          │ total    │       │ product_id (FK)  │
  │ quantity  │          │ status   │       │ action_type      │
  │ created_at│          │ items    │       │ duration         │
  └───────────┘          │(JSONB)   │       │ created_at       │
                         └──────────┘       └──────────────────┘

  ┌────────────────┐     ┌──────────────────┐
  │ chat_messages  │     │ user_presence     │
  ├────────────────┤     ├──────────────────┤
  │ id (PK)        │     │ user_id (PK, FK) │
  │ user_id (FK)   │     │ username         │
  │ username       │     │ position_x/y     │
  │ message        │     │ direction        │
  │ position_x/y   │     │ is_moving        │
  │ created_at     │     │ last_seen        │
  └────────────────┘     └──────────────────┘
```

All tables enforce **Row Level Security** — users can only read/write their own cart, orders, activity, and presence data, while products and chat messages are publicly readable.

---

## Getting Started

### Prerequisites

| Requirement | Version |
|---|---|
| Node.js | 18+ |
| npm | 9+ |
| Supabase Account | Free tier is sufficient |

### 1. Clone the Repository

```bash
git clone https://github.com/hARIsanka6/2D_shopping_experiece.git
cd 2D_shopping_experiece
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Set Up Supabase

1. Create a project at [supabase.com](https://supabase.com)
2. Navigate to **SQL Editor** and execute `supabase/schema.sql`
3. Run the additional migration scripts in the `supabase/` directory as needed:
   - `ecommerce_migration.sql` — multi-store support
   - `rls_ecommerce_policies.sql` — security policies
   - `recommendation_tracking.sql` — recommendation tables
4. Obtain your **Project URL** and **Anon Key** from **Settings → API**

### 4. Configure Environment Variables

```bash
cp .env.example .env.local
```

Edit `.env.local`:

```env
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
VITE_OPENAI_API_KEY=your_openai_api_key          # Optional — for advanced AI features
```

### 5. Start the Development Server

```bash
npm run dev
```

The application will be available at **http://localhost:3000**.

### 6. Build for Production

```bash
npm run build
```

Output is generated in the `dist/` directory, ready for static hosting.

---

## Usage Guide

1. **Sign Up / Login** — Create an account using email/password authentication
2. **Mall Hub** — Browse available stores on the mall page; enter any store or create your own
3. **Navigate** — Use `W A S D` or `Arrow Keys` to move your avatar through the store
4. **Browse Products** — Walk near shelves to see product highlights; click to view details
5. **Add to Cart** — Add products from the detail modal; manage quantities in the cart panel
6. **Chat** — Use the chat panel to communicate with other shoppers present in the store
7. **AI Assistant** — Click the AI Assistant button for product help and recommendations
8. **Scan Products** — Use the camera scanner (📸) to identify real-world objects and find matching store items
9. **Mini-Games** — Play the Fruit Catcher game to earn discount rewards
10. **Checkout** — Walk to the checkout counter area to complete your purchase

---

## AI & ML Components

### Smart Recommendation Engine

The recommendation engine uses a **weighted multi-signal scoring algorithm**:

| Signal | Weight | Data Source |
|---|---|---|
| Order History | 40% | Products the user has actually purchased |
| Cart History | 25% | Products added to cart (intent signal) |
| View History | 20% | Products the user spent time viewing |
| Trending | 15% | Global order counts across all users (30-day window) |

Scores are normalized per signal and combined into a final ranking. The engine explains *why* each product is recommended (e.g., "Because you purchased Wireless Headphones").

### TensorFlow.js Product Scanner

- Uses the **COCO-SSD** pre-trained model running entirely client-side
- Detects objects via the device camera or uploaded images
- Maps detected objects to store product categories using a curated mapping table (80+ object types → Electronics, Fashion, Sports, Home, Accessories, Food, etc.)
- Suggests relevant stores and products based on detected category

---

## Real-Time Multiplayer

The multiplayer system is powered by **Supabase Realtime** channels:

- **Presence Channel** — Tracks which users are in each store, broadcasting avatar positions, directions, animations, and camera yaw at high frequency
- **Broadcast Channel** — Handles player movement updates and in-store chat messages
- **Remote Avatar Interpolation** — Smoothly interpolates remote players' positions to reduce jitter
- **Store-Scoped Channels** — Each store has its own isolated Realtime channel, so presence and chat are scoped per store

---

## Store Owner Dashboard

Authenticated users can **create their own stores** from the Mall page. Store owners get access to:

- **Product Management** — Add, edit, and delete products with image uploads to Supabase Storage
- **Order Tracking** — View all orders placed in their store with status management
- **Store Configuration** — Set store name, description, and settings

---

## Future Scope

- Integration with OpenAI / Gemini APIs for advanced conversational AI assistant
- Voice chat between shoppers
- Mobile-responsive touch controls
- Payment gateway integration (Stripe / Razorpay)
- Expanded 3D store environments with Three.js
- Persistent avatar customization with wardrobe items
- Store analytics dashboard with sales graphs and heatmaps

---

## Contributors

| Name | GitHub | Contributions |
|---|---|---|
| Harisankar | [@hARIsanka6](https://github.com/hARIsanka6) | Project lead, core architecture, game engine |
| Jerin Joy | — | Real-time multiplayer, cart system, e-commerce features |
| Karthika Suresh | [@Karthika125](https://github.com/Karthika125) | Product identification (TensorFlow.js), NPC helper, avatar system |

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <b>Built with ❤️ as a university project — demonstrating real-time multiplayer, custom game engines, AI/ML integration, and full-stack web development.</b>
</p>
