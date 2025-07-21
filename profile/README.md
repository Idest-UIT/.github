# Idest
### Ref
<ul>
  <li><a href="https://github.com/livekit/livekit">LiveKit (WebRTC SFU)</a></li>
  <li><a href="https://dolacademy.vn">Dol</a></li>
  <li><a href="https://zim.vn">Zim</a></li>
  <li><a href="https://study4.com">Study4</a></li>
</ul>

// need update diagram
```mermaid
erDiagram
  users ||--o{ student_profiles : has
  users ||--o{ teacher_profiles : has
  users ||--o{ class_members : is
  users ||--o{ class_teachers : teaches
  users ||--o{ sessions : hosts
  users ||--o{ assignments : creates
  users ||--o{ submissions : submits
  users ||--o{ feedback : sends
  users ||--o{ feedback : receives
  users ||--o{ progress : tracks
  users ||--o{ chatbot_sessions : owns

  chatbot_sessions ||--o{ chatbot_logs : contains
  users ||--o{ chatbot_logs : messages

  classes ||--o{ class_members : has
  classes ||--o{ class_teachers : has
  classes ||--o{ sessions : includes
  classes ||--o{ assignments : includes

  assignments ||--o{ assignment_sections : contains
  assignment_sections ||--o{ question_groups : includes
  question_groups ||--o{ questions : includes

  assignments ||--o{ submissions : receives
  submissions ||--o{ question_submissions : has
  submissions ||--o{ ai_grading_logs : logs
  submissions ||--o{ feedback : has

  questions ||--o{ question_submissions : answered

  student_profiles {
    uuid user_id PK
    int target_score
    text current_level
  }

  teacher_profiles {
    uuid user_id PK
    text degree
    text specialization
    text bio
  }

  users {
    uuid id PK
    text full_name
    text email
    text password_hash
    varchar role
    text avatar_url
    boolean is_active
    timestamp created_at
    timestamp updated_at
  }

  classes {
    uuid id PK
    text name
    text description
    boolean is_group
    text invite_code
    jsonb schedule
    uuid created_by
    timestamp created_at
    timestamp updated_at
  }

  class_members {
    uuid id PK
    uuid class_id
    uuid student_id
    timestamp joined_at
    varchar status
  }

  class_teachers {
    uuid id PK
    uuid class_id
    uuid teacher_id
    varchar role
  }

  sessions {
    uuid id PK
    uuid class_id
    uuid host_id
    timestamp start_time
    timestamp end_time
    boolean is_recorded
    text recording_url
    jsonb whiteboard_data
    jsonb metadata
    timestamp created_at
  }

  assignments {
    uuid id PK
    uuid created_by
    uuid class_id
    varchar skill
    text title
    text description
    boolean is_public
    timestamp created_at
  }

  assignment_sections {
    uuid id PK
    uuid assignment_id
    text title
    varchar material_type
    text material_url
    text material_text
    int order_index
  }

  question_groups {
    uuid id PK
    uuid section_id
    varchar question_type
    text instruction
    text body_text
    text image_url
    jsonb list_data
    int order_index
  }

  questions {
    uuid id PK
    uuid group_id
    int number
    text prompt
    jsonb options
    jsonb answer
    jsonb metadata
  }

  submissions {
    uuid id PK
    uuid assignment_id
    uuid student_id
    text file_url
    timestamp submitted_at
    jsonb ai_score
    text feedback
  }

  question_submissions {
    uuid id PK
    uuid submission_id
    uuid question_id
    jsonb answer
    boolean is_correct
    float score
  }

  ai_grading_logs {
    uuid id PK
    uuid submission_id
    varchar ai_tool_used
    jsonb result
    timestamp created_at
  }

  feedback {
    uuid id PK
    uuid from_user_id
    uuid to_user_id
    uuid submission_id
    text message
    timestamp created_at
  }

  progress {
    uuid id PK
    uuid student_id
    varchar skill
    jsonb score_history
    timestamp updated_at
  }

  chatbot_sessions {
    uuid id PK
    uuid user_id
    timestamp started_at
    timestamp ended_at
    jsonb context
  }

  chatbot_logs {
    uuid id PK
    uuid session_id
    uuid user_id
    text question
    text answer
    timestamp created_at
  }
```
