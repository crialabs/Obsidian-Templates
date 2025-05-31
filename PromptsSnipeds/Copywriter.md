```
import { GoogleGenAI } from '@google/genai';

  

// Initialize Vertex with your Cloud project and location

const ai = new GoogleGenAI({

vertexai: true,

project: 'lithe-transport-448520-m1',

location: 'us-central1'

});

const model = 'gemini-2.5-pro-preview-03-25';

  

const siText1 = {text: `You are a Senior Copywriter specializing in affiliate marketing funnels for the online casino and betting niche. Your task is to generate compelling and engaging copy focused on conversion and engagement across multiple channels (WhatsApp, Email, SMS, Telegram, Landing Pages, and Ad Creatives).`};

const tools = [

];

  

// Set up generation config

const generationConfig = {

maxOutputTokens: 37047,

temperature: 1,

topP: 0.95,

seed: 0,

responseModalities: ["TEXT"],

safetySettings: [

{

category: 'HARM_CATEGORY_HATE_SPEECH',

threshold: 'OFF',

},

{

category: 'HARM_CATEGORY_DANGEROUS_CONTENT',

threshold: 'OFF',

},

{

category: 'HARM_CATEGORY_SEXUALLY_EXPLICIT',

threshold: 'OFF',

},

{

category: 'HARM_CATEGORY_HARASSMENT',

threshold: 'OFF',

}

],

tools: tools,

systemInstruction: {

parts: [siText1]

},

};

  

const msg1Text1 = {text: `You will be provided with the following information:

  

Expert: {expert_full_name}

Main Game/Niche: {main_game_niche}

Target Audience Interests: {target_audience_interests}

Main Funnel Objective: {main_funnel_objective}

Expert's Communication Tone: {expert_communication_tone}

Main VIP Group Link: {main_vip_group_link}

Secondary Link (e.g., Sales Page): {secondary_link}

Main Benefit: {main_benefit}

Key Benefit 1: {key_benefit_1}

Key Benefit 2: {key_benefit_2}

Key Benefit 3: {key_benefit_3}

Main Social Proof: {main_social_proof}

Standard Urgency Element: {urgency_element}

Standard Bonus Offer: {bonus_offer}

Curiosity/Quick Tip about the Main Game: {curiosity_tip}

Upsell Product/Service Name: {upsell_product_service_name}

Brief Transformation Description (for Storytelling LP): {transformation_description}

  

Your task is to generate all the copy listed below, following the specifications for each item. Organize your response using the exact titles and subtitles provided. Use Brazilian Portuguese. Maintain the expert's overall tone but adapt the intensity as needed for each message's objective. **Please create longer email copy than a short snippet.**

  

### FASE 1: NOVO LEAD (BOAS-VINDAS - DIA 0) ###

  

1.1. WhatsApp - Mensagem Imediata: (Enthusiastic, welcoming, direct. Max 3 lines)

1.2. E-mail - Boas-Vindas: (Professional, welcoming, direct. Catchy Subject + Email Body)

1.3. Telegram Bot - Mensagem de Confirmação: (Informative, direct. Very short text)

  

### FASE 2: AQUECIMENTO INICIAL (DIAS 1-3) ###

  

2.1. E-mail 1 (Dia 1 - Benefícios): (Informative, value-focused, encouraging. Subject + Email Body)

2.2. E-mail 2 (Dia 2 - Prova Social): (Inspiring, trustworthy, convincing. Subject + Email Body)

2.3. E-mail 3 (Dia 3 - Urgência/Incentivo): (Urgent, direct, decisive. Subject + Email Body)

2.4. WhatsApp/Telegram - Mensagem Pessoal (Opcional Dia 1/2): (Helpful, close, expert's tone. Short text)

  

### FASE 3: REENGAGAMENTO LEAD FRIO ###

  

3.1. WhatsApp - Lembrete Informal (Dia 4/5): (Light, casual, helpful. Short, informal text)

3.2. E-mail 1 - Nova Abordagem (Dia 4/5): (Curious, intriguing, renewed. Catchy Subject + Email Body)

3.3. E-mail 2 - Curiosidade/Dica (Dia 6/7): (Educational, generous, expert. Subject + Email Body)

3.4. SMS - Chamada Direta (Dia 6/7): (Direct, urgent, clear. Very short text, ideally < 160 characters)

  

### FASE 4: CONVERSÃO LEAD QUENTE ### (Consider secondary_link if provided, otherwise focus on VIP Group)

  

4.1. WhatsApp - Contagem Regressiva/Oferta: (Urgent, scarce, direct. Short text)

4.2. Telegram - Depoimento Forte: (Inspiring, strong social proof. Short text + mention result/testimonial)

4.3. E-mail 1 - Urgência Máxima: (Decisive, urgent, unmissable. Subject reflecting urgency + Email Body)

4.4. E-mail 2 - Oferta Bônus: (Unique opportunity, generous, decisive. Subject + Email Body)

  

### FASE 5: PÓS-CONVERSÃO ### (Consider joining the group or purchasing the product)

  

5.1. E-mail 1 - Boas-Vindas Oficial: (Welcoming, congratulatory, informative. Subject + Email Body)

5.2. E-mail 2 - Entrega Bônus Extra/Conteúdo: (Generous, value-adding, exclusive. Subject + Email Body)

5.3. E-mail 3 - Upsell (Opcional): (Strategic, next-level focused, opportunity. Subject + Email Body. Only if upsell_product_service_name is provided)

  

### LANDING PAGES (Textos Principais) ###

  

6.1. Landing Page A (Captura Direta): (3 Headlines, 3 Subheadlines, 3 Testimonials/Feedbacks, 2 CTA Button Texts, Short Bio of the Expert)

6.2. Landing Page B (Benefícios): (3 Headlines, 3 Subheadlines, 3 Testimonials/Feedbacks, Short description for EACH Key Benefit, 2 CTA Button Texts, Short Bio of the Expert)

6.3. Landing Page C (Provas Sociais): (3 Headlines, 3 Subheadlines, 3 Testimonials/Feedbacks, Short Storytelling Paragraph based on transformation_description, 2 CTA Button Texts, Short Bio of the Expert)

  
  

### CRIATIVOS (Chamadas Curtas) ###

  

7.1. Chamadas para Anúncios Estáticos/Imagens: (5-7 calls to action, max 10 words each. Cover welcome, results, urgency, direct CTA)

7.2. Chamadas para Anúncios em Vídeo: (5-7 calls to action, max 10 words each. Cover welcome, results, urgency, direct CTA, adapted for video format)`};

  

const chat = ai.chats.create({

model: model,

config: generationConfig

});

  

async function sendMessage(message) {

const response = await chat.sendMessageStream({

message: message

});

process.stdout.write('stream result: ');

for await (const chunk of response) {

if (chunk.text) {

process.stdout.write(chunk.text);

} else {

process.stdout.write(JSON.stringify(chunk) + '\n');

}

}

}

  

async function generateContent() {

await sendMessage([

msg1Text1

]);

}

  

generateContent();
```