# LLM Tools

Single Page Application als Frontend für einen OpenAI-kompatiblen LLM-Endpunkt.  
Kein Build-Schritt, kein Framework, keine Abhängigkeiten – eine einzige `index.html`.

---

## Features

| Tool | Beschreibung |
|---|---|
| Übersetzen | DeepL-ähnliches Übersetzungstool, 12 Sprachen |
| Rechtschreibung | Automatische Korrektur von Rechtschreibung & Grammatik |
| Code-Kommentierung | Generiert JSDoc, Docstrings, Javadoc, XML-Docs oder Inline-Kommentare |

Alle Anfragen laufen als **Single Shot** – kein Chat-Verlauf, kein State zwischen Anfragen.

---

## Voraussetzungen

- Lokaler Webserver (z.B. XAMPP / Apache) **oder** direkt im Browser öffnen
- OpenAI-kompatibler Endpunkt, z.B.:
  - [Google Gemini](https://aistudio.google.com/apikey) (kostenlos, Cloud)
  - [LM Studio](https://lmstudio.ai) (lokal, offline)

---

## Setup

**1. Datei ablegen**
```
htdocs/llm-frontend/index.html
```

**2. Im Browser öffnen**
```
http://localhost/llm-frontend/
```

**3. Einstellungen konfigurieren**  
Oben rechts auf **⚙ Einstellungen** klicken und eintragen:

| Feld | Google Gemini | LM Studio |
|---|---|---|
| Endpoint URL | `https://generativelanguage.googleapis.com/v1beta/openai/chat/completions` | `http://127.0.0.1:1234/v1/chat/completions` |
| Modell | `gemini-2.5-flash` | `lmstudio-community/gemma-4-E4B-it-GGUF` |
| API Key | dein Gemini-Key | *(leer lassen)* |
| Max. Tokens | `32768` | `4096` |

Einstellungen werden im `localStorage` des Browsers gespeichert.

---

## Projektstruktur

```
llm-frontend/
├── index.html      # gesamte App (HTML + CSS + JS)
├── README.md
└── ANLEITUNG.txt   # Code-Erklärung
```

---

## API-Format

Die App spricht das **OpenAI Chat Completions**-Format:

```http
POST /v1/chat/completions
Content-Type: application/json
Authorization: Bearer <API_KEY>

{
  "model": "gemini-2.5-flash",
  "max_tokens": 32768,
  "messages": [
    { "role": "system", "content": "<system prompt>" },
    { "role": "user",   "content": "<user input>" }
  ]
}
```

Da Google Gemini und LM Studio dasselbe Format implementieren,  
ist kein providerspezifischer Code nötig.

---

## Tastenkürzel

| Shortcut | Aktion |
|---|---|
| `Strg + Enter` | Anfrage im aktiven Tab senden |

---

## Hinweise

- Der API-Key wird ausschließlich im `localStorage` des Browsers gespeichert – niemals an Dritte weitergeben.
- Im kostenlosen Google-Gemini-Tarif werden Eingaben möglicherweise für das Modelltraining verwendet.
- Markdown-Code-Fences (` ```lang ... ``` `) werden in der Code-Ausgabe automatisch entfernt.
