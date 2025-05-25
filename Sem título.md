```
flowchart TD
    %% Canais Externos
    subgraph "Canais Externos"
        WA[WhatsApp Business API]
        TG[Telegram Bot API]
    end

    %% Endpoints de Webhook
    subgraph "Recepção de Webhooks"
        WA_Web[Webhook Endpoint (/webhook/whatsapp)]
        TG_Web[Webhook Endpoint (/webhook/telegram)]
    end

    %% Fila e Processamento Assíncrono
    subgraph "Processamento Assíncrono"
        Queue["Fila de Processamento<br/>(RabbitMQ/Redis)"]
        Processor["Processador de Mensagens"]
    end

    %% Middleware de Autenticação e Segregação
    subgraph "Middleware"
        Auth["Autenticação & Autorização<br/>(Hono + RLS - Supabase)"]
    end

    %% Módulos Internos
    subgraph "Serviços Internos"
        Analytics["Analytics / Trackers"]
        CRM["Leads / Project Manager"]
        Chat["Chat ao Vivo"]
    end

    %% Fluxo de Mensagens
    WA --> WA_Web
    TG --> TG_Web

    WA_Web --> Queue
    TG_Web --> Queue

    Queue --> Processor
    Processor --> Auth

    Auth --> Analytics
    Auth --> CRM
    Auth --> Chat

```