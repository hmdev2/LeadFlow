# Regras de Negócio

## 1. Objetivo do Documento

Este documento tem como objetivo definir as regras de negócio do **LeadFlow CRM**, descrevendo as condições, restrições e comportamentos esperados para o funcionamento do sistema no MVP.

As regras de negócio complementam os requisitos funcionais, detalhando como determinadas ações devem se comportar dentro do contexto operacional do produto.

Este documento deve servir como referência para desenvolvimento, modelagem de banco de dados, definição de permissões, criação de endpoints, testes, backlog e validação do MVP.

## 2. Contexto

O LeadFlow CRM será utilizado por pequenas equipes comerciais que precisam centralizar o cadastro, acompanhamento e gestão de leads.

O sistema deverá permitir que os usuários cadastrem leads, acompanhem oportunidades em um pipeline Kanban, registrem interações, criem tarefas, consultem indicadores básicos e controlem o acesso às informações conforme o perfil de cada usuário.

No MVP, o sistema atenderá uma organização principal, mas sua estrutura deverá considerar o vínculo entre usuários, leads, tarefas, interações e organização, mantendo o produto preparado para uma possível evolução futura para multi-tenant.

As regras definidas neste documento devem manter o MVP simples, objetivo e coerente com a proposta inicial do produto.

## 3. Perfis Considerados

O MVP do LeadFlow CRM considera três perfis principais de usuário:

| Perfil           | Papel principal                                      |
| ---------------- | ---------------------------------------------------- |
| Administrador    | Gerenciar sistema, usuários e permissões             |
| Gestor Comercial | Gerenciar a operação comercial e acompanhar a equipe |
| Vendedor / SDR   | Atender e acompanhar os próprios leads               |

## 4. Padrão de Identificação das Regras

As regras de negócio serão identificadas pelo prefixo **RN**, seguido de numeração sequencial.

Exemplo:

- **RN001** - Todo lead deve pertencer a uma organização.

- **RN002** - Todo lead deve possuir um status.

- **RN003** - Vendedores acessam apenas leads sob sua responsabilidade.

Cada regra será descrita com:

- Código da regra.

- Nome da regra.

- Descrição.

- Aplicação no sistema.

## 5. Regras de Organização

### RN001 - Todo dado operacional deve pertencer a uma organização

Todo usuário, lead, tarefa, interação, configuração e evento relevante do sistema deve estar vinculado à organização atual.

**Aplicação no sistema:**

- Usuários internos devem possuir vínculo com a organização.

- Leads devem pertencer à organização atual.

- Tarefas devem pertencer à organização atual.

- Interações devem pertencer à organização atual.

- Configurações devem pertencer à organização atual.

- O sistema não deve misturar dados entre organizações, mesmo que o MVP utilize apenas uma organização principal.

### RN002 - O MVP não deve expor gestão de múltiplas organizações

Embora a estrutura do sistema deva estar preparada para uma evolução futura para multi-tenant, o MVP não deve apresentar ao usuário final telas ou fluxos complexos de múltiplas empresas.

**Aplicação no sistema:**

- O Administrador deve visualizar apenas a organização principal.

- A interface deve tratar a organização como a empresa atual.

- Não deve existir no MVP troca de organização, painel de tenants, subdomínios ou cobrança por organização.

- A preparação para multi-tenant deve ser estrutural, não operacional.

### RN003 - A organização atual deve limitar todas as consultas internas

Todas as consultas internas do sistema devem considerar a organização atual do usuário autenticado.

**Aplicação no sistema:**

- Listagens devem retornar apenas dados da organização atual.

- Filtros devem considerar apenas dados da organização atual.

- Dashboards devem calcular apenas dados da organização atual.

- Tarefas e interações devem ser exibidas apenas se pertencerem à organização atual.

## 6. Regras de Usuários e Perfis

### RN004 - Todo usuário interno deve possuir vínculo ativo com a organização

Para acessar a área interna do CRM, o usuário deve possuir um vínculo ativo com a organização atual.

**Aplicação no sistema:**

- Usuários sem vínculo não devem acessar a área interna.

- Usuários com vínculo inativo não devem acessar os dados da organização.

- A inativação do vínculo não deve excluir a conta global do usuário.

### RN005 - Todo vínculo de usuário deve possuir um perfil

Todo usuário vinculado à organização deve possuir um perfil de acesso definido.

**Aplicação no sistema:**

- Os perfis permitidos no MVP são Administrador, Gestor Comercial e Vendedor / SDR.

- O perfil determina quais funcionalidades o usuário pode acessar.

- O perfil determina quais dados o usuário pode visualizar, criar, editar ou movimentar.

- Um usuário não deve operar no sistema sem perfil definido.

### RN006 - Apenas Administradores podem gerenciar usuários

A criação, edição de vínculo, alteração de perfil e inativação de usuários na organização devem ser ações restritas ao Administrador.

**Aplicação no sistema:**

- Gestores Comerciais não devem gerenciar usuários.

- Vendedores / SDR não devem gerenciar usuários.

- O Administrador pode alterar perfil e status do vínculo do usuário na organização.

- Alterações de dados globais da conta devem ser tratadas com cautela.

### RN007 - Usuário inativo não deve acessar dados internos da organização

Quando o vínculo de um usuário com a organização estiver inativo, esse usuário não deve conseguir acessar a área interna da organização.

**Aplicação no sistema:**

- O login pode até validar a conta global do usuário, mas o acesso à organização deve ser bloqueado.

- O usuário inativo não deve visualizar leads, tarefas, interações ou dashboards.

- Dados criados anteriormente pelo usuário devem ser preservados.

## 7. Regras de Leads

### RN008 - Todo lead deve possuir uma organização

Todo lead cadastrado no sistema deve estar vinculado à organização atual.

**Aplicação no sistema:**

- Leads criados pela área interna devem receber a organização atual.

- Leads criados pelo formulário público devem ser vinculados à organização principal do MVP.

- O sistema deve impedir criação de leads sem organização.

### RN009 - Todo lead deve possuir dados mínimos para atendimento

Para que um lead seja considerado válido no MVP, ele deve possuir informações mínimas suficientes para permitir o atendimento comercial.

**Campos mínimos obrigatórios:**

- Nome.

- Pelo menos um dado de contato: e-mail ou telefone.

- Origem.

- Status.

**Aplicação no sistema:**

- O sistema deve impedir cadastro de lead sem nome.

- O sistema deve impedir cadastro de lead sem e-mail e sem telefone.

- O sistema deve impedir cadastro de lead sem origem.

- O sistema deve impedir cadastro de lead sem status.

- Campos como empresa, interesse demonstrado e observações podem ser opcionais no MVP.

- Leads vindos do formulário público também devem respeitar os campos mínimos definidos para captura.

### RN010 - Todo lead deve possuir um status

Todo lead deve possuir um status atual dentro do processo comercial.

**Aplicação no sistema:**

- O status deve representar a etapa atual do lead no pipeline.

- O status deve ser obrigatório.

- O status deve ser atualizado quando o lead for movido no Kanban.

- O status deve ser exibido na listagem, nos detalhes e no dashboard.

### RN011 - Status iniciais do pipeline

Os status iniciais do pipeline no MVP são:

- Novo.

- Em contato.

- Qualificado.

- Proposta enviada.

- Negociação.

- Ganho.

- Perdido.

**Aplicação no sistema:**

- O Kanban deve possuir uma coluna para cada status.

- Todo lead deve aparecer na coluna correspondente ao seu status.

- O dashboard deve utilizar esses status para indicadores básicos.

- A personalização avançada de status não faz parte do MVP.

### RN012 - Todo lead deve possuir uma origem

Todo lead deve possuir uma origem de contato.

**Aplicação no sistema:**

- A origem deve ser obrigatória no cadastro interno.

- A origem deve ser definida automaticamente como Site no formulário público.

- A origem deve ser utilizada em filtros e indicadores.

- Leads sem origem não devem ser considerados válidos no fluxo principal.

### RN013 - Origens iniciais de leads

As origens iniciais disponíveis no MVP são:

- Site.

- Instagram.

- LinkedIn.

- Indicação.

- Google Ads.

- Eventos.

- WhatsApp.

- Outro.

**Aplicação no sistema:**

- Essas origens devem estar disponíveis no cadastro interno de leads.

- A origem Site deve ser aplicada automaticamente para leads do formulário público.

- A origem Outro deve ser usada quando nenhuma das opções principais representar corretamente o canal de entrada.

### RN014 - Lead cadastrado por Vendedor / SDR deve ser atribuído automaticamente a ele

Quando um Vendedor / SDR cadastrar um lead pela área interna, esse lead deve ser atribuído automaticamente ao próprio vendedor.

**Aplicação no sistema:**

- O lead deve aparecer na carteira do vendedor.

- O lead deve aparecer no pipeline individual do vendedor.

- O lead deve ser considerado nos indicadores individuais do vendedor.

- Administrador e Gestor Comercial podem alterar o responsável posteriormente.

### RN015 - Lead cadastrado por Administrador ou Gestor Comercial pode ter responsável definido manualmente

Quando um Administrador ou Gestor Comercial cadastrar um lead, o responsável poderá ser definido durante o cadastro ou posteriormente.

**Aplicação no sistema:**

- O lead pode iniciar com responsável definido.

- O lead pode iniciar sem responsável, se fizer sentido para a operação.

- Leads sem responsável devem ficar visíveis para Administrador e Gestor Comercial.

- Vendedores não devem visualizar leads sem responsável, salvo regra futura.

### RN016 - Leads sem responsável devem ser acompanhados por Administrador e Gestor Comercial

Leads sem responsável não devem ficar ocultos da operação comercial.

**Aplicação no sistema:**

- Administradores devem visualizar leads sem responsável.

- Gestores Comerciais devem visualizar leads sem responsável.

- Deve existir forma de identificar ou filtrar leads sem responsável.

- O objetivo é evitar que oportunidades fiquem esquecidas.

- Vendedores / SDR não devem visualizar leads sem responsável como regra padrão do MVP.

### RN017 - Vendedor / SDR acessa apenas leads atribuídos a ele ou cadastrados por ele

O Vendedor / SDR deve ter acesso restrito aos leads sob sua responsabilidade ou criados por ele.

**Aplicação no sistema:**

- O vendedor não deve visualizar leads de outros vendedores.

- O vendedor não deve editar leads de outros vendedores.

- O vendedor não deve mover no Kanban leads de outros vendedores.

- O vendedor não deve registrar interações em leads fora do seu escopo.

- O vendedor não deve criar tarefas em leads fora do seu escopo.

### RN018 - Administrador pode visualizar e gerenciar todos os leads da organização

O Administrador deve possuir acesso amplo aos leads da organização atual.

**Aplicação no sistema:**

- Pode visualizar todos os leads.

- Pode editar leads.

- Pode atribuir e trocar responsáveis.

- Pode mover leads no Kanban.

- Pode registrar interações.

- Pode criar tarefas.

- Pode arquivar leads.

- Pode reativar leads arquivados.

### RN019 - Gestor Comercial pode visualizar e gerenciar leads da equipe

O Gestor Comercial deve possuir acesso amplo aos leads da equipe comercial.

**Aplicação no sistema:**

- Pode visualizar leads da equipe.

- Pode editar leads da equipe.

- Pode atribuir leads a vendedores.

- Pode trocar responsáveis.

- Pode mover leads da equipe no Kanban.

- Pode visualizar tarefas pendentes e atrasadas da equipe.

- Pode arquivar leads conforme as regras específicas deste documento.

- Pode reativar leads arquivados da equipe, conforme escopo de permissão.

### RN020 - Leads duplicados devem ser tratados de forma operacional

O sistema poderá permitir o cadastro de leads com dados semelhantes, mas deve facilitar a identificação de possíveis duplicidades para evitar confusão operacional.

**Aplicação no sistema:**

- O sistema deve considerar e-mail e telefone como principais dados para identificação de possível duplicidade.

- No MVP, o sistema não precisa impedir automaticamente o cadastro de leads duplicados.

- No MVP, o sistema não precisa realizar mesclagem automática de leads.

- Quando possível, o sistema deve alertar ou facilitar a identificação de leads com e-mail ou telefone já cadastrados.

- Leads duplicados identificados pela equipe poderão ser arquivados por Administrador ou Gestor Comercial, conforme regra de permissão.

- O arquivamento de um lead duplicado deve preservar seu histórico.

## 8. Regras de Responsável pelo Lead

### RN021 - Responsável pelo lead deve ser usuário ativo da organização

O responsável por um lead deve ser um usuário com vínculo ativo na organização atual.

**Aplicação no sistema:**

- Não deve ser possível atribuir lead a usuário inativo.

- Não deve ser possível atribuir lead a usuário sem vínculo com a organização.

- Caso um usuário responsável seja inativado, seus leads devem permanecer preservados e poderão ser redistribuídos por Administrador ou Gestor Comercial.

### RN022 - Apenas Administrador e Gestor Comercial podem trocar responsável

A troca de responsável por um lead deve ser restrita ao Administrador e ao Gestor Comercial.

**Aplicação no sistema:**

- Vendedor / SDR não deve trocar o responsável do lead.

- Administrador pode trocar responsável de qualquer lead da organização.

- Gestor Comercial pode trocar responsável de leads da equipe.

- Toda troca de responsável deve gerar registro automático no histórico do lead.

### RN023 - Troca de responsável não deve apagar histórico anterior

Quando o responsável por um lead for alterado, o histórico anterior deve ser preservado.

**Aplicação no sistema:**

- Interações anteriores devem continuar vinculadas ao lead.

- Tarefas anteriores devem ser preservadas.

- O histórico deve indicar a troca de responsável.

- O novo responsável deve conseguir entender o contexto anterior do atendimento.

### RN024 - Leads de usuário inativo devem permanecer acessíveis para gestão

Quando um usuário for inativado na organização, seus leads não devem ser excluídos.

**Aplicação no sistema:**

- Os leads continuam pertencendo à organização.

- Administrador e Gestor Comercial devem conseguir visualizar esses leads.

- Os leads podem ser redistribuídos para outro responsável ativo.

- O histórico deve permanecer preservado.

## 9. Regras de Movimentação no Pipeline

### RN025 - Movimentar lead no Kanban atualiza seu status

Quando um lead for movido entre colunas do Kanban, seu status deve ser atualizado automaticamente.

**Aplicação no sistema:**

- A coluna de destino representa o novo status.

- A listagem e a página de detalhes devem refletir o novo status.

- O dashboard deve considerar o status atualizado.

- A movimentação deve respeitar as permissões do usuário.

### RN026 - Mudança de status deve gerar evento automático no histórico

Toda mudança de status do lead deve gerar um registro automático no histórico.

**Aplicação no sistema:**

- O evento deve indicar o status anterior.

- O evento deve indicar o novo status.

- O evento deve indicar o usuário responsável pela mudança, quando aplicável.

- O evento deve registrar data e hora.

- O histórico não deve depender apenas de registros manuais.

### RN027 - Leads ganhos ou perdidos continuam preservados

Leads marcados como Ganho ou Perdido não devem ser excluídos automaticamente.

**Aplicação no sistema:**

- Leads ganhos continuam disponíveis para consulta.

- Leads perdidos continuam disponíveis para consulta.

- Ambos devem manter histórico, tarefas e interações.

- O sistema pode permitir filtros para visualizar ou ocultar esses leads conforme a tela.

### RN028 - Lead ganho representa oportunidade convertida

O status Ganho deve representar que a oportunidade foi convertida em cliente ou negócio fechado.

**Aplicação no sistema:**

- Leads ganhos devem contar nos indicadores de conversão.

- Leads ganhos não devem ser considerados oportunidades abertas.

- O histórico deve preservar a mudança para Ganho.

### RN029 - Lead perdido representa oportunidade encerrada sem conversão

O status Perdido deve representar que a oportunidade foi encerrada sem conversão.

**Aplicação no sistema:**

- Leads perdidos devem contar nos indicadores de perdas.

- Leads perdidos não devem ser considerados oportunidades abertas.

- O histórico deve preservar a mudança para Perdido.

## 10. Regras de Arquivamento de Leads

### RN030 - Arquivamento deve substituir exclusão definitiva no fluxo comum

No MVP, leads que não devem mais aparecer no fluxo ativo devem ser arquivados, e não excluídos definitivamente.

**Aplicação no sistema:**

- O lead arquivado deve preservar seus dados.

- O histórico deve ser preservado.

- As tarefas e interações devem permanecer vinculadas ao lead.

- A exclusão definitiva não deve ser tratada como ação comum do sistema.

### RN031 - Lead arquivado é lead preservado fora do fluxo ativo

Um lead arquivado representa uma oportunidade que não deve mais aparecer no fluxo comercial ativo, mas que deve continuar preservada para consulta, auditoria e histórico comercial.

**Aplicação no sistema:**

- O lead arquivado não deve aparecer no Kanban padrão.

- O lead arquivado não deve aparecer na listagem padrão de leads ativos.

- O lead arquivado deve preservar dados principais, histórico, tarefas e interações.

- O lead arquivado poderá ser consultado por Administrador e Gestor Comercial, conforme filtros ou tela específica.

- O arquivamento deve gerar evento automático no histórico do lead.

- O termo inativo não deve ser usado como estado separado no MVP, salvo decisão técnica ou futura regra complementar.

### RN032 - Administrador pode arquivar qualquer lead da organização

O Administrador pode arquivar qualquer lead da organização atual.

**Aplicação no sistema:**

- A ação deve respeitar a organização atual.

- A ação deve gerar evento automático no histórico.

- O lead deve sair do fluxo ativo padrão.

- O lead deve continuar disponível para consulta administrativa, conforme filtros ou telas específicas.

### RN033 - Gestor Comercial pode arquivar leads da equipe em situações operacionais

O Gestor Comercial pode arquivar leads da equipe quando a ação estiver relacionada à organização operacional do pipeline.

**Aplicação no sistema:**

O Gestor Comercial poderá arquivar um lead quando:

- O lead estiver duplicado operacionalmente.

- O lead não possuir potencial comercial após análise.

- O lead tiver sido encerrado como perdido e não precisar permanecer no fluxo ativo.

- O lead tiver sido cadastrado por engano.

- O lead estiver sem movimentação e for decidido que deve sair do fluxo ativo.

- O lead pertencer à equipe sob acompanhamento do gestor.

### RN034 - Gestor Comercial não deve arquivar leads fora do escopo da equipe

O Gestor Comercial não deve arquivar leads que não estejam dentro do seu escopo de acompanhamento.

**Aplicação no sistema:**

- O gestor deve atuar apenas sobre leads da equipe.

- O sistema deve impedir arquivamento de leads fora da organização atual.

- O sistema deve impedir arquivamento de leads sem permissão.

### RN035 - Vendedor / SDR não pode arquivar leads

No MVP, o Vendedor / SDR não deve arquivar leads.

**Aplicação no sistema:**

- O vendedor pode alterar status dos seus próprios leads conforme permissão.

- O vendedor pode registrar interações.

- O vendedor pode criar tarefas.

- A retirada do lead do fluxo ativo deve ficar restrita ao Administrador e ao Gestor Comercial, conforme regra.

### RN036 - Arquivamento deve gerar registro automático no histórico

Toda ação de arquivar um lead deve gerar evento automático no histórico do lead.

**Aplicação no sistema:**

- O evento deve indicar que o lead foi arquivado.

- O evento deve indicar o usuário responsável pela ação.

- O evento deve registrar data e hora.

- O evento pode incluir motivo, se o sistema possuir esse campo no MVP.

- O histórico deve permitir entender por que o lead saiu do fluxo ativo.

### RN037 - Lead arquivado não deve aparecer no fluxo ativo padrão

Leads arquivados não devem aparecer nas listagens e no Kanban padrão de leads ativos.

**Aplicação no sistema:**

- O Kanban padrão deve priorizar leads ativos.

- A listagem padrão deve priorizar leads ativos.

- Leads arquivados podem ser acessados por filtros ou área específica.

- Dashboards operacionais devem considerar apenas leads ativos, salvo indicador específico.

### RN038 - Lead arquivado pode ser reativado por usuário autorizado

Um lead arquivado poderá ser reativado por usuário autorizado quando voltar a fazer parte do fluxo comercial ativo.

**Aplicação no sistema:**

- Administrador pode reativar leads arquivados da organização atual.

- Gestor Comercial pode reativar leads arquivados da equipe, conforme escopo de permissão.

- Vendedor / SDR não deve reativar leads arquivados no MVP.

- Ao ser reativado, o lead deve voltar ao status que possuía antes do arquivamento, salvo decisão diferente registrada em regra futura.

- A reativação deve gerar evento automático no histórico do lead.

- Dados, histórico, tarefas e interações anteriores devem permanecer preservados.

## 11. Regras de Histórico e Interações

### RN039 - Histórico do lead deve combinar registros manuais e automáticos

O histórico do lead deve conter tanto interações manuais registradas por usuários quanto eventos automáticos gerados pelo sistema.

**Aplicação no sistema:**

- Interações manuais registram contatos e observações.

- Eventos automáticos registram mudanças relevantes feitas no sistema.

- Ambos devem aparecer no histórico do lead.

- O histórico deve preservar a rastreabilidade do atendimento.

### RN040 - Interações manuais devem registrar usuário, data e tipo

Toda interação manual registrada em um lead deve conter informações mínimas para rastreabilidade.

**Aplicação no sistema:**

- Tipo da interação.

- Descrição.

- Usuário que registrou.

- Data e hora do registro.

- Lead relacionado.

- Organização relacionada.

### RN041 - Tipos de interação manual no MVP

Os tipos de interação manual previstos no MVP são:

- Ligação.

- WhatsApp.

- E-mail.

- Reunião.

- Observação interna.

- Envio de proposta.

- Outro.

**Aplicação no sistema:**

- O usuário deve selecionar um tipo ao registrar a interação.

- O tipo deve facilitar leitura do histórico.

- O tipo não representa integração real com ferramentas externas.

### RN042 - Eventos automáticos obrigatórios no histórico

O sistema deve registrar automaticamente no histórico do lead os seguintes eventos:

- Mudança de status.

- Troca de responsável.

- Arquivamento do lead.

- Reativação do lead, quando aplicável.

**Aplicação no sistema:**

- Cada evento deve indicar o que foi alterado.

- Cada evento deve indicar o usuário responsável pela ação, quando aplicável.

- Cada evento deve indicar data e hora.

- Eventos automáticos devem ser exibidos junto com as interações manuais.

### RN043 - Criação de tarefa pode gerar evento automático no histórico

A criação de tarefa relacionada a um lead pode gerar evento automático no histórico quando for considerada relevante para o acompanhamento comercial.

**Aplicação no sistema:**

- O sistema pode registrar que uma tarefa foi criada.

- O evento deve indicar título ou resumo da tarefa.

- O evento deve indicar responsável e data de vencimento, quando aplicável.

- Essa regra pode ser implementada de forma simples no MVP.

### RN044 - Histórico não deve ser apagado em alterações de lead

Alterações em dados do lead não devem apagar o histórico existente.

**Aplicação no sistema:**

- Interações anteriores devem permanecer.

- Eventos automáticos anteriores devem permanecer.

- Mudanças de responsável não devem remover histórico antigo.

- Arquivamento não deve apagar histórico.

- Reativação não deve apagar histórico.

## 12. Regras de Tarefas e Lembretes

### RN045 - Toda tarefa deve estar vinculada a um lead

No MVP, as tarefas devem ser relacionadas a leads.

**Aplicação no sistema:**

- Não deve existir tarefa solta sem lead relacionado.

- A tarefa deve pertencer à mesma organização do lead.

- A tarefa deve aparecer na página de detalhes do lead.

### RN046 - Toda tarefa deve possuir responsável

Toda tarefa deve possuir um usuário responsável por sua execução.

**Aplicação no sistema:**

- O responsável deve possuir vínculo ativo com a organização.

- Administrador e Gestor Comercial podem criar tarefas para vendedores.

- Vendedor / SDR pode criar tarefas para seus próprios leads.

- O responsável pela tarefa deve conseguir visualizá-la conforme seu escopo.

### RN047 - Toda tarefa deve possuir data de vencimento

A data de vencimento é obrigatória para que o sistema consiga identificar pendências e atrasos.

**Aplicação no sistema:**

- A tarefa deve possuir uma data de vencimento.

- A data de vencimento será usada como lembrete simples.

- O MVP não exige notificação automática.

- O sistema deve indicar visualmente tarefas vencidas.

### RN048 - Status iniciais de tarefa

Os status iniciais de tarefa no MVP são:

- Pendente.

- Concluída.

**Aplicação no sistema:**

- Toda nova tarefa deve iniciar como Pendente.

- Ao ser marcada como concluída, deve registrar data de conclusão.

- Tarefas concluídas não devem ser consideradas atrasadas.

### RN049 - Tarefa atrasada é tarefa pendente com vencimento ultrapassado

Uma tarefa deve ser considerada atrasada quando estiver pendente e sua data de vencimento tiver passado.

**Aplicação no sistema:**

- Tarefas concluídas não devem ser consideradas atrasadas.

- Tarefas pendentes com vencimento futuro não devem ser consideradas atrasadas.

- A identificação de atraso deve aparecer para usuários autorizados.

- O dashboard pode utilizar essa regra para indicadores.

### RN050 - Vendedor / SDR gerencia tarefas dos próprios leads

O Vendedor / SDR pode criar, visualizar, editar e concluir tarefas relacionadas aos seus próprios leads.

**Aplicação no sistema:**

- O vendedor não deve gerenciar tarefas de leads de outros vendedores.

- O vendedor não deve criar tarefas para outros usuários.

- O vendedor deve visualizar tarefas pendentes e atrasadas dos próprios leads.

### RN051 - Gestor Comercial acompanha tarefas da equipe

O Gestor Comercial deve conseguir visualizar tarefas pendentes e atrasadas da equipe.

**Aplicação no sistema:**

- O gestor pode acompanhar follow-ups da equipe.

- O gestor pode criar tarefas para vendedores.

- O gestor pode identificar responsáveis por tarefas.

- O gestor pode usar essas informações para priorizar oportunidades.

### RN052 - Administrador possui acesso amplo às tarefas

O Administrador pode visualizar e gerenciar tarefas da organização atual.

**Aplicação no sistema:**

- Pode visualizar tarefas pendentes.

- Pode visualizar tarefas atrasadas.

- Pode criar tarefas.

- Pode criar tarefas para vendedores.

- Pode concluir ou editar tarefas conforme necessidade administrativa.

### RN053 - Tarefas pendentes não devem ser apagadas automaticamente ao encerrar ou arquivar um lead

Tarefas pendentes vinculadas a leads ganhos, perdidos ou arquivados devem ser preservadas pelo sistema.

**Aplicação no sistema:**

- Ao marcar um lead como Ganho, o sistema não deve apagar tarefas pendentes automaticamente.

- Ao marcar um lead como Perdido, o sistema não deve apagar tarefas pendentes automaticamente.

- Ao arquivar um lead, o sistema não deve apagar tarefas pendentes automaticamente.

- O sistema não deve concluir tarefas automaticamente apenas porque o lead foi ganho, perdido ou arquivado.

- As tarefas devem continuar disponíveis para consulta conforme regra de visualização.

- Em versão futura, o sistema poderá sugerir encerramento ou revisão de tarefas pendentes ao ganhar, perder ou arquivar um lead.

- No MVP, a decisão de concluir uma tarefa deve ser feita por usuário autorizado.

## 13. Regras do Formulário Público de Captura

### RN054 - Formulário público deve criar lead automaticamente

Quando o formulário público for enviado com dados válidos, o sistema deve criar automaticamente um lead no CRM.

**Aplicação no sistema:**

- O visitante não precisa estar autenticado.

- O lead deve ser criado na organização principal do MVP.

- O lead deve ficar disponível na área interna para usuários autorizados.

- O envio deve exibir confirmação visual ao visitante.

### RN055 - Lead do formulário público deve entrar com origem Site

Todo lead criado pelo formulário público deve receber automaticamente a origem Site.

**Aplicação no sistema:**

- O visitante não deve selecionar a origem.

- A origem deve aparecer nos detalhes do lead.

- A origem deve ser utilizada nos filtros e indicadores.

- Essa regra simula um fluxo real de captação pelo site.

### RN056 - Lead do formulário público deve entrar com status Novo

Todo lead criado pelo formulário público deve iniciar com status Novo.

**Aplicação no sistema:**

- O lead deve aparecer na coluna Novo do Kanban.

- O status pode ser alterado posteriormente por usuário autorizado.

- O lead deve ser considerado como novo nos indicadores aplicáveis.

### RN057 - Lead do formulário público pode iniciar sem responsável

No MVP, leads vindos do formulário público podem ser criados sem responsável definido.

**Aplicação no sistema:**

- Administrador e Gestor Comercial devem visualizar esses leads.

- Deve ser possível atribuir responsável posteriormente.

- Leads sem responsável não devem ficar ocultos da operação.

- Vendedores / SDR não devem visualizar esses leads até que sejam atribuídos a eles.

### RN058 - Formulário público não deve executar automações externas

No MVP, o formulário público não deve disparar integrações externas.

**Aplicação no sistema:**

- Não haverá envio automático de e-mail.

- Não haverá integração com WhatsApp.

- Não haverá integração com ferramentas de marketing.

- Não haverá automação avançada de distribuição.

- O foco é criar o lead no CRM.

## 14. Regras de Dashboard e Indicadores

### RN059 - Dashboard geral deve considerar dados da organização

O dashboard geral deve exibir indicadores calculados com base nos dados da organização atual.

**Aplicação no sistema:**

- Administrador visualiza indicadores gerais da organização.

- Gestor Comercial visualiza indicadores da equipe.

- Os dados devem respeitar permissões e escopo de acesso.

- Indicadores não devem considerar dados de outra organização.

### RN060 - Dashboard individual deve respeitar escopo do usuário

O dashboard individual deve exibir apenas dados permitidos para o usuário autenticado.

**Aplicação no sistema:**

- Vendedor / SDR visualiza indicadores dos seus próprios leads.

- Gestor Comercial pode visualizar indicadores individuais quando aplicável.

- Administrador pode visualizar indicadores individuais quando aplicável.

- O dashboard individual não deve revelar dados de leads sem permissão.

### RN061 - Taxa de conversão deve considerar leads ganhos

No MVP, a taxa de conversão deve ser calculada com base nos leads marcados como Ganho em relação ao conjunto de leads considerado pelo indicador.

**Aplicação no sistema:**

- No dashboard geral, considera o escopo geral permitido.

- No dashboard individual, considera apenas leads do usuário.

- Leads perdidos podem ser utilizados para comparação.

- A fórmula exata poderá ser detalhada no documento de métricas ou nos requisitos de dashboard, se necessário.

### RN062 - Tarefas atrasadas devem ser calculadas pela regra de vencimento

O indicador de tarefas atrasadas deve considerar tarefas pendentes cuja data de vencimento já passou.

**Aplicação no sistema:**

- Tarefas concluídas não entram como atrasadas.

- O indicador deve respeitar o escopo do usuário.

- O indicador deve considerar apenas tarefas da organização atual.

## 15. Regras de Permissões

### RN063 - Permissões devem ser aplicadas nas telas e nas ações

O sistema deve aplicar regras de permissão tanto na interface quanto nas ações internas.

**Aplicação no sistema:**

- Um botão não deve aparecer para quem não tem permissão.

- Mesmo que uma ação seja chamada diretamente, o sistema deve validar permissão.

- Endpoints e operações internas devem respeitar o perfil do usuário.

- A permissão deve considerar organização, perfil e escopo do dado.

### RN064 - Vendedor / SDR não deve acessar dados de outros vendedores

O sistema deve impedir que vendedores acessem informações de leads que não pertencem ao seu escopo.

**Aplicação no sistema:**

- A restrição vale para listagem.

- A restrição vale para Kanban.

- A restrição vale para página de detalhes.

- A restrição vale para tarefas.

- A restrição vale para interações.

- A restrição vale para dashboard individual.

### RN065 - Gestor Comercial não deve gerenciar configurações administrativas

O Gestor Comercial pode acompanhar a operação comercial, mas não deve gerenciar configurações administrativas do sistema.

**Aplicação no sistema:**

- Não pode criar usuários.

- Não pode alterar perfis de acesso.

- Não pode gerenciar configurações básicas da organização.

- Pode acompanhar leads, tarefas, responsáveis e pipeline da equipe.

### RN066 - Administrador é o único perfil com acesso às configurações básicas

As configurações básicas da organização devem ser restritas ao Administrador.

**Aplicação no sistema:**

- Apenas Administrador acessa configurações.

- Apenas Administrador edita dados básicos da organização.

- Apenas Administrador visualiza opções administrativas sensíveis.

- Configurações avançadas ficam fora do MVP.

## 16. Regras Fora do Escopo do MVP

### RN067 - O MVP não deve possuir integração real com canais externos

O sistema não deve depender de integrações reais com WhatsApp, e-mail, redes sociais, Google Ads, LinkedIn ou ferramentas externas.

**Aplicação no sistema:**

- Contatos feitos fora do sistema devem ser registrados manualmente.

- O formulário público simula entrada de leads pelo site.

- Integrações reais ficam para versões futuras.

### RN068 - O MVP não deve possuir automações avançadas

O MVP não deve incluir automações avançadas de funil, distribuição automática complexa, notificações externas ou inteligência artificial.

**Aplicação no sistema:**

- Tarefas usam vencimento e indicação visual de atraso.

- Não há push, e-mail automático ou automação externa.

- Não há IA para classificação ou priorização de leads.

- O foco é manter o fluxo principal simples e funcional.

### RN069 - Exclusão definitiva de leads não é fluxo comum do MVP

A exclusão definitiva de leads não deve fazer parte do fluxo operacional comum da primeira versão.

**Aplicação no sistema:**

- Leads devem ser arquivados.

- Dados e histórico devem ser preservados.

- Caso exista exclusão definitiva por necessidade técnica, ela deve ser restrita, excepcional e não priorizada na interface do MVP.

## 17. Critérios Gerais de Validação das Regras

As regras de negócio serão consideradas atendidas quando:

- O sistema restringir corretamente o acesso conforme perfil.

- Leads pertencerem à organização atual.

- Leads possuírem dados mínimos para atendimento.

- Leads possuírem status e origem.

- Vendedores visualizarem apenas seus próprios leads.

- Administradores e Gestores Comerciais conseguirem visualizar leads sem responsável.

- Trocas de status e responsável gerarem histórico automático.

- Arquivamento substituir exclusão definitiva no fluxo comum.

- Leads arquivados puderem ser reativados por usuário autorizado.

- Leads duplicados puderem ser identificados ou tratados operacionalmente.

- Tarefas pendentes e atrasadas forem identificadas corretamente.

- Tarefas pendentes forem preservadas quando leads forem ganhos, perdidos ou arquivados.

- Leads do formulário público entrarem como origem Site e status Novo.

- O dashboard respeitar o escopo de acesso do usuário.

- Dados operacionais forem preservados mesmo em arquivamentos, reativações e trocas de responsável.

## 18. Observações Finais

Este documento define as principais regras de negócio do MVP do LeadFlow CRM.

As regras aqui descritas devem orientar a implementação do sistema, garantindo que o comportamento das funcionalidades esteja alinhado ao escopo aprovado, às personas definidas e aos requisitos funcionais.

O MVP deve priorizar simplicidade, clareza e rastreabilidade, evitando fluxos complexos que não sejam necessários para validar a primeira versão do produto.

As regras foram ajustadas para reduzir ambiguidades operacionais no MVP, especialmente quanto ao uso do termo arquivamento, tratamento de possíveis leads duplicados, definição de campos mínimos obrigatórios, reativação de leads arquivados e preservação de tarefas pendentes em leads ganhos, perdidos ou arquivados.

No MVP, o sistema deverá priorizar preservação de dados e rastreabilidade das ações, evitando exclusões automáticas, conclusões automáticas de tarefas ou comportamentos que removam informações importantes do histórico comercial.

As regras poderão ser refinadas em versões futuras conforme novas necessidades comerciais, operacionais ou técnicas forem identificadas.
