BuyBee — AI Shopping Assistant with Memory

Overview

BuyBee is a Node.js-based AI shopping assistant that helps users discover products through a conversational interface. Users can ask queries like:

- “Suggest shoes under ₹1000”
- “Best skincare for oily skin”

Unlike typical chatbots, BuyBee improves over time by using memory via Hindsight. It learns from user preferences, feedback, and past interactions to refine future recommendations.

---

🔗 Project Links

- GitHub Repository: https://github.com/swarnasinh1/BuyBee
- LinkedIn Post: https://www.linkedin.com/posts/nikita-choudhary-b4947b378_ai-bot-means-an-artificial-intelligence-activity-7450613838288445440-_fHM
- Demo Video: https://youtu.be/V16Uw_VSPVc

---

🧠 Core Idea

Most AI assistants are stateless. They generate responses but don’t improve.

BuyBee solves this by adding memory:

- Stores user interactions
- Learns preferences (budget, dislikes, categories)
- Adapts future recommendations

---

⚙️ Tech Stack

- Node.js
- Express.js
- Frontend (HTML, CSS, JavaScript)
- Hindsight (Agent Memory)
- LLM API

---

🏗️ System Architecture

User → Frontend Chat UI → Backend API (Node.js)
→ Product Filtering Logic → LLM Response
→ Hindsight Memory Store → Future Retrieval

---

❌ Problem

Initial system behavior:

- Repeated wrong recommendations
- No memory of user preferences
- Same mistakes across sessions

Example:
User rejects sneakers → system still suggests sneakers later

---

✅ Solution (Hindsight Integration)

BuyBee stores and retrieves past interactions:

- Saves queries, responses, and feedback
- Retrieves relevant past context
- Injects memory into future responses

This allows the agent to learn from experience, not just respond.

---

💻 Key Implementation

Without Memory

app.post("/recommend", async (req, res) => {
  const { query } = req.body;
  const products = await searchProducts(query);
  const response = await llm.generate(products);
  res.json(response);
});

With Memory

await hindsight.save({
  userId,
  query,
  response,
  feedback
});

const past = await hindsight.search({
  userId,
  query
});

const response = await llm.generate({
  query,
  context: past
});

---

🔄 Real Interaction Example

User: “Suggest shoes under ₹1000”
Agent: shows sneakers

User: “I don’t like sneakers”

Before Memory:

→ Still suggests sneakers

After Memory:

→ Avoids sneakers
→ Suggests alternatives (sandals, loafers)

This behavior is not hardcoded—it emerges from stored interactions.

---

⚠️ Challenges Faced

The biggest issue was not AI—it was system integration:

- Frontend not sending "userId"
- Backend not linking memory correctly
- CORS and API connection errors
- Inconsistent request structure

Fix:

- Standardized API payloads
- Ensured user identity in every request
- Cleaned middleware setup

---

📈 Results

After adding memory:

- More relevant recommendations
- Reduced repetition
- Personalized user experience
- Behavior improved across sessions

---

📚 Key Learnings

- Memory changes behavior, not just responses
- User identity is critical for personalization
- Backend-frontend consistency is essential
- AI systems fail silently without proper state handling

---

🔮 Future Improvements

- Better product ranking algorithms
- Stronger feedback signals
- UI improvements for personalization
- Scalable memory optimization

---

🎥 Demo

Watch the working demo here:
https://youtu.be/V16Uw_VSPVc

---

📌 Conclusion

BuyBee demonstrates that adding memory transforms an AI assistant from a static responder into a learning system.

The shift is simple but powerful:
From → answering queries
To → learning from users

---

📎 References

- Hindsight GitHub: https://github.com/vectorize-io/hindsight
- Documentation: https://hindsight.vectorize.io/
- Agent Memory: https://vectorize.io/features/agent-memory