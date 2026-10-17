# System Architecture

## Overview

The proposed workflow allows users to ask business questions in plain English and receive answers based on relational database records.

## Workflow Diagram

```text
flowchart TD
    A["User asks a business question"] --> B["n8n Chat Trigger"]
    B --> C["AI Agent + LLM"]
    C --> D["Inspect database schema"]
    D --> E["Generate SQL query"]
    E --> F["Validate query and permissions"]
    F --> G["Execute read-only query in PostgreSQL"]
    G --> H["Interpret returned results"]
    H --> I["Present answer in plain English"]

    C -. "Ambiguous question" .-> J["Ask user for clarification"]
    J -. "Clarified question" .-> C

    D -. "Required data unavailable" .-> K["Explain limitation to user"]
    G -. "Query error" .-> L["Handle error safely"]
    L --> K
```

## Component Responsibilities

| Component | Responsibility |
|---|---|
| Chat Trigger | Receives the user's question |
| AI Agent and LLM | Interprets intent and coordinates the workflow |
| Schema Inspection | Identifies relevant tables and columns |
| SQL Generation | Produces a query for the requested information |
| Query Validation | Checks that the query follows permitted operations |
| PostgreSQL | Executes the approved query |
| Result Interpretation | Converts database results into a clear response |
| Clarification and Error Handling | Handles ambiguous requests, missing data, and query failures |

## Design Considerations

- Database access should use least-privilege permissions.
- Analytical queries should use read-only access wherever possible.
- Generated SQL should be validated before execution.
- Ambiguous requests should be clarified instead of guessed.
- Responses should reflect actual database results.
- Credentials and confidential database details must not be committed to the repository.

## Implementation Note

This is a conceptual architecture for the portfolio demonstration. The final diagram should be revised to match the actual workflow nodes and controls once the demonstration has been implemented and tested.
