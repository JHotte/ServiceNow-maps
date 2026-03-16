```mermaid

classDiagram
  class HRCase {
    +String number
    +String state
    +String short_description
    +String description
    +Date opened
    +Date closed
    +priority: String
    +addComment(text)
    +close(code, notes)
  }

  class User {
    +String sys_id
    +String name
    +String email
  }

  class Group {
    +String sys_id
    +String name
  }

  class KnowledgeArticle {
    +String number
    +String title
    +String kb_category
    +publish()
  }

  class Attachment {
    +String file_name
    +int sizeKB
    +String content_type
  }

  class SLA {
    +String name
    +Date start
    +Date target
    +bool breached
  }

  class Task {
    +String number
    +String state
    +String short_description
    +assignTo(user)
    +complete()
  }

  User "1" <-- "0..*" HRCase : requester
  User "0..1" <-- "0..*" HRCase : opened_by
  User "0..1" <-- "0..*" HRCase : assigned_to
  Group "0..1" <-- "0..*" HRCase : assignment_group

  HRCase "1" o-- "0..*" Attachment : has >
  HRCase "0..*" --> "0..1" KnowledgeArticle : resolves_with >
  HRCase "1" --> "0..*" SLA : governed_by >
  HRCase "1" --> "0..*" Task : spawns >

  Group "0..1" <-- "0..*" Task : assignment_group
  User "0..1" <-- "0..*" Task : assigned_to
