# Secure LLMs for Audit Report Writing — A Practical Guide

This repository provides a practical, NDA-safe workflow for using **locally hosted LLMs** to assist in writing smart contract audit reports. It is intended as a **step-by-step educational guide** for security researchers who want to use AI productively without violating confidentiality or legal obligations.

---

## 📌 Why This Guide?

Using cloud-based LLMs (like ChatGPT or Claude) can expose sensitive client code to third parties, violating NDAs and IP agreements. This guide shows how to:

- Maintain full control over data and models
- Draft audit issues quickly and securely
- Customize your workflow with a local chat interface

---

## 🧠 Core Concepts

- **Cloud LLMs = NDA Risk:** Sending code to third-party servers can lead to data leaks.
- **Local LLMs = Control:** Run models like Gemma or LLaMA on your machine with no outbound traffic.
- **Prompt Engineering:** Customize system prompts to output clean, structured vulnerability descriptions.

---

## 🛠 Environment Setup

This guide uses [Ollama](https://ollama.com) as the LLM runtime and [Open WebUI](https://github.com/open-webui/open-webui) as the interface.

### 1. Install Ollama

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

### 2. Run a Local Model (e.g., Gemma 3)

```bash
ollama run gemma3:latest
```

Other supported models include: `llama3`, `deepseek-r1`

### 3. Install Open WebUI (Chat GUI)

```bash
docker run -d -p 3000:8080 \
  --add-host=host.docker.internal:host-gateway \
  -v open-webui:/app/backend/data --name open-webui \
  --restart always ghcr.io/open-webui/open-webui:v0.6.5
```

Then open [http://localhost:3000](http://localhost:3000) in your browser.

---

### 4. Set Your System Prompt in Open WebUI

To ensure consistent and professional output tailored for audit reporting:

1. Open Open WebUI in your browser at [http://localhost:3000](http://localhost:3000).
2. Go to **Settings** → **Custom Instructions**.
3. Copy the contents of `system_prompt.md` into the **System Prompt** field.
4. Scroll to the **Model Settings** section.
5. Set **Temperature** to `0.15`.

---

## 🧾 Using Your System Prompt

Customize your assistant’s behavior using `system_prompt.md` in this repo. It helps structure raw inputs (e.g., GitHub notes or findings) into ready-to-paste audit report issues.

Example workflow:

1. Copy a vulnerability note from a GitHub PR or your note app.
2. Paste it into Open WebUI.
3. Let the LLM generate a formatted issue (title, description, recommendation).
