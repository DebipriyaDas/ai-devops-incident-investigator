
# Database Schema

## investigations

| Column                 | Type      |
| ---------------------- | --------- |
| id                     | UUID      |
| created_at             | timestamp |
| file_name              | text      |
| file_type              | text      |
| uploaded_log           | text      |
| incident_summary       | text      |
| incident_category      | text      |
| root_cause             | text      |
| severity               | text      |
| confidence_score       | float     |
| recommended_resolution | text      |
| historical_insights    | text      |
| recommended_actions    | jsonb     |
| postmortem             | text      |

Primary Key

```
id
```

Recommended Actions stored as:

```json
[
  "Action 1",
  "Action 2"
]
```
