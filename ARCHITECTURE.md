# VORTEX: ARQUITETURA DE MICROSSERVIÇOS E SEGURANÇA (BACK-END)

Este documento define a arquitetura técnica, serviços e o modelo de dados que suportarão o alto nível de seriedade, segurança e rastreabilidade exigidos pelo Projeto VORTEX.

---

## 1. PRINCÍPIOS ARQUITETURAIS

1.  **Imutabilidade:** O Log de Eventos Disciplinares (Auditoria) deve ser imutável (append-only), garantindo que nenhuma punição ou infração possa ser apagada ou alterada.
2.  **Separação de Preocupações:** Uso de arquitetura de microsserviços para isolar funcionalidades críticas (Governança, Biometria, Comunicação).
3.  **Compliance Biométrico:** Dados biométricos (Descritor Biométrico) devem ser **separados** do Banco de Dados principal e **cifrados** em repouso.

---

## 2. SERVIÇOS CRÍTICOS DE MICROSSERVIÇO

| Microsserviço | Função Principal | Tecnologia Base Sugerida |
| :--- | :--- | :--- |
| **Identity Service** | Gerenciamento de `USER_ID`, Acesso 2FA/Biometria, Status de Verificação. | GoLang (para performance e segurança), PostgreSQL. |
| **Biometric Service** | Armazenamento e comparação do **Descritor Biométrico Cifrado**. | Python/ML (para processamento), Banco de Dados NoSQL criptografado (e.g., MongoDB/Vault). |
| **Governance Service** | Interface da Polícia VORTEX, Gestão de Casos (N1-N4), Aplicação de Punição. | Java/Spring Boot (para estabilidade e regras de negócio complexas). |
| **Audit Log Service** | Coleta, armazenamento e consulta de logs de sistema e disciplinares. **Garante Imutabilidade.** | **Apache Kafka** (para streaming e imutabilidade do log) + Banco de Dados de Logs (e.g., ClickHouse). |
| **Stream Service** | Gerenciamento do Feed Principal (`main-feed.html`) e Conteúdo. | Node.js/Redis (para alta velocidade e cache de dados). |

---

## 3. MODELO DE DADOS: GOVERNANÇA (Rigor Técnico)

### A. Tabela: `USERS` (Identity Service)

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `user_id` | UUID (PK) | Identificador Único, usado em todos os logs. |
| `biometric_hash` | VARCHAR(256) | Hash criptográfico do descritor biométrico (não o dado em si). |
| `status` | ENUM | Ativo, Restrito (48h/7d), Banido (N4). |
| `last_governance_level`| INT | Último Nível Disciplinar Aplicado (1 a 4). |

### B. Tabela: `DISCIPLINARY_LOG` (Audit Log Service - Kafka)

Esta tabela (ou tópico Kafka) é **APPEND-ONLY (Imutável)**.

| Campo | Tipo | Descrição |
| :--- | :--- | :--- |
| `log_hash` | SHA-256 (PK) | Hash da linha, prova a integridade. |
| `timestamp_utc` | TIMESTAMP | Carimbo de tempo preciso (UTC). |
| `user_id` | UUID | Usuário que sofreu/executou a ação. |
| `event_type` | ENUM | INFRACTION, PUNISHMENT, ADMIN_ACTION. |
| `punishment_level`| INT | Nível (1-4) se for um evento de PUNIÇÃO. |
| `moderator_id` | UUID | ID do Moderador/Polícia VORTEX que aplicou. |

---
