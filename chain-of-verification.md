Chain-of-Verification (CoVe)

Google's research team uses this to eliminate hallucinations.

The model generates an answer, then generates verification questions, answers them, and refines the original response.

Template:

Task: [your question]

Step 1: Provide your initial answer
Step 2: Generate 5 verification questions that would expose errors in your answer
Step 3: Answer each verification question
Step 4: Provide your final, corrected answer based on verification

---

Example:

Task: Explain how transformers handle long-context windows

Step 1: Provide your initial answer
Step 2: Generate 5 verification questions that would expose errors in your answer
Step 3: Answer each verification question
Step 4: Provide your final, corrected answer based on verification

---