# VORTEX: WIREFRAME FUNCIONAL DE GOVERNANÇA E CONTROLE (POLÍCIA VORTEX)

Este documento detalha as especificações funcionais e visuais do Painel de Controle, garantindo que a moderação e governança do VORTEX operem com rigor e seriedade (sem elementos "pré-infantis").

---

## 1. MÓDULO: FLUXO DISCIPLINA / CASOS ATIVOS

**Propósito:** Centro de Comando para a Polícia VORTEX aplicar as punições (Nível 1 a Nível 4) e gerenciar casos.

| Elemento | Especificação Técnica | UI/UX (Design de Gestão Avançada) |
| :--- | :--- | :--- |
| **Título/Identificação** | VORTEX GOVERNANCE PANEL v3.1 - MÓDULO: DISCIPLINA | Fonte monoespaçada, Ciano Neon. |
| **Login Admin** | **Acesso Biométrico Duplo Obrigatório (2FA)**. Auditado e registrado no Kafka. | Interface de terminal. Sem links de recuperação social. |
| **Navegação (Sidebar)** | Links de Navegação Crítica: DASHBOARD, LOGS DE AUDITORIA, GESTÃO DE CONVITES, CASOS ATIVOS. | Ícones abstratos. Roxo Magenta quando ativo. |
| **Data Grid (Tabela Principal)** | Tabela de Casos Abertos. Filtrável por Nível (N1-N4) e Status. | Colunas: `CASE_ID`, `USER_ID`, `INFRACTION_HASH`, `NÍVEL ATUAL`, `MODERADOR ALOCADO`, `STATUS`. |

---

## 2. DETALHAMENTO DO CASO (MODAL/POP-UP)

**Aberto ao clicar em uma linha da Tabela Principal.**

- **LOGS BRUTOS:** Exibição imutável do conteúdo reportado (texto/mídia). O hash do log deve ser visível.
- **HISTÓRICO DISCIPLINAR:** Linha do tempo de punições anteriores do `USER_ID` para embasamento legal da nova punição.
- **STATUS DO USUÁRIO:** Conexão em tempo real ao "User Service" para verificar status de banimento/restrição.

---

## 3. BOTÕES DE AÇÃO (PUNIÇÃO - IRREVOGÁVEL)

| Nível | Punição | Cor/Aviso | Propósito |
| :--- | :--- | :--- | :--- |
| **N1** | EMITIR ADVERTÊNCIA | Amarelo | Aviso formal, primeiro registro no histórico disciplinar. |
| **N2** | RESTRINGIR 48 HORAS | Laranja | Bloqueio temporário de comunicação (Chat e Feed). |
| **N3** | RESTRINGIR 7 DIAS | Vermelho | Bloqueio estendido, penalidade por reincidência ou infração grave. |
| **N4** | BANIMENTO PERMANENTE | Vermelho Intenso / Blackout | Revogação de Acesso Biométrico e Social. Requer aprovação de Nível Superior. |

---

---

## 4. MÓDULO: AUDITORIA DE LOGS IMUTÁVEIS

**Propósito:** Fornecer à Polícia VORTEX uma visão inalterável de todas as ações no sistema, garantindo a transparência e rastreabilidade da moderação.

| Elemento | Propósito e Especificação Técnica | UI/UX (Design de Terminal de Dados) |
| :--- | :--- | :--- |
| **Título** | VORTEX GOVERNANCE PANEL / MÓDULO: LOG AUDIT | Fonte monoespaçada, Ciano, enfatizando a natureza técnica e crítica. |
| **Filtros de Busca** | Filtros essenciais para rastreabilidade: `TIMESTAMP RANGE` (UTC), `USER_ID`, `EVENT_TYPE` (e.g., `COMMUNICATION_INFRACTION`, `ADMIN_ACTION`, `BIOMETRIC_FAIL`). | Campos de entrada simples com ícones de lupa e relógio. |
| **Visão Principal** | Tabela de logs em tempo real (ou próximo a ele), simulando uma saída de *stream* de dados de alta velocidade (Kafka). | Logs exibidos em formato de terminal (texto verde/ciano sobre fundo preto). |
| **Formato do Log** | O formato deve ser rigoroso para provar imutabilidade. | Exemplo: `[2025-10-20T17:35:01Z] [USER: 9XF3T8D] [EVENT: MSG_SEND_FAIL] [HASH: 7C4D...90A]` |
| **Detalhe do Hash** | **Prova de Integridade (Blockchain-like):** Cada evento tem um *hash* de segurança (SHA-256) que prova que o log não foi adulterado. | O *hash* é exibido e é clicável para simular a verificação da cadeia de logs. |
| **Alerta de Anomalia** | Destacar ações críticas (e.g., tentativa de acesso não autorizado, reversão de punição por um Admin, falha de integridade de dado). | Logs com anomalias piscam em **Vermelho Intenso** e **Roxo Magenta**. |

---

## CONCLUSÃO DO WIREFRAME VORTEX

Com este módulo, o VORTEX tem a arquitetura de acesso, comunidade e governança 100% especificada no padrão de grandeza e seriedade exigido. O projeto está pronto para a fase de desenvolvimento e implementação dos códigos finais.
