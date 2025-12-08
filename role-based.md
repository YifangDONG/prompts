Role-Based Constraint Prompting

The expert don't just ask AI to "write code." They assign expert roles with specific constraints.

Template:

You are a [specific role] with [X years] experience in [domain].
Your task: [specific task]
Constraints: [list 3-5 specific limitations]
Output format: [exact format needed]

---

Example:

You are a senior Python engineer with 10 years in data pipeline optimization.
Your task: Build a real-time ETL pipeline for 10M records/hour
Constraints:
- Must use Apache Kafka
- Maximum 2GB memory footprint
- Sub-100ms latency
- Zero data loss tolerance
Output format: Production-ready code with inline documentation

---
