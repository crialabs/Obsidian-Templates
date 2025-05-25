Okay, let's get our hands dirty with some code!

This will be a starter Hono project setup with Supabase integration, focusing on a few key areas you requested. Remember, this is a foundation, and a full-fledged production system will require more error handling, testing, security hardening, and detailed implementation for each module.

**Prerequisites:**

1.  **Node.js and npm/yarn:** Make sure you have them installed.
2.  **Supabase Project:**
    *   Create a Supabase project.
    *   Get your `SUPABASE_URL`, `SUPABASE_ANON_KEY`, `SUPABASE_SERVICE_ROLE_KEY`, and `SUPABASE_JWT_SECRET`.
    *   Enable JWT authentication.
    *   (Optional for now, but crucial later) Set up Row Level Security (RLS) on your tables.
3.  **Install Dependencies:**
    ```bash
    mkdir hono-omnichannel-api
    cd hono-omnichannel-api
    npm init -y
    npm install hono supabase-js @supabase/supabase-js dotenv zod hono # For JWT middleware: hono/jwt
    # Or if you prefer yarn
    # yarn add hono supabase-js @supabase/supabase-js dotenv zod hono
    npm install -D typescript @types/node ts-node nodemon # Dev dependencies
    ```
4.  **`tsconfig.json`:**
    Create a `tsconfig.json` file in your project root:
    ```json
    {
      "compilerOptions": {
        "target": "ES2020",
        "module": "ESNext",
        "moduleResolution": "node",
        "esModuleInterop": true,
        "strict": true,
        "skipLibCheck": true,
        "outDir": "./dist",
        "rootDir": "./src",
        "baseUrl": "./src",
        "paths": {
          "@/*": ["*"]
        }
      },
      "include": ["src/**/*"],
      "exclude": ["node_modules"]
    }
    ```
5.  **`.env` file:**
    Create a `.env` file in your project root (add this to `.gitignore`!):
    ```env
    SUPABASE_URL=your_supabase_url
    SUPABASE_ANON_KEY=your_supabase_anon_key
    SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key # Use with caution
    SUPABASE_JWT_SECRET=your_supabase_jwt_secret # From Supabase Auth settings
    PORT=3000
    ```

**Project Structure (Simplified):**

```
hono-omnichannel-api/
├── .env
├── package.json
├── tsconfig.json
├── src/
│   ├── index.ts            # Main Hono app entry point
│   ├── core/
│   │   ├── supabase.ts     # Supabase client setup
│   │   └── validators.ts   # Zod schemas
│   ├── api/
│   │   └── v1/
│   │       ├── middleware/
│   │       │   └── auth.ts # Authentication middleware
│   │       ├── channels.ts # Channel management routes
│   │       └── index.ts    # V1 API router
│   ├── webhooks/
│   │   └── whatsapp.ts   # Example WhatsApp webhook
│   └── types/
│       └── index.ts        # Custom TypeScript types (e.g., for Hono context)
├── public/                 # For static files like the client-side tracker
│   └── tracker.js
```

---

**1. Supabase Client (`src/core/supabase.ts`)**

```typescript
import { createClient, SupabaseClient } from '@supabase/supabase-js';
import 'dotenv/config'; // To load .env variables

const supabaseUrl = process.env.SUPABASE_URL;
const supabaseAnonKey = process.env.SUPABASE_ANON_KEY; // For client-side like operations or if RLS handles everything
const supabaseServiceRoleKey = process.env.SUPABASE_SERVICE_ROLE_KEY; // For admin operations, use carefully

if (!supabaseUrl || !supabaseAnonKey || !supabaseServiceRoleKey || !process.env.SUPABASE_JWT_SECRET) {
  throw new Error('Supabase URL, Anon Key, Service Role Key, or JWT Secret not found in environment variables.');
}

// Client for general use, respects RLS if user JWT is provided
export const supabase = createClient(supabaseUrl, supabaseAnonKey);

// Admin client, bypasses RLS. Use with extreme caution and only when necessary.
// Prefer creating specific database roles and using those with a custom JWT if possible.
export const supabaseAdmin = createClient(supabaseUrl, supabaseServiceRoleKey, {
  auth: {
    autoRefreshToken: false,
    persistSession: false,
  }
});

// Function to get a Supabase client instance for a specific user's JWT
// This client will operate under the user's RLS policies
export const getSupabaseClientForUser = (jwt: string): SupabaseClient => {
  return createClient(supabaseUrl, supabaseAnonKey, {
    global: {
      headers: { Authorization: `Bearer ${jwt}` },
    },
  });
};

console.log('Supabase client initialized.');
```

---

**2. Custom Types (`src/types/index.ts`)**

This is for extending Hono's context if needed, especially after authentication.

```typescript
// src/types/index.ts
import { JwtVariables } from 'hono/jwt'; // If using hono/jwt

export type HonoEnv = {
  Variables: {
    user?: { sub: string; [key: string]: any }; // User payload from JWT
    // You can add other variables here, e.g., db client specific to the request
    // supabaseUserClient?: SupabaseClient;
  } & JwtVariables; // Include if using hono/jwt for its default variables
  Bindings: { // For Cloudflare Workers or similar environments
    // Define your bindings here if deploying to CF Workers
  };
};
```

---

**3. Authentication Middleware (`src/api/v1/middleware/auth.ts`)**

```typescript
// src/api/v1/middleware/auth.ts
import { createMiddleware } from 'hono/factory';
import { verify } from 'hono/jwt';
import { HonoEnv } from '@/types'; // Adjust path if necessary

const jwtSecret = process.env.SUPABASE_JWT_SECRET!;

if (!jwtSecret) {
  throw new Error("SUPABASE_JWT_SECRET is not defined in environment variables.");
}

export const authMiddleware = createMiddleware<HonoEnv>(async (c, next) => {
  const authHeader = c.req.header('Authorization');
  if (!authHeader || !authHeader.startsWith('Bearer ')) {
    return c.json({ error: 'Unauthorized', message: 'Bearer token is missing or malformed.' }, 401);
  }

  const token = authHeader.substring(7); // Remove "Bearer "

  try {
    const decodedPayload = await verify(token, jwtSecret);
    // `decodedPayload` will contain `sub` (user_id), `role`, `exp`, etc.
    // You might want to add more checks here, e.g., if user exists in your db
    // or if the token is not blacklisted.

    // Example: Validate 'sub' exists
    if (!decodedPayload.sub) {
        return c.json({ error: 'Unauthorized', message: 'Invalid token: subject missing.' }, 401);
    }

    c.set('user', { sub: decodedPayload.sub as string, ...decodedPayload });
    // c.set('supabaseUserClient', getSupabaseClientForUser(token)); // Option to set user-specific client

    await next();
  } catch (err: any) {
    console.error("JWT Verification Error:", err.message);
    return c.json({ error: 'Unauthorized', message: 'Invalid or expired token.' }, 401);
  }
});
```

---

**4. Zod Validators (`src/core/validators.ts`)**

```typescript
// src/core/validators.ts
import { z } from 'zod';

export const createChannelSchema = z.object({
  type: z.enum(['whatsapp', 'telegram', 'instagram']),
  name: z.string().min(3).max(100),
  credentials: z.object({
    // Define specific credential fields per type if needed
    // For example, for WhatsApp:
    // phoneNumberId: z.string().optional(),
    // accessToken: z.string().optional(),
    // For Telegram:
    // botToken: z.string().optional(),
  }).passthrough(), // Allows other properties in credentials
});

export type CreateChannelInput = z.infer<typeof createChannelSchema>;

export const updateChannelSchema = createChannelSchema.partial();
export type UpdateChannelInput = z.infer<typeof updateChannelSchema>;

// Example for sending a message
export const sendMessageSchema = z.object({
    contact_identifier: z.string().min(1), // e.g., "whatsapp:+1234567890"
    content: z.object({
        type: z.enum(["text", "image", "template"]),
        text: z.string().optional(),
        media_url: z.string().url().optional(),
        template_name: z.string().optional(),
    }),
});
export type SendMessageInput = z.infer<typeof sendMessageSchema>;
```

---

**5. Channels API Routes (`src/api/v1/channels.ts`)**

```typescript
// src/api/v1/channels.ts
import { Hono } from 'hono';
import { zValidator } from '@hono/zod-validator';
import { supabase, supabaseAdmin } from '@/core/supabase'; // Using admin for now, adjust based on RLS
import { createChannelSchema, updateChannelSchema } from '@/core/validators';
import { authMiddleware } from './middleware/auth';
import { HonoEnv } from '@/types';

const channelsApp = new Hono<HonoEnv>();

// Apply auth middleware to all channel routes
channelsApp.use('*', authMiddleware);

// POST /api/v1/channels - Create a new channel
channelsApp.post('/', zValidator('json', createChannelSchema), async (c) => {
  const channelData = c.req.valid('json');
  const user = c.get('user'); // Get user from auth middleware

  if (!user || !user.sub) {
    return c.json({ error: 'User not authenticated or user ID missing' }, 403);
  }

  // For RLS to work correctly, Supabase needs to know the user.
  // If using the standard `supabase` client with RLS and JWT in headers:
  // const userSupabase = getSupabaseClientForUser(c.req.header('Authorization')!.substring(7));
  // const { data, error } = await userSupabase.from('channels').insert({
  //   ...channelData,
  //   user_id: user.sub, // Make sure your table has user_id and RLS is set
  // }).select().single();

  // Using supabaseAdmin for simplicity here, assumes you handle auth context.
  // In a real app, prefer user-context client or strict RLS + service roles.
  const { data, error } = await supabaseAdmin
    .from('channels')
    .insert({
      ...channelData,
      user_id: user.sub, // This should match your DB schema
      // organization_id: user.organization_id, // If using orgs
    })
    .select()
    .single();

  if (error) {
    console.error('Supabase error creating channel:', error);
    return c.json({ error: 'Failed to create channel', details: error.message }, 500);
  }
  return c.json(data, 201);
});

// GET /api/v1/channels - List channels for the authenticated user
channelsApp.get('/', async (c) => {
  const user = c.get('user');
  if (!user || !user.sub) {
    return c.json({ error: 'User not authenticated' }, 403);
  }

  const { data, error } = await supabaseAdmin // Replace with user-context client for RLS
    .from('channels')
    .select('*')
    .eq('user_id', user.sub); // Or use RLS to handle this automatically

  if (error) {
    console.error('Supabase error fetching channels:', error);
    return c.json({ error: 'Failed to fetch channels', details: error.message }, 500);
  }
  return c.json(data);
});

// GET /api/v1/channels/:id - Get a specific channel
channelsApp.get('/:id', async (c) => {
  const user = c.get('user');
  const channelId = c.req.param('id');
  if (!user || !user.sub) {
    return c.json({ error: 'User not authenticated' }, 403);
  }

  const { data, error } = await supabaseAdmin // Replace with user-context client
    .from('channels')
    .select('*')
    .eq('id', channelId)
    .eq('user_id', user.sub) // Ensure user owns this channel
    .single();

  if (error) {
    console.error(`Supabase error fetching channel ${channelId}:`, error);
    return c.json({ error: 'Channel not found or access denied', details: error.message }, 404);
  }
  return c.json(data);
});

// PUT /api/v1/channels/:id - Update a channel
channelsApp.put('/:id', zValidator('json', updateChannelSchema), async (c) => {
    const user = c.get('user');
    const channelId = c.req.param('id');
    const updateData = c.req.valid('json');

    if (!user || !user.sub) {
      return c.json({ error: 'User not authenticated' }, 403);
    }

    const { data, error } = await supabaseAdmin // Replace with user-context client
      .from('channels')
      .update({ ...updateData, updated_at: new Date().toISOString() })
      .eq('id', channelId)
      .eq('user_id', user.sub) // Ensure user owns this channel
      .select()
      .single();

    if (error) {
      console.error(`Supabase error updating channel ${channelId}:`, error);
      return c.json({ error: 'Failed to update channel or channel not found', details: error.message }, error.code === 'PGRST116' ? 404 : 500);
    }
    return c.json(data);
});

// DELETE /api/v1/channels/:id - Delete a channel
channelsApp.delete('/:id', async (c) => {
    const user = c.get('user');
    const channelId = c.req.param('id');

    if (!user || !user.sub) {
      return c.json({ error: 'User not authenticated' }, 403);
    }

    const { error, count } = await supabaseAdmin // Replace with user-context client
      .from('channels')
      .delete({ count: 'exact' }) // Get the count of deleted rows
      .eq('id', channelId)
      .eq('user_id', user.sub); // Ensure user owns this channel

    if (error) {
      console.error(`Supabase error deleting channel ${channelId}:`, error);
      return c.json({ error: 'Failed to delete channel', details: error.message }, 500);
    }
    if (count === 0) {
        return c.json({ error: 'Channel not found or not owned by user' }, 404);
    }
    return c.json({ message: 'Channel deleted successfully' }, 200);
});


export default channelsApp;
```

---

**6. V1 API Router (`src/api/v1/index.ts`)**

```typescript
// src/api/v1/index.ts
import { Hono } from 'hono';
import channelsApp from './channels';
// Import other resource routers here (messages, leads, etc.)
// import messagesApp from './messages';

const v1App = new Hono();

v1App.route('/channels', channelsApp);
// v1App.route('/messages', messagesApp);
// ... other routes

export default v1App;
```

---

**7. Example Webhook (`src/webhooks/whatsapp.ts`)**

This is a very basic placeholder. Real WhatsApp webhooks require signature verification.

```typescript
// src/webhooks/whatsapp.ts
import { Hono } from 'hono';
import { supabaseAdmin } from '@/core/supabase'; // For storing messages

const whatsappWebhookApp = new Hono();

// This secret should be part of your webhook URL or checked via a header
const WEBHOOK_VERIFY_TOKEN = process.env.WHATSAPP_WEBHOOK_VERIFY_TOKEN || "your_very_secret_token";

// WhatsApp Webhook Verification (GET request)
whatsappWebhookApp.get('/', async (c) => {
  const mode = c.req.query('hub.mode');
  const token = c.req.query('hub.verify_token');
  const challenge = c.req.query('hub.challenge');

  if (mode && token) {
    if (mode === 'subscribe' && token === WEBHOOK_VERIFY_TOKEN) {
      console.log('WhatsApp Webhook verified');
      return c.text(challenge!, 200);
    } else {
      console.warn('WhatsApp Webhook verification failed: Invalid token or mode');
      return c.text('Forbidden', 403);
    }
  }
  return c.text('Missing query parameters for verification', 400);
});


// WhatsApp Inbound Message Handler (POST request)
whatsappWebhookApp.post('/', async (c) => {
  const body = await c.req.json();
  console.log('Received WhatsApp Webhook Payload:', JSON.stringify(body, null, 2));

  // IMPORTANT: Implement WhatsApp Signature Verification here!
  // const signature = c.req.header('X-Hub-Signature-256');
  // const rawBody = await c.req.raw.clone().text(); // Hono might need a different way to get raw body if consumed
  // if (!verifyWhatsappSignature(rawBody, signature, process.env.WHATSAPP_APP_SECRET)) {
  //   console.warn('Invalid WhatsApp signature');
  //   return c.text('Invalid signature', 403);
  // }

  // Process the payload (simplified example)
  // This structure is based on Meta's Cloud API
  if (body.object === 'whatsapp_business_account') {
    body.entry?.forEach((entry: any) => {
      entry.changes?.forEach(async (change: any) => {
        if (change.field === 'messages') {
          const messageData = change.value.messages?.[0];
          if (messageData) {
            const from = messageData.from; // Sender phone number
            const messageType = messageData.type;
            let textContent = null;

            if (messageType === 'text') {
              textContent = messageData.text.body;
            } else if (messageType === 'image') {
              // Handle image (messageData.image.id to download)
              textContent = "[Image Received]";
            } // Add more types: audio, video, document, location, contacts, interactive

            console.log(`Message from ${from}: ${textContent || `[${messageType}]`}`);

            // Example: Store in Supabase (highly simplified)
            // You'd need to:
            // 1. Find or create a contact based on 'from' number.
            // 2. Find the correct channel_id.
            // 3. Store the message.
            try {
              const { error } = await supabaseAdmin.from('messages_log').insert({
                external_id: messageData.id,
                sender_identifier: from,
                receiver_identifier: change.value.metadata.display_phone_number, // Your WA number
                channel_type: 'whatsapp',
                content: textContent || `Unsupported type: ${messageType}`,
                payload: messageData, // Store the full payload for debugging/later processing
                direction: 'inbound',
                timestamp: new Date(parseInt(messageData.timestamp) * 1000),
              });
              if (error) console.error("Error saving message to DB:", error);
            } catch (dbError) {
              console.error("DB Insert Exception:", dbError);
            }
          }
        }
      });
    });
  }

  return c.text('EVENT_RECEIVED', 200); // Meta expects a 200 OK quickly
});

export default whatsappWebhookApp;
```
*Note: `messages_log` is a hypothetical table. You'd use your `messages` table.*

---

**8. Main Hono App (`src/index.ts`)**

```typescript
// src/index.ts
import { Hono } from 'hono';
import { cors } from 'hono/cors';
import { logger } from 'hono/logger';
import { secureHeaders } from 'hono/secure-headers';
import { prettyJSON } from 'hono/pretty-json';
import 'dotenv/config';

import v1ApiApp from './api/v1';
import whatsappWebhookApp from './webhooks/whatsapp';
// Import other webhook routers
// import telegramWebhookApp from './webhooks/telegram';

import { HonoEnv } from './types';

const app = new Hono<HonoEnv>();

// --- Global Middleware ---
app.use('*', logger()); // Basic request logger
app.use('*', prettyJSON()); // Pretty print JSON responses
app.use('*', secureHeaders()); // Adds security-related headers
app.use(
  '/api/*', // Apply CORS only to API routes, or '*' for all
  cors({
    origin: ['http://localhost:3001', 'https://your-nextjs-app.com', 'https://your-nuxt-app.com'], // Your frontend URLs
    allowMethods: ['GET', 'POST', 'PUT', 'DELETE', 'OPTIONS'],
    allowHeaders: ['Content-Type', 'Authorization'],
    credentials: true,
  })
);

// --- Routes ---
app.get('/', (c) => {
  return c.json({ message: 'Omnichannel API is alive!' });
});

// API Version 1
app.route('/api/v1', v1ApiApp);

// Webhooks
app.route('/webhooks/whatsapp', whatsappWebhookApp);
// app.route('/webhooks/telegram', telegramWebhookApp);
// ... other webhooks

// --- Error Handling ---
app.onError((err, c) => {
  console.error(`Unhandled error: ${err}`, err.stack);
  // Check if it's a HonoHTTPException for specific status codes
  if (err instanceof Error && 'status' in err) {
    return c.json({ error: 'An error occurred', message: err.message }, (err as any).status || 500);
  }
  return c.json({ error: 'Internal Server Error', message: err.message || 'Something went wrong' }, 500);
});

app.notFound((c) => {
  return c.json({ error: 'Not Found', message: `The path ${c.req.path} was not found.` }, 404);
});


// --- Server ---
const port = parseInt(process.env.PORT || '3000');
console.log(`Server is running on port ${port}`);

// For local development with Node.js
// In production, you might deploy this to a serverless environment
// or use a process manager like PM2.
export default {
  port: port,
  fetch: app.fetch,
};

// If you want to run directly with `ts-node src/index.ts`
// (needs `serve` from `@hono/node-server` or similar)
/*
import { serve } from '@hono/node-server'
if (process.env.NODE_ENV !== 'test') { // Avoid running server during tests
  serve({
    fetch: app.fetch,
    port: port
  }, info => {
    console.log(`Hono server listening on http://localhost:${info.port}`)
  })
}
*/
```

---

**9. Client-Side Tracker (`public/tracker.js` - Conceptual)**

This is a very simplified example. A real tracker would be more robust.

```javascript
// public/tracker.js
(function() {
  const API_ENDPOINT = 'YOUR_API_URL/api/v1/track/event'; // Replace with your actual API endpoint
  let userCookieId = null;

  function getCookie(name) {
    const value = `; ${document.cookie}`;
    const parts = value.split(`; ${name}=`);
    if (parts.length === 2) return parts.pop().split(';').shift();
    return null;
  }

  function setCookie(name, value, days) {
    let expires = "";
    if (days) {
      const date = new Date();
      date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
      expires = "; expires=" + date.toUTCString();
    }
    document.cookie = name + "=" + (value || "") + expires + "; path=/; SameSite=Lax";
  }

  function generateUUID() { // Basic UUID generator
    return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
      var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8);
      return v.toString(16);
    });
  }

  function initTracker() {
    userCookieId = getCookie('_omni_tracker_uid');
    if (!userCookieId) {
      userCookieId = generateUUID();
      setCookie('_omni_tracker_uid', userCookieId, 365); // Cookie for 1 year
    }
    console.log('OmniTracker Initialized. User ID:', userCookieId);
    trackPageView(); // Track initial page view
    attachEventListeners();
  }

  function trackEvent(eventName, properties = {}) {
    const payload = {
      event_name: eventName,
      page_url: window.location.href,
      user_cookie_id: userCookieId,
      properties: properties,
      timestamp: new Date().toISOString(),
      // You could also try to capture GTM client ID or FB fbp/fbc if available
      // gtm_client_id: getGtmClientId(),
    };

    console.log('Tracking Event:', payload);

    navigator.sendBeacon(API_ENDPOINT, JSON.stringify(payload));
    // Or use fetch with keepalive for more reliability if sendBeacon is not sufficient
    /*
    fetch(API_ENDPOINT, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(payload),
      keepalive: true // Important for requests during page unload
    }).catch(error => console.error('Error sending tracking event:', error));
    */
  }

  function trackPageView() {
    trackEvent('page_view', { title: document.title });
  }

  function attachEventListeners() {
    // Example: Track clicks on buttons with a specific data attribute
    document.addEventListener('click', function(event) {
      let targetElement = event.target;
      // Traverse up the DOM tree if the clicked element is nested
      while (targetElement && targetElement !== document.body) {
        if (targetElement.matches('[data-omni-track-click]')) {
          const eventName = targetElement.getAttribute('data-omni-track-click') || 'button_click';
          const eventProps = {};
          // Collect other data attributes as properties
          for (const attr of targetElement.attributes) {
            if (attr.name.startsWith('data-omni-prop-')) {
              eventProps[attr.name.substring('data-omni-prop-'.length)] = attr.value;
            }
          }
          eventProps.element_id = targetElement.id || null;
          eventProps.element_text = targetElement.innerText?.substring(0,100) || targetElement.value?.substring(0,100) || null;

          trackEvent(eventName, eventProps);
          break; // Stop traversing once a trackable element is found
        }
        targetElement = targetElement.parentElement;
      }
    }, true); // Use capture phase to get event early
  }

  // --- GTM & Facebook Pixel Integration (Conceptual) ---
  // This part would be more complex in reality.
  function integrateWithGTM(eventName, properties) {
    if (window.dataLayer) {
      window.dataLayer.push({
        'event': `omni_${eventName}`, // Prefix to avoid conflicts
        ...properties
      });
    }
  }

  function integrateWithFacebookPixel(eventName, properties) {
    if (window.fbq) {
      // Map your eventName