Few-Shot with Negative Examples

Anthropic discovered that showing the model what NOT to do is as powerful as showing what TO do.

Template:

I need you to [task]. Here are examples:

✅ GOOD Example 1: [example]
✅ GOOD Example 2: [example]

❌ BAD Example 1: [example]
Why it's bad: [reason]
❌ BAD Example 2: [example]
Why it's bad: [reason]

Now complete: [your actual task]

---

Example:

I need you to write cold email subject lines. Here are examples:

✅ GOOD: "Quick question about your Q4 engineering roadmap"
✅ GOOD: "Saw your post on distributed systems—thoughts on this?"

❌ BAD: "URGENT: Limited Time Offer Inside!!!"
Why it's bad: Spam trigger words, fake urgency
❌ BAD: "You won't believe what we built..."
Why it's bad: Clickbait, no context


Now write 5 subject lines for: SaaS tool that reduces cloud costs by 40%

---