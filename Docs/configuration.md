# ⚙️ Configuration

This document explains how to **configure and customize** the AI Code Review Agent.

All configurations are designed to be **simple, centralized, and extensible**, allowing developers to tune performance, models, and analysis behavior.

---

## 📁 Configuration File Location

All configurable settings are stored in:

```text
backend/config.py
```

This approach keeps configuration **separate from business logic**, following industry best practices.

---

## 🧠 LLM Configuration

### Default Model

```python
OLLAMA_MODEL = "deepseek-coder:6.7b"
```

You can switch models based on your hardware or preferences.

### Supported Models (Examples)

| Model               | Use Case                 |
| ------------------- | ------------------------ |
| deepseek-coder:6.7b | Best overall code review |
| qwen2.5-coder:7b    | Better structured output |
| codellama:7b        | Lightweight alternative  |

After changing the model, ensure it is pulled:

```bash
ollama pull <model-name>
```

---

## ⏱️ Request & Timeout Settings

```python
OLLAMA_TIMEOUT = 120  # seconds
```

* Increase for large codebases
* Reduce for faster responses

---

## 🧩 Chunking Configuration

Large files are split to stay within LLM context limits.

```python
MAX_CHUNK_SIZE = 2000  # tokens / characters
```

### Guidelines

* Smaller chunks → safer but slower
* Larger chunks → faster but risk context overflow

---

## 🧪 Static Analysis Configuration

### Enable / Disable Tools

```python
ENABLE_PYLINT = True
ENABLE_BANDIT = True
ENABLE_RADON = True
```

You can disable any tool if not required.

---

## 🌐 Language Support Configuration

Supported languages are defined using mappings:

```python
SUPPORTED_LANGUAGES = {
    "py": "python",
    "js": "javascript",
    "java": "java"
}
```

Add new languages by extending this mapping.

---

## 📝 Prompt Configuration

Prompt templates are stored in:

```text
backend/prompts/review_prompt.txt
```

### Why External Prompts?

* Easier prompt tuning
* Version control
* Better experiment tracking

Recommended changes:

* Tone (strict vs friendly)
* Output format (JSON, markdown)
* Depth of analysis

---

## 🔐 Security & Privacy Settings

```python
STORE_CODE = False
DEBUG_MODE = False
```

* Code is **not stored by default**
* Enable debug mode only in development

---

## 🚀 Performance Tuning Tips

* Use SSD storage
* Ensure Ollama has enough RAM
* Prefer fewer, larger chunks on high-memory systems
* Disable unused static analyzers

---

## 🛣️ Future Configuration Options

Planned enhancements:

* Environment-based configs (.env)
* Per-language analysis rules
* User-defined prompts
* Async worker configuration

---

## ⭐ Summary

The configuration system allows developers to **easily adapt the project** for different environments—from hackathon demos to internal enterprise tools.

Next:

* See **user-guide.md** to learn how to use the application effectively.

---

Happy configuring! ⚙️🚀
