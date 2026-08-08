# Prompt-Engineering-Project-1

## Zero-Shot & Few-Shot Data Extraction

## Description

This project demonstrates how to design a structured prompt 
that transforms messy, unstructured customer support emails 
into clean, deterministic JSON output using an LLM (AI model).

The goal was to move beyond casual "chatting" with AI and 
instead treat it like a programmable data extraction engine — 
one that follows strict rules, uses delimiters to separate 
instructions from raw data, and never invents (hallucinates) 
missing information.

## What This Prompt Does

Given a raw, unstructured customer email, the prompt extracts 
the following 5 fields and returns them in valid JSON format:

- `customer_name`
- `order_number`
- `complaint_type`
- `severity_level` (1–5)
- `contact_phone`

##  Key Techniques Used

- **Delimiters (`"""`)** – to separate system instructions 
  from raw user data, preventing prompt injection
- **Zero hallucination rule** – if a field is missing (like 
  phone number), the model returns `null` instead of making 
  up fake data
- **Strict output formatting** – the model is instructed to 
  return only valid JSON, with no conversational filler 
  ("Sure, here's your JSON!")
- **Temperature control (0.0)** – for consistent, repeatable 
  results every time

## Files in This Repository

| File | Description |
|------|--------------|
| `prompt.txt` | The final prompt used, including the test email |
| `output.json` | The actual JSON result returned by the AI |

## Test Result

The test intentionally omitted the phone number from the 
email to check if the model would hallucinate a fake number. 
The model correctly returned `null` for `contact_phone`, 
confirming the prompt works as intended.

```json
{
  "customer_name": "Sara Khan",
  "order_number": "#ORD-78234",
  "complaint_type": "Order not delivered",
  "severity_level": 3,
  "contact_phone": null
}
```

## Key Takeaway

This project shows the difference between casually prompting 
an AI and *engineering* a prompt for reliable, production-ready 
output — a core skill for building real-world AI pipelines.
