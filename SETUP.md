# Assistente BCS - Guida Setup

## Panoramica
Assistente BCS è un chatbot AI specializzato in gioco lecito (art. 110 TULPS) con:
- Widget flottante per Netlify
- Workflow n8n con Gemini 2.0 Flash
- Knowledge Base aggiornata 2025

## Step 1: n8n Workflow

### 1a. Importa il workflow
1. Vai su **n8n.io** (cloud)
2. Workflows → **Add workflow** → **Import from JSON**
3. Copia il contenuto di `n8n-workflow.json` e incolla
4. Clicca **Import**

### 1b. Configura Gemini
1. Nel nodo **"Gemini Chat - Assistente BCS"**, clicca su **Credentials** (icona lucchetto)
2. Seleziona o crea una nuova credenziale **Google Gemini**
3. Inserisci la tua **API Key** da https://aistudio.google.com/apikey
4. Salva

### 1c. Attiva webhook
1. Clicca sul nodo **"Webhook Assistente BCS"**
2. Vedi l'URL in Production (es. `https://[n8n-domain]/webhook/assistente-bcs`)
3. Copia questo URL: lo userai nel prossimo step

## Step 2: Deploy su Netlify

### 2a. Crea sito Netlify
1. Vai su **netlify.com** e accedi
2. Click **New site** → **Deploy manually**
3. Carica il file `index.html` (drag & drop)
4. Attendi il deploy (alcuni secondi)

### 2b. Configura webhook
1. Apri il file `index.html` nel sito Netlify (o clonalo, modifica, ripubblica)
2. Cerca la riga: `const WEBHOOK_URL = "https://n8n.your-domain.com/webhook/assistente-bcs";`
3. Sostituisci con l'URL copiato da n8n
4. Salva e rideploy

### 2c. Verifica
1. Apri il sito Netlify
2. Clicca il pulsante 💬 in basso a destra
3. Prova una domanda: "Cosa sono le AWP?"

## Step 3: Test

### Query di test consigliate
- "Cosa sono i PREU?"
- "Quando è la prossima ENADA?"
- "Qual è il nuovo payout delle VLT nel 2026?"
- "Come funziona la dematerializzazione QR-code?"

## Troubleshooting

**Errore di connessione nel widget**
- Verifica l'URL webhook in index.html
- Assicurati che il workflow n8n sia Attivato (tasto play)
- Controlla che la credenziale Gemini sia valida

**Nessuna risposta da Gemini**
- Verifica il saldo API key Gemini
- Controlla il modello impostato: `gemini-2.0-flash-exp`

**CORS issues**
- n8n webhook è configurato con responseMode "onReceived"
- Netlify allow-origin è impostato correttamente

## Docs
- KB: `KB_Art110_2025.md` (su GitHub o locale)
- Workflow: `n8n-workflow.json`
- Widget: `index.html`
