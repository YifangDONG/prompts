Confidence-Weighted Prompting

Google DeepMind uses this for high-stakes decisions.

Ask the model to rate its confidence and provide alternative answers.

Template:

Answer this question: [question]

For your answer, provide:
1. Your primary answer
2. Confidence level (0-100%)
3. Key assumptions you're making
4. What would change your answer
5. Alternative answer if you're <80% confident

---

Example:

Answer this question: Will Rust replace C++ in systems programming by 2030?

For your answer, provide:
1. Your primary answer
2. Confidence level (0-100%)
3. Key assumptions you're making
4. What would change your answer
5. Alternative answer if you're <80% confident

---

Stops you from making decisions based on AI bullshit confidence.