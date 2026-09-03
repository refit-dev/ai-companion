# SaaS AI Companion Platform

A full-stack SaaS platform that allows users to create, customize, and converse with highly personalized AI companions. Engineered with Next.js, LangChain, and Llama-2, this application features persistent conversational memory, vector search, and a complete subscription monetization pipeline.

![App Preview](https://github.com/Akash4510/ai-companion/assets/78362903/427b2425-dde1-45e6-a2b5-fceca9bfa09c)

## 🏗️ Architecture & Tech Stack

This project is built on a modern, decoupled serverless architecture, utilizing the Next.js 13 App Router for seamless client/server boundaries.

*   **Framework:** Next.js 13 (App Router), React 18, TypeScript
*   **AI & LLM Orchestration:** LangChain, Replicate (Llama-2-13b), OpenAI Edge, Vercel AI SDK
*   **Database & ORM:** MongoDB, Prisma ORM
*   **Vector Database (Memory):** Pinecone
*   **Caching & Rate Limiting:** Upstash Redis
*   **Authentication & Payments:** Clerk, Stripe
*   **UI & Styling:** Tailwind CSS, Shadcn UI (Radix Primitives), Zustand, Cloudinary

## 🧠 Key Engineering Features

### 1. Persistent Conversational Memory (Vector Search)
To overcome standard LLM context window limitations, the application utilizes **Pinecone Vector Database** coupled with **LangChain**. Chat histories are vectorized and stored, allowing the model to semantically retrieve past conversation contexts in real-time. This ensures high-fidelity, context-aware responses over long-term interactions without ballooning token costs.

### 2. Edge-Optimized AI Streaming
Leveraging the Vercel AI SDK and Edge runtime, the `api/chat` routes stream AI responses back to the client chunk-by-chunk. This drastically reduces Time-to-First-Byte (TTFB) and provides a highly responsive, chat-like UI experience even when model inference takes several seconds.

### 3. Distributed Rate Limiting
To protect expensive LLM API endpoints from abuse and DDoS, the system implements distributed rate limiting using **Upstash Redis**. Algorithms govern request frequency per user session, ensuring platform stability.

### 4. Full SaaS Monetization Pipeline
Integrated **Stripe Webhooks** securely handle subscription lifecycle events. The backend cross-references webhook signatures, syncs subscription statuses with MongoDB via Prisma, and restricts premium AI companion creation to active subscribers.

## 📸 Interface Showcase

<div style="display: flex; justify-content: space-between; align-items: center;">
  <img src="https://github.com/Akash4510/ai-companion/assets/78362903/928b4de6-e506-494d-aee8-4c9fdc9fe831" alt="Configuration Panel" style="width: 48%;">
  <img src="https://github.com/Akash4510/ai-companion/assets/78362903/164fd5bf-11b1-4bcf-9a85-a437ce3e6080" alt="Live Streaming Chat" style="width: 48%;">
</div>

*Left: Custom prompt engineering and model configuration dashboard. Right: Real-time, streaming WebRTC-style chat interface.*

## 🚀 Local Development Setup

To run this project locally, you will need to provision several external services (MongoDB, Pinecone, Clerk, Stripe, Replicate, Upstash).

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/Akash4510/ai-companion.git](https://github.com/Akash4510/ai-companion.git)
   cd ai-companion
   ```

2. **Install dependencies:**
    ```bash
    npm install
    ```

3. **Environment Configuration:**
Create a `.env` file in the root directory and populate it with your specific service keys (refer to `.env.example` if available):
    ```env
    DATABASE_URL=
    NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
    CLERK_SECRET_KEY=
    REPLICATE_API_TOKEN=
    PINECONE_API_KEY=
    PINECONE_ENVIRONMENT=
    PINECONE_INDEX=
    UPSTASH_REDIS_REST_URL=
    UPSTASH_REDIS_REST_TOKEN=
    STRIPE_API_KEY=
    STRIPE_WEBHOOK_SECRET=
    NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME=
    ```

4. **Initialize Database:**
    ```bash
    npx prisma generate
    npx prisma db push
    node scripts/seed.ts # Seeds initial category data
    ```


5. **Start the development server:**
    ```bash
    npm run dev
    ```

***
