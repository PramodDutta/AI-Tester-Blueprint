# LangFlow Project: Jira → Test Case RAG

- **Author:** Pramod Dutta
- **Role:** Principal SDET
- **Website:** [The Testing Academy](https://thetestingacademy.com/)
- **LinkedIn:** [linkedin.com/in/pramoddutta](https://www.linkedin.com/in/pramoddutta/)

---

## 🎯 Project Overview

Build a RAG system that generates test cases from Jira tickets using historical patterns.

---

## 📋 Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                JIRA → TEST CASE RAG                              │
└─────────────────────────────────────────────────────────────────┘

INGESTION FLOW (One-time):
[Jira Export] → [Text Splitter] → [Embeddings] → [Vector Store]
   (CSV)          (chunks)         (OpenAI)       (Chroma)

QUERY FLOW (Per request):
[New Jira Ticket] → [Retriever] → [LLM + Context] → [Test Cases]
     (input)         (similar       (Claude)         (output)
                     tickets)
```

---

## 🛠️ Step-by-Step Build

### Phase 1: Index Historical Data

1. **Export Jira History**
   - Export past tickets + their test cases as CSV
   - Format: `ticket_id, summary, description, test_cases`

2. **Build Ingestion Flow**
   - Add **File Loader** (CSV)
   - Add **Text Splitter** (Recursive, 500 chars)
   - Add **OpenAI Embeddings**
   - Add **Chroma** vector store
   - Connect and run

### Phase 2: Build Query Flow

1. **Add Query Components**
   - **Chat Input**: New ticket description
   - **Chroma Retriever**: Find similar tickets
   - **Prompt Template**:
   
   ```
   Based on similar past tickets and their test cases,
   generate test cases for this new ticket:
   
   NEW TICKET:
   {input}
   
   SIMILAR PAST TICKETS AND THEIR TESTS:
   {context}
   
   Generate comprehensive test cases following the patterns above.
   ```
   
   - **LLM**: Claude or GPT-4
   - **Chat Output**: Generated test cases

2. **Connect the Flow**
   ```
   Chat Input → Retriever → Prompt → LLM → Chat Output
                    ↓
                [Chroma Store]
   ```

---

## 📝 Usage

**Query:**
```
New Feature: User can export their dashboard as PDF

Requirements:
- Export button on dashboard
- PDF should include all widgets
- Respect user's date range filter
```

**Output:**
```markdown
## Test Cases for PDF Export

Based on similar features (CSV Export, Report Generation):

| ID | Test Case | Priority |
|---|---|---|
| TC-01 | Verify Export button is visible on dashboard | P0 |
| TC-02 | Export generates valid PDF file | P0 |
| TC-03 | PDF includes all visible widgets | P0 |
| TC-04 | Date range filter is respected in export | P1 |
| TC-05 | Export works with no data (empty state) | P1 |
| TC-06 | Large dashboard exports without timeout | P1 |
| TC-07 | PDF is readable and well-formatted | P2 |
...
```

---

## 💡 Benefits

- ✅ Learns from your team's patterns
- ✅ Consistent test case quality
- ✅ No training required — just examples
- ✅ Improves as you add more data

---

## 📚 See Also

- [LangFlow Components](ch_05_langflow_components.md)
- [Platform Comparison](../ch_05_platform_comparison.md)
