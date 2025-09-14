# GARAKA "NIGHTSHADE" - Prompt Injection Test Framework

**The Ultimate Holistic AI Pentesting Tool for Modern LLM Applications**

---

## Overview

GARAKA "NIGHTSHADE" is a comprehensive, open-source penetration testing framework designed to evaluate the security posture of applications powered by Large Language Models (LLMs). Moving beyond simplistic jailbreaks, GARAKA implements a holistic methodology inspired by real-world AI pentesting practices, systematically attacking all layers of an AI-enabled system: inputs, ecosystem, model, prompt engineering, data (RAG/KAG), and the underlying web application.

Built upon the Intent-Technique-Evasion-Utility taxonomy, GARAKA automates the discovery and exploitation of sophisticated vulnerabilities like prompt injection, data leakage from RAG systems, business logic abuse, and API over-scoping. It is not merely a scanner; it is a research platform for understanding and defeating modern AI guardrails.

*This tool is intended for authorized security assessments only.*

---

## Core Methodology (6 Pillars)

GARAKA tests against the following attack surfaces, mirroring professional AI pentest engagements:

1.  **System Inputs:** Identifies and tests all entry points (APIs, forms, file uploads, voice, etc.).
2.  **Ecosystem:** Explores connected services (logging, monitoring, observability tools, APIs) surrounding the LLM.
3.  **Model (Red Teaming):** Tests for harmful content generation, bias, and basic jailbreaks.
4.  **Prompt Engineering:** Attempts to leak or manipulate the system prompt and instruction set.
5.  **Data (RAG/KAG):** Targets vulnerabilities in Retrieval-Augmented Generation systems to exfiltrate sensitive documents, PII, or trade secrets.
6.  **Application:** Identifies classic web vulnerabilities (XSS, RCE, insecure streaming via WebSockets) within the host application.

The ultimate goal is **Pivoting**: Using access gained through any of the above vectors to compromise other internal systems.

---

## Key Features

*   **Taxonomy-Driven Testing:** Leverages a curated, evolving taxonomy of intents, techniques, and evasions derived from academic research, underground communities (Bossy Group/Liberatus), and real-world exploits.
*   **Multi-Model Support:** Tests against frontier models (OpenAI GPT-4o, Anthropic Claude 3, Google Gemini) via API and local models (Llama 3, Mistral, DeepSeek-R1) via Hugging Face Transformers.
*   **Advanced Evasion Techniques:** Implements state-of-the-art bypasses including:
    *   Meta-character confusion (`$`, `%`, `#`)
    *   Unicode obfuscation and hidden characters
    *   Emoji encoding (Unicode metadata extraction)
    *   Link smuggling (exfiltrating data via image URLs)
    *   Bjection (custom, training-data-unaware encoding schemes)
    *   Syntactic anti-classifiers (metaphorical phrasing to bypass image filters)
*   **Comprehensive Reporting:** Generates detailed JSON, CSV, and interactive HTML reports with confidence scores, success rates, and raw payloads/responses.
*   **Parallel Execution:** Utilizes multi-threading for rapid, large-scale testing across multiple targets.
*   **Extensible Architecture:** Easily add new attack vectors, custom intents, or integrate with new LLM providers.

---

## Installation

### Prerequisites
*   Python 3.9+
*   A working GPU (recommended for local models) or API keys for cloud models
*   `pip` package manager

### Setup Steps

```bash
# Clone the repository
git clone https://github.com/marcostolosa/garaka.git
cd garaka

# Create and activate a virtual environment (recommended)
python -m venv garaka-env
source garaka-env/bin/activate  # On Windows: garaka-env\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure your models
cp model_config.json.example model_config.json
# Edit model_config.json with your API keys and paths
```

---

## Usage

### Configuration
Edit `model_config.json` to define your test targets. Example:

```json
{
  "gpt-4o": {
    "type": "api",
    "model_id": "gpt-4o",
    "endpoint": "https://api.openai.com/v1/chat/completions",
    "api_key": "sk-your-openai-key-here"
  },
  "llama3": {
    "type": "local",
    "model_path": "meta-llama/Meta-Llama-3-8B-Instruct",
    "endpoint": ""
  },
  "deepseek-r1": {
    "type": "local",
    "model_path": "deepseek-ai/deepseek-llm-67b-chat",
    "endpoint": ""
  }
}
```

### Running Tests
Execute the framework against one or more configured models:

```bash
python garaka.py --models gpt-4o llama3 deepseek-r1 --workers 10
```

### Output
Results are saved in `/var/tmp/garaka/reports/report_<timestamp>/`. The primary output is `index.html`.

---

## License

MIT License. See `LICENSE` file for details.

---

## Legal Disclaimer

**GARAKA is a security research tool.** Its use must be confined to systems you own or have explicit, written authorization to test. Unauthorized use violates laws such as the Computer Fraud and Abuse Act (CFAA) and GDPR. This tool does not condone or facilitate illegal activity. Use responsibly and ethically.

---

## Acknowledgements

*   Jason Haddix for pioneering the holistic AI pentesting methodology and taxonomy.
*   All researchers contributing to the field of LLM security.
