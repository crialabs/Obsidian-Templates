```nodeflow-list
- nodes
  - reengajamento:Sequência 1 (Re-engajamento)
    - objetivo, o
    - email1, i
    - email2, i
    - email3, i
    - email4, i
  - nutricao:Sequência 2 (Nutrição)
    - objetivo, o
    - emailA, i
    - emailB, i
    - emailC, i
    - emailD, i
  - qualificacao:Sequência 3 (Qualificação)
    - objetivo, o
    - email5, i
    - email6, i
    - email7, i
    - email8, i
    - email9, i
    - email10, i
    - email11, i
  - follow_up:Sequência 4 (Follow-up)
    - objetivo, o
    - email12, i
    - email13, i
    - email14, i
    - email15, i
  - leads_inativos:Leads Inativos
    - lead_data, o
  - novos_leads:Novos Leads
    - lead_data, o
  - todos_leads:Todos os Leads
    - lead_data, o
  - leads_nao_respondem:Leads Não Respondem
    - lead_data, o
- edges
  - leads_inativos,lead_data, reengajamento, email1
  - novos_leads,lead_data, nutricao, emailA
  - todos_leads,lead_data, qualificacao, email5
  - leads_nao_respondem,lead_data, follow_up, email12
  - reengajamento,objetivo, nutricao, objetivo
  - reengajamento,objetivo, qualificacao, objetivo
  - reengajamento,objetivo, follow_up, objetivo
```