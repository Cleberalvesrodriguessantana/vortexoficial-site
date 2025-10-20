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

## 4. PRÓXIMO MÓDULO CRÍTICO DE GOVERNANÇA

**AUDITORIA DE LOGS IMUTÁVEIS:**

Deve ser a próxima tela a ser detalhada, focando na consulta de logs de sistema (ações de usuários e ações de moderação), garantindo que todas as decisões sejam rastreáveis e inalteráveis (Tecnologia Kafka/Blockchain-like).
