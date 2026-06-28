# Modelagem de Banco de Dados

## 1. Objetivo do Documento

Este documento tem como objetivo definir a modelagem de banco de dados do **LeadFlow CRM**, descrevendo as principais entidades, tabelas, campos, relacionamentos, índices e regras de integridade necessárias para o MVP.

A modelagem de banco de dados deve servir como referência para o desenvolvimento, arquitetura, criação de migrations, implementação de endpoints, construção das telas, elaboração do backlog e planejamento dos testes do sistema.

Este documento traduz os requisitos funcionais, requisitos não funcionais e regras de negócio em uma estrutura de dados organizada, coerente com o escopo aprovado para a primeira versão do produto.

## 2. Contexto da Modelagem

O LeadFlow CRM será um sistema web voltado para pequenas equipes comerciais que precisam centralizar, organizar e acompanhar leads recebidos por diferentes canais.

O MVP deverá permitir autenticação de usuários, cadastro e gerenciamento de leads, pipeline Kanban, página de detalhes do lead, histórico de interações, tarefas de acompanhamento, dashboard básico, formulário público de captura e controle simples de permissões.

No MVP, o sistema atenderá inicialmente uma organização principal. Apesar disso, a modelagem deverá considerar desde o início o vínculo dos dados principais com uma organização, preparando o sistema para uma possível evolução futura para multi-tenant sem exigir uma grande reestruturação.

Essa preparação para multi-tenant não deverá aumentar a complexidade operacional do MVP. A interface continuará simples, tratando a organização como a empresa atual, enquanto a estrutura de banco manterá os vínculos necessários para evolução futura.

## 3. Premissas da Modelagem

A modelagem de banco de dados do LeadFlow CRM deverá seguir as premissas abaixo:

- O sistema deverá possuir uma organização principal no MVP.

- As principais entidades operacionais deverão estar vinculadas a uma organização.

- A conta de usuário deverá ser separada do vínculo do usuário com a organização.

- O perfil de acesso deverá pertencer ao vínculo do usuário com a organização.

- Ações operacionais relacionadas a leads, tarefas e histórico deverão referenciar preferencialmente o vínculo do usuário com a organização, e não apenas a conta global do usuário.

- Os leads deverão pertencer a uma organização.

- Todo lead deverá possuir status e origem.

- Um lead poderá possuir responsável definido ou ficar temporariamente sem responsável.

- Leads vindos do formulário público poderão ser criados sem responsável inicial.

- O histórico do lead deverá preservar registros manuais e eventos automáticos.

- As tarefas deverão estar vinculadas a leads.

- A exclusão definitiva de leads não deverá ser o fluxo comum do MVP.

- Leads arquivados deverão preservar seus dados, tarefas e histórico.

- Leads arquivados deverão manter seu status atual, removendo ambiguidades entre status comercial e arquivamento.

- A modelagem deverá favorecer consultas por organização, responsável, status, origem, e-mail, telefone e datas.

- O banco de dados deverá apoiar os filtros, permissões, dashboard, identificação de possíveis duplicidades e rastreabilidade básica do sistema.

## 4. Convenções de Nomenclatura

A modelagem utilizará nomes de tabelas e campos em inglês, seguindo um padrão comum de desenvolvimento web.

As descrições e regras deste documento serão escritas em português.

Convenções adotadas:

- Nomes de tabelas em inglês, no plural.

- Nomes de campos em inglês, no formato `snake_case`.

- Chaves primárias nomeadas como `id`.

- Chaves estrangeiras nomeadas com o sufixo `_id`.

- Campos de data de criação e atualização nomeados como `created_at` e `updated_at`.

- Campos de arquivamento representados por `archived_at`, quando aplicável.

- Campos relacionados ao vínculo de usuários com a organização deverão usar o sufixo `organization_user_id`.

- Campos de status e tipo representados preferencialmente por valores controlados.

## 5. Visão Geral das Entidades

A modelagem inicial do MVP considera as seguintes entidades principais:

| Entidade | Tabela | Finalidade |
| -------- | ------ | ---------- |
| Organização | `organizations` | Representa a empresa ou organização que utiliza o CRM |
| Usuário | `users` | Representa a conta global de login do usuário |
| Vínculo do usuário | `organization_users` | Representa o vínculo do usuário com uma organização, incluindo perfil e status |
| Lead | `leads` | Representa uma oportunidade comercial ou contato recebido |
| Status do lead | `lead_statuses` | Representa as etapas do pipeline comercial |
| Origem do lead | `lead_sources` | Representa os canais de entrada dos leads |
| Interação do lead | `lead_interactions` | Registra interações manuais e eventos automáticos do histórico do lead |
| Tarefa | `tasks` | Representa tarefas de acompanhamento vinculadas a leads |
| Configurações da organização | `organization_settings` | Armazena configurações básicas da organização |

## 6. Diagrama Conceitual Simplificado

A estrutura conceitual do banco pode ser representada da seguinte forma:

```text
organizations
    ├── organization_users
    │       └── users
    │
    ├── lead_statuses
    ├── lead_sources
    ├── leads
    │       ├── responsible_organization_user_id -> organization_users
    │       ├── created_by_organization_user_id -> organization_users
    │       ├── archived_by_organization_user_id -> organization_users
    │       ├── lead_status_id -> lead_statuses
    │       ├── lead_source_id -> lead_sources
    │       ├── lead_interactions
    │       └── tasks
    │
    └── organization_settings
```

## 7. Tabelas da Modelagem

## 7.1 Tabela `organizations`

A tabela `organizations` deverá armazenar os dados básicos da organização que utiliza o LeadFlow CRM.

No MVP, o sistema utilizará uma organização principal. Mesmo assim, essa tabela é necessária para manter a estrutura preparada para evolução futura para multi-tenant.

| Campo | Tipo sugerido | Obrigatório | Descrição |
| ----- | ------------- | ----------- | --------- |
| id | bigint | Sim | Identificador único da organização |
| name | varchar | Sim | Nome da organização |
| slug | varchar | Não | Identificador textual opcional para uso futuro |
| status | varchar | Sim | Status da organização, como `active` ou `inactive` |
| created_at | timestamp | Sim | Data de criação do registro |
| updated_at | timestamp | Sim | Data da última atualização |

### Observações

- No MVP, deverá existir uma organização principal cadastrada.

- A interface não deverá expor gestão complexa de múltiplas organizações.

- O campo `slug` poderá ser útil futuramente em cenários com subdomínio, rotas públicas ou identificação da organização.

- A inativação de uma organização não faz parte do fluxo operacional comum do MVP.

## 7.2 Tabela `users`

A tabela `users` deverá armazenar a identidade global dos usuários do sistema.

Essa tabela representa a conta de login do usuário, contendo dados que não devem depender diretamente de uma organização específica.

| Campo | Tipo sugerido | Obrigatório | Descrição |
| ----- | ------------- | ----------- | --------- |
| id | bigint | Sim | Identificador único do usuário |
| name | varchar | Sim | Nome do usuário |
| email | varchar | Sim | E-mail utilizado para login |
| password | varchar | Sim | Senha armazenada de forma segura |
| created_at | timestamp | Sim | Data de criação do registro |
| updated_at | timestamp | Sim | Data da última atualização |

### Observações

- O e-mail deverá ser único na tabela `users`.

- A senha nunca deverá ser armazenada em texto puro.

- O Administrador do MVP poderá criar usuários de forma simples pela interface, mas a estrutura deverá preservar a separação entre conta global e vínculo organizacional.

- Em uma evolução futura, um mesmo usuário poderá estar vinculado a mais de uma organização com perfis diferentes.

## 7.3 Tabela `organization_users`

A tabela `organization_users` deverá representar o vínculo entre usuários e organizações.

Essa tabela é responsável por armazenar o perfil de acesso do usuário dentro da organização, bem como o status desse vínculo.

| Campo | Tipo sugerido | Obrigatório | Descrição |
| ----- | ------------- | ----------- | --------- |
| id | bigint | Sim | Identificador único do vínculo |
| organization_id | bigint | Sim | Organização à qual o usuário está vinculado |
| user_id | bigint | Sim | Usuário vinculado à organização |
| role | varchar | Sim | Perfil do usuário na organização |
| status | varchar | Sim | Status do vínculo, como `active` ou `inactive` |
| created_at | timestamp | Sim | Data de criação do vínculo |
| updated_at | timestamp | Sim | Data da última atualização |

### Valores iniciais para `role`

| Valor | Descrição |
| ----- | --------- |
| admin | Administrador |
| commercial_manager | Gestor Comercial |
| salesperson | Vendedor / SDR |

### Valores iniciais para `status`

| Valor | Descrição |
| ----- | --------- |
| active | Usuário ativo na organização |
| inactive | Usuário inativo na organização |

### Observações

- Um usuário não deverá possuir mais de um vínculo com a mesma organização.

- O vínculo deverá determinar as permissões do usuário dentro da organização.

- A inativação do vínculo não deverá excluir a conta global do usuário.

- Usuários inativos na organização não deverão acessar os dados internos dessa organização.

- A estrutura permite que futuramente um mesmo usuário atue em organizações diferentes com perfis diferentes.

- Campos operacionais de responsável, criação, conclusão ou arquivamento deverão apontar preferencialmente para `organization_users.id`, garantindo que a ação esteja associada ao usuário dentro da organização correta.

## 7.4 Tabela `lead_statuses`

A tabela `lead_statuses` deverá armazenar os status disponíveis para o pipeline comercial da organização.

No MVP, os status serão padronizados, mas a existência dessa tabela permite melhor organização da modelagem e facilita uma futura evolução para configuração de pipeline.

| Campo | Tipo sugerido | Obrigatório | Descrição |
| ----- | ------------- | ----------- | --------- |
| id | bigint | Sim | Identificador único do status |
| organization_id | bigint | Sim | Organização à qual o status pertence |
| name | varchar | Sim | Nome exibido do status |
| key | varchar | Sim | Identificador interno do status |
| position | integer | Sim | Ordem de exibição no Kanban |
| is_default | boolean | Sim | Indica se é um status padrão do sistema |
| created_at | timestamp | Sim | Data de criação do registro |
| updated_at | timestamp | Sim | Data da última atualização |

### Status iniciais

| Nome | Chave sugerida | Ordem |
| ---- | -------------- | ----- |
| Novo | new | 1 |
| Em contato | contacted | 2 |
| Qualificado | qualified | 3 |
| Proposta enviada | proposal_sent | 4 |
| Negociação | negotiation | 5 |
| Ganho | won | 6 |
| Perdido | lost | 7 |

### Observações

- Todo lead deverá possuir um status válido.

- A movimentação no Kanban deverá atualizar o status atual do lead.

- No MVP, não haverá personalização avançada do pipeline.

- A tabela permite que os status sejam utilizados em filtros, listagens, Kanban e dashboard.

- O arquivamento de um lead não deverá alterar seu status comercial no MVP. Um lead arquivado deverá manter o `lead_status_id` atual e ser retirado do fluxo ativo por meio do campo `archived_at`.

## 7.5 Tabela `lead_sources`

A tabela `lead_sources` deverá armazenar as origens disponíveis para cadastro e classificação dos leads.

No MVP, as origens serão padronizadas, mas a tabela facilita filtros, indicadores e evolução futura.

| Campo | Tipo sugerido | Obrigatório | Descrição |
| ----- | ------------- | ----------- | --------- |
| id | bigint | Sim | Identificador único da origem |
| organization_id | bigint | Sim | Organização à qual a origem pertence |
| name | varchar | Sim | Nome exibido da origem |
| key | varchar | Sim | Identificador interno da origem |
| is_default | boolean | Sim | Indica se é uma origem padrão do sistema |
| created_at | timestamp | Sim | Data de criação do registro |
| updated_at | timestamp | Sim | Data da última atualização |

### Origens iniciais

| Nome | Chave sugerida |
| ---- | -------------- |
| Site | site |
| Instagram | instagram |
| LinkedIn | linkedin |
| Indicação | referral |
| Google Ads | google_ads |
| Eventos | events |
| WhatsApp | whatsapp |
| Outro | other |

### Observações

- Todo lead deverá possuir uma origem válida.

- Leads criados pelo formulário público deverão receber automaticamente a origem `Site`.

- As origens deverão ser utilizadas nos filtros e indicadores do dashboard.

- No MVP, não haverá personalização avançada de origens, salvo decisão posterior.

## 7.6 Tabela `leads`

A tabela `leads` deverá armazenar os dados principais das oportunidades comerciais cadastradas no CRM.

Cada lead deverá estar vinculado a uma organização, possuir status, possuir origem e poderá ter um responsável pelo atendimento.

| Campo | Tipo sugerido | Obrigatório | Descrição |
| ----- | ------------- | ----------- | --------- |
| id | bigint | Sim | Identificador único do lead |
| organization_id | bigint | Sim | Organização à qual o lead pertence |
| lead_status_id | bigint | Sim | Status atual do lead no pipeline |
| lead_source_id | bigint | Sim | Origem do contato |
| responsible_organization_user_id | bigint | Não | Vínculo organizacional responsável pelo atendimento |
| created_by_organization_user_id | bigint | Não | Vínculo organizacional que cadastrou o lead, quando aplicável |
| name | varchar | Sim | Nome do lead |
| email | varchar | Não | E-mail do lead |
| phone | varchar | Não | Telefone do lead |
| company | varchar | Não | Empresa do lead |
| interest | text | Não | Interesse demonstrado pelo lead |
| notes | text | Não | Observações gerais sobre o lead |
| capture_channel | varchar | Sim | Canal de cadastro do lead, como `internal` ou `public_form` |
| ip_address | varchar | Não | Endereço IP de origem quando o lead for criado pelo formulário público, se tecnicamente adequado |
| user_agent | text | Não | Identificação básica do navegador/dispositivo quando o lead for criado pelo formulário público, se útil para diagnóstico ou proteção contra abuso |
| archived_at | timestamp | Não | Data de arquivamento do lead |
| archived_by_organization_user_id | bigint | Não | Vínculo organizacional que arquivou o lead |
| archived_reason | text | Não | Motivo do arquivamento, quando informado |
| created_at | timestamp | Sim | Data de criação do registro |
| updated_at | timestamp | Sim | Data da última atualização |

### Valores iniciais para `capture_channel`

| Valor | Descrição |
| ----- | --------- |
| internal | Lead criado pela área interna do CRM |
| public_form | Lead criado pelo formulário público de captura |

### Observações

- Todo lead deverá possuir `organization_id`.

- Todo lead deverá possuir `lead_status_id`.

- Todo lead deverá possuir `lead_source_id`.

- O lead deverá possuir nome e pelo menos um dado de contato: e-mail ou telefone.

- O campo `responsible_organization_user_id` poderá ser nulo, principalmente para leads vindos do formulário público.

- Quando um Vendedor / SDR cadastrar um lead pela área interna, o campo `responsible_organization_user_id` deverá receber o vínculo organizacional ativo desse vendedor.

- Quando o lead for criado pelo formulário público, o campo `capture_channel` deverá receber `public_form`.

- Os campos `ip_address` e `user_agent` deverão ser opcionais e usados apenas como apoio técnico para diagnóstico, rastreio básico e proteção contra abuso, sem expor essas informações ao usuário final.

- Leads sem responsável deverão ser visíveis para Administrador e Gestor Comercial.

- Leads arquivados não deverão aparecer no fluxo ativo padrão.

- O arquivamento não deverá apagar dados, tarefas ou histórico do lead.

- No MVP, o arquivamento não deverá alterar o `lead_status_id`. O lead arquivado deverá manter seu status comercial atual, e a reativação deverá apenas remover `archived_at`, `archived_by_organization_user_id` e, se aplicável, o motivo de arquivamento.

- O campo `archived_reason` deverá ser opcional e poderá registrar motivos como duplicidade, ausência de potencial comercial, cadastro por engano, oportunidade parada ou encerramento operacional.

## 7.7 Tabela `lead_interactions`

A tabela `lead_interactions` deverá armazenar o histórico do lead, incluindo interações manuais registradas pelos usuários e eventos automáticos gerados pelo sistema.

Essa tabela será essencial para preservar o contexto do atendimento comercial e garantir rastreabilidade das ações importantes.

| Campo | Tipo sugerido | Obrigatório | Descrição |
| ----- | ------------- | ----------- | --------- |
| id | bigint | Sim | Identificador único da interação ou evento |
| organization_id | bigint | Sim | Organização à qual o registro pertence |
| lead_id | bigint | Sim | Lead relacionado ao registro |
| organization_user_id | bigint | Não | Vínculo organizacional responsável pelo registro ou ação |
| type | varchar | Sim | Tipo da interação ou evento |
| description | text | Sim | Descrição do registro |
| metadata | json | Não | Dados adicionais sobre o evento ou alteração |
| created_at | timestamp | Sim | Data de criação do registro |
| updated_at | timestamp | Sim | Data da última atualização |

### Tipos manuais iniciais

| Valor sugerido | Descrição |
| -------------- | --------- |
| call | Ligação |
| whatsapp | WhatsApp |
| email | E-mail |
| meeting | Reunião |
| internal_note | Observação interna |
| proposal_sent | Envio de proposta |
| other | Outro |

### Eventos automáticos iniciais

| Valor sugerido | Descrição |
| -------------- | --------- |
| status_changed | Mudança de status |
| responsible_changed | Troca de responsável |
| lead_archived | Arquivamento do lead |
| lead_reactivated | Reativação do lead |
| task_created | Criação de tarefa relevante, quando aplicável |

### Observações

- O histórico deverá combinar registros manuais e automáticos.

- Mudanças de status deverão gerar evento automático.

- Trocas de responsável deverão gerar evento automático.

- Arquivamento e reativação de leads deverão gerar evento automático.

- O campo `metadata` poderá armazenar informações como status anterior, novo status, responsável anterior, novo responsável, motivo do arquivamento ou dados resumidos de uma tarefa.

- O histórico não deverá ser apagado quando o lead for editado, arquivado, reativado ou tiver seu responsável alterado.

- O campo `organization_user_id` poderá ser nulo em eventos automáticos sem usuário autenticado, mas ações internas feitas por usuários deverão registrar o vínculo organizacional responsável.

## 7.8 Tabela `tasks`

A tabela `tasks` deverá armazenar as tarefas de acompanhamento relacionadas aos leads.

As tarefas servirão para organizar follow-ups, retornos, reuniões, envio de propostas e outras ações comerciais necessárias durante o acompanhamento da oportunidade.

| Campo | Tipo sugerido | Obrigatório | Descrição |
| ----- | ------------- | ----------- | --------- |
| id | bigint | Sim | Identificador único da tarefa |
| organization_id | bigint | Sim | Organização à qual a tarefa pertence |
| lead_id | bigint | Sim | Lead relacionado à tarefa |
| responsible_organization_user_id | bigint | Sim | Vínculo organizacional responsável pela execução da tarefa |
| created_by_organization_user_id | bigint | Não | Vínculo organizacional que criou a tarefa |
| title | varchar | Sim | Título da tarefa |
| description | text | Não | Descrição ou orientação da tarefa |
| due_date | date ou datetime | Sim | Data de vencimento da tarefa |
| status | varchar | Sim | Status atual da tarefa |
| completed_at | timestamp | Não | Data de conclusão da tarefa |
| completed_by_organization_user_id | bigint | Não | Vínculo organizacional que concluiu a tarefa |
| created_at | timestamp | Sim | Data de criação do registro |
| updated_at | timestamp | Sim | Data da última atualização |

### Status iniciais de tarefa

| Valor | Descrição |
| ----- | --------- |
| pending | Pendente |
| completed | Concluída |

### Observações

- Toda tarefa deverá estar vinculada a um lead.

- Toda tarefa deverá pertencer à mesma organização do lead.

- Toda tarefa deverá possuir responsável.

- O responsável deverá ser um vínculo ativo em `organization_users` na mesma organização da tarefa.

- Toda tarefa deverá possuir data de vencimento.

- Uma tarefa pendente deverá ser considerada atrasada quando a data de vencimento tiver passado.

- Tarefas concluídas não deverão ser consideradas atrasadas.

- Tarefas pendentes não deverão ser apagadas automaticamente quando um lead for ganho, perdido ou arquivado.

- No MVP, lembretes serão representados pela data de vencimento e indicação visual de atraso, sem notificação automática.

## 7.9 Tabela `organization_settings`

A tabela `organization_settings` deverá armazenar configurações básicas da organização atual.

No MVP, as configurações deverão ser simples e limitadas a necessidades operacionais iniciais.

| Campo | Tipo sugerido | Obrigatório | Descrição |
| ----- | ------------- | ----------- | --------- |
| id | bigint | Sim | Identificador único da configuração |
| organization_id | bigint | Sim | Organização à qual a configuração pertence |
| key | varchar | Sim | Chave da configuração |
| value | text ou json | Não | Valor da configuração |
| created_at | timestamp | Sim | Data de criação do registro |
| updated_at | timestamp | Sim | Data da última atualização |

### Exemplos de configurações possíveis

| Chave | Finalidade |
| ----- | ---------- |
| public_form_enabled | Indicar se o formulário público está ativo |
| default_public_lead_status_id | Status padrão para leads vindos do formulário público |
| default_public_lead_source_id | Origem padrão para leads vindos do formulário público |
| public_form_privacy_notice | Texto simples sobre uso dos dados enviados pelo formulário público |
| public_form_spam_protection_enabled | Indicar se a proteção básica contra abuso está ativa |

### Observações

- Apenas Administradores deverão acessar configurações básicas.

- Configurações avançadas não fazem parte do MVP.

- A tabela poderá apoiar ajustes simples sem exigir mudanças estruturais no banco.

## 8. Relacionamentos entre Entidades

## 8.1 Organização e Usuários

Uma organização poderá possuir vários usuários vinculados por meio da tabela `organization_users`.

Um usuário poderá estar vinculado a uma ou mais organizações em uma evolução futura.

No MVP, o usuário estará vinculado à organização principal.

Relacionamentos:

- `organizations.id` → `organization_users.organization_id`

- `users.id` → `organization_users.user_id`

## 8.2 Organização e Leads

Uma organização poderá possuir vários leads.

Cada lead deverá pertencer obrigatoriamente a uma organização.

Relacionamento:

- `organizations.id` → `leads.organization_id`

## 8.3 Lead e Status

Cada lead deverá possuir um status atual.

Um status poderá estar associado a vários leads.

Relacionamento:

- `lead_statuses.id` → `leads.lead_status_id`

## 8.4 Lead e Origem

Cada lead deverá possuir uma origem.

Uma origem poderá estar associada a vários leads.

Relacionamento:

- `lead_sources.id` → `leads.lead_source_id`

## 8.5 Lead e Responsável

Um lead poderá possuir um responsável.

O responsável deverá ser representado pelo vínculo ativo do usuário com a organização atual.

Relacionamento:

- `organization_users.id` → `leads.responsible_organization_user_id`

### Observação

A aplicação deverá garantir que o `organization_users.organization_id` do responsável seja igual ao `leads.organization_id` do lead e que o vínculo esteja ativo.

## 8.6 Lead e Criador

Um lead poderá registrar qual vínculo organizacional realizou seu cadastro.

Esse vínculo poderá ser nulo quando o lead for criado pelo formulário público.

Relacionamento:

- `organization_users.id` → `leads.created_by_organization_user_id`

## 8.7 Lead e Arquivamento

Um lead poderá registrar qual vínculo organizacional realizou seu arquivamento.

Esse vínculo será nulo enquanto o lead estiver ativo ou quando o arquivamento não tiver usuário autenticado associado.

Relacionamento:

- `organization_users.id` → `leads.archived_by_organization_user_id`

## 8.8 Lead e Interações

Um lead poderá possuir várias interações e eventos no histórico.

Cada interação deverá pertencer a um único lead.

Relacionamento:

- `leads.id` → `lead_interactions.lead_id`

## 8.9 Interação e Usuário na Organização

Uma interação ou evento poderá registrar o vínculo organizacional responsável pela ação.

Relacionamento:

- `organization_users.id` → `lead_interactions.organization_user_id`

## 8.10 Lead e Tarefas

Um lead poderá possuir várias tarefas.

Cada tarefa deverá estar vinculada a um único lead.

Relacionamento:

- `leads.id` → `tasks.lead_id`

## 8.11 Usuário na Organização e Tarefas

Uma tarefa deverá possuir um vínculo organizacional responsável.

Uma tarefa também poderá registrar o vínculo organizacional que a criou e o vínculo organizacional que a concluiu.

Relacionamentos:

- `organization_users.id` → `tasks.responsible_organization_user_id`

- `organization_users.id` → `tasks.created_by_organization_user_id`

- `organization_users.id` → `tasks.completed_by_organization_user_id`

## 9. Regras de Integridade dos Dados

A modelagem deverá respeitar as seguintes regras de integridade:

- Todo lead deverá possuir organização.

- Todo lead deverá possuir status válido.

- Todo lead deverá possuir origem válida.

- Todo lead deverá possuir nome.

- Todo lead deverá possuir pelo menos e-mail ou telefone.

- Um lead poderá ficar sem responsável quando aplicável.

- Quando houver responsável, ele deverá ser um vínculo ativo da organização.

- O vínculo organizacional responsável pelo lead deverá pertencer à mesma organização do lead.

- Toda tarefa deverá possuir organização.

- Toda tarefa deverá estar vinculada a um lead.

- Toda tarefa deverá pertencer à mesma organização do lead relacionado.

- Toda tarefa deverá possuir responsável.

- O responsável pela tarefa deverá ser um vínculo ativo da organização.

- Toda tarefa deverá possuir data de vencimento.

- Toda interação deverá possuir organização.

- Toda interação deverá estar vinculada a um lead.

- Toda interação deverá pertencer à mesma organização do lead relacionado.

- Todo vínculo de usuário com organização deverá possuir perfil.

- Todo vínculo de usuário com organização deverá possuir status.

- Um mesmo usuário não deverá ser vinculado mais de uma vez à mesma organização.

- Leads arquivados deverão preservar seus dados, tarefas e interações.

- Leads arquivados deverão manter seu status comercial atual.

- Alterações de responsável não deverão apagar histórico anterior.

- Mudanças de status deverão preservar o lead e gerar histórico automático.

- Tarefas não deverão ser apagadas automaticamente quando um lead for ganho, perdido ou arquivado.

- Possíveis duplicidades deverão poder ser identificadas por e-mail ou telefone dentro da organização.

## 10. Índices Recomendados

Para apoiar desempenho adequado no MVP, especialmente em listagens, filtros, Kanban, dashboard e identificação de possíveis duplicidades, recomenda-se a criação de índices nos principais campos de consulta.

## 10.1 Índices em `users`

| Campo | Finalidade |
| ----- | ---------- |
| email | Login e identificação única do usuário |

## 10.2 Índices em `organization_users`

| Campo | Finalidade |
| ----- | ---------- |
| organization_id | Listagem de usuários da organização |
| user_id | Identificação dos vínculos do usuário |
| organization_id, user_id | Evitar vínculo duplicado |
| organization_id, role | Filtros por perfil na organização |
| organization_id, status | Filtros por status do vínculo |

## 10.3 Índices em `lead_statuses`

| Campo | Finalidade |
| ----- | ---------- |
| organization_id | Listagem de status da organização |
| organization_id, key | Identificação interna do status na organização |
| organization_id, position | Ordenação das colunas no Kanban |

## 10.4 Índices em `lead_sources`

| Campo | Finalidade |
| ----- | ---------- |
| organization_id | Listagem de origens da organização |
| organization_id, key | Identificação interna da origem na organização |

## 10.5 Índices em `leads`

| Campo | Finalidade |
| ----- | ---------- |
| organization_id | Restrição por organização |
| lead_status_id | Filtro e Kanban por status |
| lead_source_id | Filtro e dashboard por origem |
| responsible_organization_user_id | Filtro por responsável e dashboard individual |
| created_by_organization_user_id | Identificação de leads cadastrados pelo usuário na organização |
| capture_channel | Separação entre leads internos e leads vindos do formulário público |
| archived_at | Separação entre leads ativos e arquivados |
| created_at | Indicadores por período |
| organization_id, lead_status_id | Consulta do Kanban por organização e status |
| organization_id, responsible_organization_user_id | Carteira individual de vendedor |
| organization_id, archived_at | Listagem padrão de leads ativos |
| organization_id, email | Busca e identificação de possíveis duplicidades por e-mail dentro da organização |
| organization_id, phone | Busca e identificação de possíveis duplicidades por telefone dentro da organização |
| organization_id, capture_channel | Consulta de leads por origem de cadastro, especialmente formulário público |

## 10.6 Índices em `lead_interactions`

| Campo | Finalidade |
| ----- | ---------- |
| organization_id | Restrição por organização |
| lead_id | Listagem do histórico do lead |
| organization_user_id | Rastreabilidade por vínculo organizacional |
| type | Filtro ou leitura por tipo de interação/evento |
| created_at | Ordenação cronológica do histórico |
| lead_id, created_at | Exibição do histórico do lead em ordem cronológica |

## 10.7 Índices em `tasks`

| Campo | Finalidade |
| ----- | ---------- |
| organization_id | Restrição por organização |
| lead_id | Listagem de tarefas por lead |
| responsible_organization_user_id | Tarefas do vínculo organizacional responsável |
| status | Filtro por pendente ou concluída |
| due_date | Identificação de tarefas atrasadas |
| organization_id, responsible_organization_user_id, status | Listagem de tarefas por responsável e status |
| organization_id, status, due_date | Indicador de tarefas atrasadas |

## 11. Regras para Arquivamento e Preservação de Dados

O MVP deverá priorizar preservação de dados e rastreabilidade.

Por isso, a exclusão definitiva de leads não deverá ser tratada como ação comum do sistema.

A modelagem deverá considerar:

- `archived_at` para indicar que o lead saiu do fluxo ativo.

- `archived_by_organization_user_id` para registrar qual vínculo organizacional arquivou o lead.

- `archived_reason` para registrar opcionalmente o motivo do arquivamento.

- Evento automático em `lead_interactions` para registrar o arquivamento.

- Preservação de tarefas e interações relacionadas ao lead arquivado.

- Possibilidade de consulta futura de leads arquivados por Administrador e Gestor Comercial.

Leads arquivados não deverão aparecer no Kanban padrão nem na listagem padrão de leads ativos.

No MVP, o arquivamento não deverá alterar o status comercial do lead. O lead deverá manter o `lead_status_id` atual, e a reativação deverá apenas remover os campos de arquivamento aplicáveis.

Dessa forma, não será necessário utilizar um campo `previous_status_id` no MVP, pois o status anterior não será perdido durante o arquivamento.

## 12. Regras para Histórico do Lead

O histórico do lead deverá ser centralizado na tabela `lead_interactions`.

Essa tabela deverá registrar tanto interações manuais quanto eventos automáticos.

Registros manuais incluem:

- Ligação.

- WhatsApp.

- E-mail.

- Reunião.

- Observação interna.

- Envio de proposta.

- Outro.

Eventos automáticos incluem:

- Mudança de status.

- Troca de responsável.

- Arquivamento do lead.

- Reativação do lead.

- Criação de tarefa relevante, quando aplicável.

A modelagem deverá garantir que o histórico continue vinculado ao lead mesmo após alterações de status, troca de responsável, arquivamento ou reativação.

## 13. Regras para Formulário Público de Captura

O formulário público deverá criar leads automaticamente na organização principal do MVP.

A modelagem deverá permitir que leads criados pelo formulário público tenham:

- `organization_id` definido com a organização principal.

- `lead_source_id` correspondente à origem Site.

- `lead_status_id` correspondente ao status Novo.

- `capture_channel` definido como `public_form`.

- `created_by_organization_user_id` nulo, pois o cadastro foi feito por visitante público.

- `responsible_organization_user_id` nulo, salvo regra futura de atribuição automática.

- `ip_address` e `user_agent` preenchidos opcionalmente, quando forem úteis para diagnóstico técnico, rastreio básico ou proteção contra abuso.

Leads sem responsável deverão ficar disponíveis para Administrador e Gestor Comercial, evitando que oportunidades fiquem ocultas ou sem acompanhamento.

Os campos técnicos de rastreio do formulário público não deverão ser tratados como informações visíveis no fluxo comercial comum. Eles deverão apoiar diagnóstico, segurança básica e prevenção de spam, conforme necessidade técnica do MVP.

## 14. Regras para Dashboard e Indicadores

A modelagem deverá apoiar os indicadores básicos previstos para o dashboard do MVP.

Indicadores esperados e origem dos dados:

| Indicador | Base de cálculo sugerida |
| --------- | ------------------------ |
| Total de leads cadastrados | Contagem em `leads` por organização |
| Leads novos no mês | Contagem em `leads` por `created_at` e status Novo, conforme regra de dashboard |
| Leads ganhos | Contagem em `leads` com status Ganho |
| Leads perdidos | Contagem em `leads` com status Perdido |
| Taxa de conversão | Proporção de leads ganhos dentro do escopo considerado |
| Tarefas atrasadas | Contagem em `tasks` com status Pendente e `due_date` vencida |
| Leads por status | Agrupamento de `leads` por `lead_status_id` |
| Leads por origem | Agrupamento de `leads` por `lead_source_id` |
| Evolução de oportunidades | Agrupamento de leads por data de criação ou mudanças de status registradas no histórico |

Os indicadores deverão respeitar:

- A organização atual.

- O perfil do usuário autenticado.

- O escopo de acesso do usuário.

- A separação entre dashboard geral e dashboard individual.

- A regra de arquivamento, considerando leads ativos por padrão nos indicadores operacionais, salvo quando houver indicador específico para leads arquivados.

## 15. Observações sobre Multi-tenant Futuro

O MVP não deverá implementar multi-tenant completo.

Isso significa que não farão parte desta primeira versão:

- Múltiplas empresas pela interface.

- Troca de organização pelo usuário.

- Subdomínios por empresa.

- Planos de assinatura.

- Cobrança recorrente.

- Painel de tenants.

- Provisionamento automático de organizações.

Apesar disso, a modelagem deverá manter vínculo com `organization_id` nas principais tabelas operacionais.

Entidades que deverão considerar organização desde o MVP:

- Usuários por meio de `organization_users`.

- Leads.

- Status de leads.

- Origens de leads.

- Interações.

- Tarefas.

- Configurações.

Essa decisão reduz o risco de refatoração estrutural caso o LeadFlow evolua futuramente para um modelo SaaS ou multi-tenant.

O uso de campos como `responsible_organization_user_id`, `created_by_organization_user_id` e `completed_by_organization_user_id` reforça essa preparação, pois evita associar ações operacionais apenas ao usuário global e preserva o contexto da organização em que a ação ocorreu.

## 16. Entidades Fora do MVP

As entidades abaixo não deverão ser priorizadas na modelagem inicial do MVP, pois estão relacionadas a funcionalidades fora do escopo aprovado:

- Planos de assinatura.

- Cobranças.

- Pagamentos.

- Integrações com WhatsApp.

- Integrações com e-mail marketing.

- Integrações com redes sociais.

- Mensagens automáticas.

- Chat interno.

- Discador telefônico.

- Propostas com assinatura eletrônica.

- Contratos.

- Módulo financeiro.

- Relatórios analíticos avançados.

- Inteligência artificial.

- Importação em massa por planilha.

- Exportação avançada de dados.

- Auditoria administrativa complexa.

Essas entidades poderão ser avaliadas em versões futuras, conforme evolução do produto e novas necessidades comerciais ou técnicas.

## 17. Critérios Gerais de Validação da Modelagem

A modelagem será considerada adequada para o MVP quando permitir:

- Criar e autenticar usuários.

- Vincular usuários a uma organização com perfil e status.

- Diferenciar Administrador, Gestor Comercial e Vendedor / SDR.

- Cadastrar leads vinculados à organização.

- Registrar status e origem dos leads.

- Permitir leads sem responsável quando aplicável.

- Atribuir leads a vínculos organizacionais ativos.

- Impedir atribuição de leads a usuários sem vínculo ativo com a organização.

- Listar leads por status, origem, responsável e organização.

- Apoiar busca e identificação de possíveis duplicidades por e-mail e telefone.

- Exibir o pipeline Kanban por status.

- Atualizar status ao mover leads no Kanban.

- Registrar histórico manual e eventos automáticos do lead.

- Criar e acompanhar tarefas vinculadas a leads.

- Atribuir tarefas a vínculos organizacionais ativos.

- Identificar tarefas pendentes e atrasadas.

- Gerar indicadores básicos para dashboard.

- Criar leads automaticamente pelo formulário público.

- Registrar dados técnicos opcionais de origem do formulário público, quando aplicável.

- Arquivar leads sem excluir seus dados.

- Registrar opcionalmente o motivo do arquivamento.

- Reativar leads arquivados sem perda de status comercial.

- Preservar tarefas e histórico em leads ganhos, perdidos ou arquivados.

- Respeitar o escopo de acesso por organização e perfil.

- Manter estrutura preparada para evolução futura sem expor complexidade ao usuário final.

## 18. Observações Finais

Este documento define a modelagem inicial de banco de dados do MVP do LeadFlow CRM.

A estrutura proposta prioriza simplicidade, clareza, rastreabilidade e preservação de dados, mantendo coerência com o escopo aprovado, os requisitos funcionais, os requisitos não funcionais e as regras de negócio.

A modelagem considera o conceito de organização desde o início, mesmo que o MVP opere com apenas uma organização principal. Essa decisão prepara o sistema para uma possível evolução futura para multi-tenant, sem comprometer a simplicidade da primeira versão.

A modelagem também evita associar responsabilidades operacionais apenas ao usuário global, preferindo o vínculo organizacional como referência para responsáveis, criadores, concluidores e usuários que executam ações relevantes dentro da organização.

As tabelas, campos e relacionamentos descritos neste documento deverão orientar a criação das migrations, models, endpoints, telas, testes e demais decisões técnicas do desenvolvimento.

A modelagem poderá ser refinada durante a etapa de arquitetura ou implementação, desde que mantenha os comportamentos essenciais definidos neste documento e preserve as regras principais do MVP.
