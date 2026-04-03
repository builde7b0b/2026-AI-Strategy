# Private Chat → Public YouTube Script (Sanitized Prompt Template)

Use this after any ChatGPT session. **Do NOT paste raw transcripts.** Paste a sanitized summary.

## Sanitization rules (fast)
- Replace names → {{NAME}}
- Replace client/company if needed → {{CLIENT}}, {{COMPANY}}
- Replace private links/docs → {{LINK}}
- Remove: API keys, secrets, wallet private keys, invoices, contract terms
- Replace exact revenue numbers → ranges

---

## Prompt to paste into ChatGPT

```text
You are my content operator. I want a YouTube script based on a PRIVATE conversation, but you must protect sensitive data.

Here is a SANITIZED SUMMARY of the conversation (do NOT ask for the raw transcript, and do NOT output any private placeholders as real data):

[PASTE SANITIZED SUMMARY HERE]

Instructions:
1) Create a YouTube script (8–12 minutes) with:
   - Hook (0:00–0:20)
   - Context (who I am + what I’m building)
   - The workflow (step-by-step what I did with AI)
   - The deliverables produced (specific artifacts, not vague)
   - The reusable framework viewers can copy
   - Call to action
2) Make it sound like an execution-first engineer. Confident, direct, not cringe.
3) Include 3 “pattern lines” I can reuse in future videos.
4) Include a 30-second section explaining the model choice safely:
   - Avoid hard-coding model names if it will date the video.
   - Focus on workflow and constraints as the real secret.
5) Output:
   A) Full script with timestamps
   B) A 10-line teleprompter version
   C) 5 short-form clip hooks (10–20 sec)

Constraints:
- Do NOT reveal sensitive information.
- Do NOT invent names, companies, links, or numbers.
- If a detail is missing, use placeholders like {{CLIENT}}.
```
