# Requisitos Funcionais

## 1. Objetivo do Documento

Este documento tem como objetivo definir os requisitos funcionais do **LeadFlow CRM**, descrevendo as funcionalidades que deverão ser implementadas na primeira versão funcional do sistema.

Os requisitos funcionais registrados neste documento servem como referência para o desenvolvimento, validação, testes, definição de telas, modelagem de banco de dados, criação de endpoints, elaboração do backlog e planejamento das entregas do MVP.

Este documento deve responder, de forma objetiva, o que o sistema deve permitir que seus usuários façam.

## 2. Contexto

O LeadFlow CRM será um sistema web voltado para o controle e acompanhamento de leads em pequenas equipes comerciais.

Atualmente, os leads recebidos por canais como site, Instagram, LinkedIn, indicação, Google Ads, eventos e WhatsApp ficam distribuídos entre planilhas, conversas, anotações soltas e ferramentas não integradas. Isso dificulta o acompanhamento das oportunidades, gera perda de informações importantes e aumenta o risco de leads serem esquecidos ou mal acompanhados.

O sistema deverá centralizar os leads em um único ambiente, permitir o acompanhamento das oportunidades por meio de um pipeline visual, registrar interações, controlar tarefas de follow-up, exibir indicadores básicos e restringir o acesso às informações conforme o perfil de cada usuário.

No MVP, o sistema será utilizado inicialmente por uma única empresa ou organização. Apesar disso, a estrutura funcional deverá considerar desde o início o conceito de organização, permitindo que usuários, leads, tarefas, interações e configurações sejam associados à organização atual.

Essa abordagem tem como objetivo manter o MVP simples, mas preparado para uma possível evolução futura para multi-tenant, sem exigir uma grande reestruturação conceitual do sistema.

No MVP, essa complexidade estrutural não deverá ser exposta ao usuário final. Para o Administrador, a experiência deverá permanecer simples, com ações como adicionar usuário, definir perfil, definir status e gerenciar configurações básicas da organização.

O MVP do LeadFlow CRM atenderá inicialmente três perfis principais de usuário:

| Perfil | Papel principal |

| ---------------- | ---------------------------------------------------- |

| Administrador | Gerenciar sistema, usuários e permissões |

| Gestor Comercial | Gerenciar a operação comercial e acompanhar a equipe |

| Vendedor / SDR | Atender e acompanhar os próprios leads |

## 3. Padrão de Identificação dos Requisitos

Os requisitos funcionais serão identificados pelo prefixo **RF**, seguido de numeração sequencial.

Exemplo:

- **RF001** - Login de usuários.

- **RF002** - Logout de usuários.

- **RF003** - Proteção de rotas internas.

Cada requisito será descrito com:

- Código do requisito.

- Nome do requisito.

- Descrição.

- Perfis envolvidos.

- Critérios de aceitação.

## 4. Requisitos Funcionais

## 4.1 Autenticação, Organização e Usuários

### RF001 - Login de usuários

O sistema deve permitir que usuários cadastrados acessem a área interna do CRM utilizando e-mail e senha.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O usuário deve conseguir informar e-mail e senha.

- O sistema deve validar as credenciais informadas.

- O sistema deve permitir o acesso apenas quando as credenciais forem válidas.

- O sistema deve impedir o acesso quando as credenciais forem inválidas.

- Após o login, o usuário deve ser direcionado para a área interna do CRM.

- O acesso do usuário deve considerar seu vínculo com a organização atual.

### RF002 - Logout de usuários

O sistema deve permitir que usuários autenticados encerrem sua sessão.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O usuário autenticado deve conseguir sair do sistema.

- Após o logout, a sessão do usuário deve ser encerrada.

- Após o logout, o usuário não deve conseguir acessar rotas internas sem realizar novo login.

- O usuário deve ser redirecionado para a tela de login ou página pública definida pelo sistema.

### RF003 - Proteção de rotas internas

O sistema deve proteger as rotas internas do CRM, permitindo acesso apenas a usuários autenticados e vinculados à organização atual.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- Usuários não autenticados não devem acessar páginas internas do CRM.

- Ao tentar acessar uma rota interna sem autenticação, o usuário deve ser redirecionado para a tela de login.

- Usuários autenticados devem acessar apenas as áreas permitidas conforme seu perfil na organização atual.

- O sistema deve preservar a separação entre área pública e área interna.

- O sistema deve impedir que usuários sem vínculo ativo com a organização atual acessem a área interna.

### RF004 - Organização principal do MVP

O sistema deve operar, no MVP, considerando uma organização principal.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- O sistema deve possuir uma organização principal associada aos dados do MVP.

- Usuários internos devem estar vinculados à organização principal.

- Leads devem estar vinculados à organização principal.

- Tarefas devem estar vinculadas à organização principal.

- Interações devem estar vinculadas à organização principal.

- Configurações devem estar vinculadas à organização principal.

- O MVP não deve exigir gerenciamento de múltiplas organizações pela interface.

### RF005 - Criação ou vinculação de usuários à organização

O sistema deve permitir que o Administrador crie ou vincule usuários à organização atual.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- O Administrador deve conseguir adicionar um usuário à organização atual.

- Caso o e-mail informado ainda não exista como conta de usuário, o sistema deve permitir criar uma nova conta.

- Caso o e-mail informado já exista como conta de usuário, o sistema deve permitir vincular essa conta à organização atual, desde que ainda não exista vínculo ativo ou pendente.

- O sistema deve impedir que o mesmo usuário seja vinculado mais de uma vez à mesma organização.

- O vínculo do usuário com a organização deve possuir um perfil de acesso.

- O vínculo do usuário com a organização deve possuir um status.

- No MVP, a interface deve apresentar esse processo de forma simples, como adição de usuário à empresa atual.

- A operação deve manter a estrutura preparada para futura evolução para convites ou vínculo de usuários existentes.

### RF006 - Criação inicial de conta de usuário pelo Administrador

No MVP, o sistema deve permitir que o Administrador crie uma conta inicial de usuário ao adicioná-lo à organização atual.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- O Administrador deve conseguir informar nome, e-mail, senha inicial ou senha provisória e perfil do usuário na organização.

- O sistema deve validar os campos obrigatórios.

- O sistema deve impedir a criação de uma nova conta com e-mail já existente.

- Se o e-mail já existir, o sistema deve tratar o caso internamente como vínculo de usuário existente à organização atual.

- A conta criada deve ser vinculada automaticamente à organização atual.

- O usuário criado deve conseguir acessar o sistema conforme seu vínculo e perfil na organização.

- A interface não deve exigir que o Administrador entenda a separação técnica entre conta global e vínculo organizacional.

### RF007 - Vínculo de usuário existente à organização

O sistema deve permitir que uma conta de usuário já existente seja vinculada à organização atual.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- O Administrador deve conseguir informar o e-mail de um usuário existente.

- O sistema deve identificar quando o e-mail já pertence a uma conta de usuário.

- O sistema deve permitir vincular o usuário existente à organização atual.

- O sistema deve exigir a definição de um perfil para o usuário dentro da organização atual.

- O sistema deve impedir vínculo duplicado entre o mesmo usuário e a mesma organização.

- O vínculo deve permitir que o mesmo usuário tenha perfis diferentes em organizações diferentes em uma evolução futura.

- No MVP, esse comportamento deve ocorrer de forma transparente para o Administrador.

### RF008 - Gerenciamento do vínculo do usuário com a organização

O sistema deve permitir que o Administrador gerencie o vínculo de usuários com a organização atual.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- O Administrador deve conseguir visualizar usuários vinculados à organização atual.

- O Administrador deve conseguir alterar o perfil do usuário dentro da organização atual.

- O Administrador deve conseguir alterar o status do vínculo do usuário com a organização atual.

- O Administrador não deve ser tratado como proprietário absoluto da identidade global do usuário.

- Alterações no vínculo devem afetar apenas o acesso e as permissões do usuário dentro da organização atual.

- O sistema deve manter separação conceitual entre conta de usuário e vínculo organizacional.

### RF009 - Definição de perfil do usuário na organização

O sistema deve permitir que cada usuário vinculado à organização possua um perfil de acesso dentro dessa organização.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- O sistema deve permitir os perfis Administrador, Gestor Comercial e Vendedor / SDR.

- Todo vínculo ativo entre usuário e organização deve possuir um perfil de acesso.

- O perfil deve determinar quais funcionalidades o usuário pode acessar dentro da organização.

- O perfil deve determinar quais dados o usuário pode visualizar ou modificar dentro da organização.

- Apenas o Administrador deve gerenciar perfis de acesso dos usuários na organização.

- O perfil deve pertencer ao vínculo com a organização, e não apenas à conta global do usuário.

### RF010 - Status do usuário na organização

O sistema deve permitir controlar o status do usuário dentro da organização atual.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- O vínculo do usuário com a organização deve possuir status.

- O sistema deve permitir identificar usuários ativos na organização.

- O sistema deve permitir identificar usuários inativos na organização.

- Usuários inativos não devem conseguir acessar dados internos da organização.

- A inativação deve afetar apenas o vínculo do usuário com a organização atual.

- A inativação não deve excluir a conta global do usuário.

### RF011 - Restrição de edição da identidade global do usuário

O sistema deve evitar que o Administrador edite livremente dados globais da conta de usuário quando essa conta puder ser reutilizada em outras organizações futuramente.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- O Administrador deve gerenciar principalmente o vínculo do usuário com a organização.

- O Administrador deve conseguir alterar perfil e status do usuário na organização.

- Alterações em dados globais, como e-mail de login, devem ser tratadas como operação restrita.

- O sistema deve evitar que uma alteração feita por um Administrador em uma organização afete indevidamente o acesso do usuário em outra organização futura.

- No MVP, ajustes simples de nome poderão existir, mas a modelagem deve permitir separar dados globais da conta e dados do vínculo organizacional.

## 4.2 Gestão de Leads

### RF012 - Cadastro de leads

O sistema deve permitir o cadastro de leads na área interna do CRM, vinculando cada lead à organização atual.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O usuário autorizado deve conseguir cadastrar um novo lead.

- O cadastro deve conter os campos necessários para identificação e acompanhamento da oportunidade.

- O sistema deve validar os campos obrigatórios.

- O lead cadastrado deve ficar disponível na listagem de leads.

- O lead cadastrado deve possuir status inicial.

- O lead cadastrado deve possuir origem.

- O lead cadastrado deve possuir data de cadastro.

- O lead cadastrado deve estar vinculado à organização atual.

- Quando o lead for cadastrado por um Vendedor / SDR, o sistema deve atribuir automaticamente esse vendedor como responsável, salvo regra diferente definida posteriormente.

### RF013 - Campos do lead

O sistema deve permitir que um lead contenha as informações principais necessárias para acompanhamento comercial.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O lead deve conter nome.

- O lead deve conter e-mail.

- O lead deve conter telefone.

- O lead deve permitir informar empresa.

- O lead deve permitir informar origem do contato.

- O lead deve permitir informar interesse demonstrado.

- O lead deve permitir informar responsável pelo atendimento.

- O lead deve permitir registrar observações.

- O lead deve possuir status atual.

- O lead deve possuir data de cadastro.

- O lead deve possuir data da última atualização.

- O lead deve possuir vínculo com a organização atual.

### RF014 - Responsável padrão para leads cadastrados por vendedor

O sistema deve atribuir automaticamente ao Vendedor / SDR a responsabilidade pelos leads cadastrados por ele.

**Perfis envolvidos:**

- Vendedor / SDR.

**Critérios de aceitação:**

- Quando um Vendedor / SDR cadastrar um lead, o lead deve ser atribuído automaticamente a ele.

- O lead cadastrado pelo Vendedor / SDR deve aparecer em sua carteira de leads.

- O lead cadastrado pelo Vendedor / SDR deve aparecer em seu pipeline individual.

- O lead cadastrado pelo Vendedor / SDR deve aparecer em seu dashboard individual, quando aplicável.

- O sistema deve permitir exceções apenas se houver regra específica definida posteriormente.

- Essa regra não impede que Administrador ou Gestor Comercial alterem o responsável posteriormente, conforme permissões.

### RF015 - Edição de leads

O sistema deve permitir a edição de leads conforme as permissões do usuário autenticado na organização atual.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O Administrador deve conseguir editar leads cadastrados na organização atual.

- O Gestor Comercial deve conseguir editar leads da equipe na organização atual.

- O Vendedor / SDR deve conseguir editar apenas leads atribuídos a ele ou cadastrados por ele na organização atual.

- O sistema deve validar os campos obrigatórios durante a edição.

- A data da última atualização deve ser modificada após alterações relevantes no lead.

- O sistema deve impedir edição por usuários sem permissão.

- O sistema deve impedir edição de leads fora da organização atual.

### RF016 - Visualização de leads

O sistema deve permitir a visualização dos dados de um lead conforme as permissões do usuário autenticado.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O Administrador deve conseguir visualizar todos os leads da organização atual.

- O Gestor Comercial deve conseguir visualizar os leads da equipe na organização atual.

- O Vendedor / SDR deve conseguir visualizar leads atribuídos a ele ou cadastrados por ele na organização atual.

- O sistema deve impedir visualização de leads fora do escopo de permissão do usuário.

- O sistema deve impedir visualização de leads fora da organização atual.

- A visualização deve apresentar as principais informações comerciais do lead.

### RF017 - Listagem de leads

O sistema deve permitir a listagem de leads cadastrados no CRM.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O Administrador deve visualizar todos os leads disponíveis na organização atual.

- O Gestor Comercial deve visualizar os leads da equipe na organização atual.

- O Vendedor / SDR deve visualizar apenas os leads atribuídos a ele ou cadastrados por ele.

- A listagem deve exibir dados resumidos dos leads.

- A listagem deve permitir acesso à página de detalhes do lead.

- Leads arquivados ou inativos devem ser tratados conforme regra definida para visualização.

- A listagem deve considerar apenas leads da organização atual.

### RF018 - Busca de leads

O sistema deve permitir a busca de leads por informações principais.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O usuário deve conseguir buscar leads por nome.

- O usuário deve conseguir buscar leads por e-mail.

- O usuário deve conseguir buscar leads por telefone.

- O usuário deve conseguir buscar leads por empresa.

- A busca deve respeitar o escopo de acesso do usuário autenticado.

- O sistema não deve retornar leads que o usuário não tem permissão para visualizar.

- O sistema não deve retornar leads fora da organização atual.

### RF019 - Filtro de leads por status

O sistema deve permitir filtrar leads pelo status atual no processo comercial.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O usuário deve conseguir filtrar leads por status.

- Os status iniciais devem incluir Novo, Em contato, Qualificado, Proposta enviada, Negociação, Ganho e Perdido.

- O filtro deve respeitar as permissões do usuário.

- A listagem deve exibir apenas os leads correspondentes ao status selecionado.

- O filtro deve considerar apenas leads da organização atual.

### RF020 - Filtro de leads por origem

O sistema deve permitir filtrar leads pela origem do contato.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O usuário deve conseguir filtrar leads por origem.

- As origens iniciais devem incluir Site, Instagram, LinkedIn, Indicação, Google Ads, Eventos, WhatsApp e Outro.

- O filtro deve respeitar as permissões do usuário.

- A listagem deve exibir apenas os leads correspondentes à origem selecionada.

- O filtro deve considerar apenas leads da organização atual.

### RF021 - Filtro de leads por responsável

O sistema deve permitir filtrar leads pelo responsável pelo atendimento.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

**Critérios de aceitação:**

- O Administrador deve conseguir filtrar leads por responsável.

- O Gestor Comercial deve conseguir filtrar leads da equipe por responsável.

- O Vendedor / SDR não deve utilizar esse filtro para visualizar leads de outros usuários.

- O filtro deve exibir apenas leads compatíveis com o perfil autenticado.

- O filtro deve considerar apenas responsáveis vinculados à organização atual.

### RF022 - Visualização de leads sem responsável

O sistema deve permitir que Administrador e Gestor Comercial visualizem leads sem responsável definido.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

**Critérios de aceitação:**

- O Administrador deve conseguir visualizar leads sem responsável da organização atual.

- O Gestor Comercial deve conseguir visualizar leads sem responsável da organização atual.

- A listagem de leads deve permitir identificar leads sem responsável.

- O sistema deve permitir filtrar leads sem responsável.

- Leads criados pelo formulário público e sem responsável devem aparecer nessa visualização.

- O objetivo dessa visualização é evitar que oportunidades fiquem esquecidas sem acompanhamento.

- O Vendedor / SDR não deve visualizar leads sem responsável, salvo regra específica definida posteriormente.

### RF023 - Definição de responsável pelo lead

O sistema deve permitir definir um responsável pelo atendimento de um lead.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

**Critérios de aceitação:**

- O Administrador deve conseguir atribuir leads a vendedores vinculados à organização atual.

- O Gestor Comercial deve conseguir atribuir leads a vendedores da equipe.

- O sistema deve permitir que um lead fique sem responsável quando aplicável.

- O sistema deve registrar o responsável atual do lead.

- O Vendedor / SDR não deve atribuir leads a outros usuários.

- O responsável atribuído deve possuir vínculo ativo com a organização atual.

### RF024 - Alteração de responsável pelo lead

O sistema deve permitir a troca do responsável por um lead conforme o perfil do usuário.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

**Critérios de aceitação:**

- O Administrador deve conseguir alterar o responsável de qualquer lead da organização atual.

- O Gestor Comercial deve conseguir alterar o responsável de leads da equipe.

- A alteração deve atualizar o responsável atual do lead.

- A alteração deve respeitar as permissões do usuário autenticado.

- O Vendedor / SDR não deve trocar o responsável por leads.

- O novo responsável deve estar vinculado à organização atual.

- A troca de responsável deve gerar registro automático no histórico do lead.

### RF025 - Arquivamento ou inativação de leads

O sistema deve permitir arquivar ou inativar leads que não devem mais aparecer no fluxo ativo.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial, conforme regra definida.

**Critérios de aceitação:**

- O sistema deve permitir retirar um lead do fluxo ativo sem exclusão definitiva.

- O Administrador deve conseguir arquivar ou inativar leads.

- O Gestor Comercial poderá arquivar ou inativar leads conforme regra de negócio definida posteriormente.

- Leads arquivados ou inativos devem preservar seus dados e histórico.

- O sistema deve evitar exclusão definitiva de leads como fluxo comum do MVP.

- O arquivamento ou inativação deve ocorrer apenas em leads da organização atual.

- O arquivamento ou inativação deve gerar registro automático no histórico do lead.

## 4.3 Pipeline Kanban

### RF026 - Visualização do pipeline Kanban

O sistema deve permitir a visualização dos leads em um pipeline visual no formato Kanban.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O pipeline deve exibir colunas por status do processo comercial.

- Os status iniciais devem ser Novo, Em contato, Qualificado, Proposta enviada, Negociação, Ganho e Perdido.

- Os leads devem ser exibidos na coluna correspondente ao seu status atual.

- A visualização deve respeitar as permissões do usuário autenticado.

- O pipeline deve permitir identificar rapidamente a etapa de cada oportunidade.

- O pipeline deve exibir apenas leads da organização atual.

### RF027 - Cards de leads no Kanban

O sistema deve exibir os leads no Kanban por meio de cards com informações resumidas.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- Cada lead deve aparecer como um card no Kanban.

- O card deve exibir informações principais do lead.

- O card deve permitir identificar o nome do lead.

- O card deve permitir identificar a empresa, quando informada.

- O card deve permitir identificar a origem ou responsável, quando aplicável.

- O card deve permitir acesso à página de detalhes do lead.

- O card deve representar apenas leads pertencentes à organização atual.

### RF028 - Movimentação de leads entre etapas

O sistema deve permitir mover leads entre as etapas do pipeline Kanban.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O Administrador deve conseguir mover qualquer lead da organização atual no Kanban.

- O Gestor Comercial deve conseguir mover leads da equipe.

- O Vendedor / SDR deve conseguir mover apenas leads atribuídos a ele ou cadastrados por ele.

- O sistema deve impedir movimentações feitas por usuários sem permissão.

- O lead movido deve passar a pertencer à nova etapa selecionada.

- O sistema deve impedir movimentação de leads fora da organização atual.

### RF029 - Atualização automática de status no Kanban

O sistema deve atualizar automaticamente o status do lead quando ele for movido entre colunas do Kanban.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- Ao mover um lead para outra coluna, o status do lead deve ser atualizado.

- A nova coluna deve representar o novo status do lead.

- A atualização deve ser refletida na listagem e nos detalhes do lead.

- A alteração deve respeitar as permissões do usuário autenticado.

- A movimentação deve preservar os dados anteriores do lead.

- A alteração de status deve gerar registro automático no histórico do lead.

### RF030 - Acesso aos detalhes do lead pelo Kanban

O sistema deve permitir acessar a página de detalhes do lead a partir do card exibido no Kanban.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O card do lead deve possuir ação para acessar os detalhes da oportunidade.

- O usuário deve ser direcionado para a página de detalhes do lead.

- O acesso deve respeitar as permissões do usuário.

- Usuários sem permissão não devem acessar detalhes de leads fora do seu escopo.

- Usuários não devem acessar detalhes de leads fora da organização atual.

## 4.4 Página de Detalhes do Lead

### RF031 - Página de detalhes do lead

O sistema deve disponibilizar uma página de detalhes para cada lead.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- Cada lead deve possuir uma página de detalhes.

- A página deve exibir os dados completos do lead.

- A página deve exibir o status atual.

- A página deve exibir a origem do contato.

- A página deve exibir o responsável atual.

- A página deve permitir acesso ao histórico de interações.

- A página deve permitir acesso às tarefas vinculadas ao lead.

- A página deve respeitar o vínculo do lead com a organização atual.

### RF032 - Visualização de dados completos do lead

O sistema deve permitir que usuários autorizados visualizem os dados completos de um lead.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- A página deve exibir nome, e-mail, telefone e empresa.

- A página deve exibir origem do contato.

- A página deve exibir interesse demonstrado.

- A página deve exibir observações gerais.

- A página deve exibir responsável pelo atendimento.

- A página deve exibir status atual.

- A página deve exibir data de cadastro.

- A página deve exibir data da última atualização.

- A visualização deve respeitar as permissões do usuário autenticado.

### RF033 - Edição do lead pela página de detalhes

O sistema deve permitir editar informações do lead a partir da página de detalhes, conforme permissão do usuário.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O usuário autorizado deve conseguir editar dados do lead.

- O sistema deve validar os campos obrigatórios.

- O sistema deve impedir edição por usuários sem permissão.

- O Vendedor / SDR deve editar apenas leads atribuídos a ele ou cadastrados por ele.

- As alterações devem ser refletidas na listagem, no Kanban e nos detalhes do lead.

- A edição deve ocorrer apenas em leads da organização atual.

## 4.5 Histórico de Interações e Eventos

### RF034 - Registro de interações manuais

O sistema deve permitir registrar manualmente interações realizadas com cada lead.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O usuário autorizado deve conseguir registrar uma interação em um lead.

- A interação deve estar vinculada a um lead.

- A interação deve estar vinculada à organização atual.

- A interação deve conter tipo.

- A interação deve conter descrição.

- A interação deve registrar o usuário responsável pelo registro.

- A interação deve registrar data e hora.

- O sistema deve impedir registros em leads fora do escopo de permissão do usuário.

### RF035 - Tipos de interação manual

O sistema deve permitir classificar as interações manuais por tipo.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O sistema deve permitir registrar interação do tipo Ligação.

- O sistema deve permitir registrar interação do tipo WhatsApp.

- O sistema deve permitir registrar interação do tipo E-mail.

- O sistema deve permitir registrar interação do tipo Reunião.

- O sistema deve permitir registrar interação do tipo Observação interna.

- O sistema deve permitir registrar interação do tipo Envio de proposta.

- O sistema deve permitir registrar interação do tipo Outro.

### RF036 - Registro automático de eventos importantes no histórico do lead

O sistema deve registrar automaticamente eventos importantes no histórico do lead, mesmo quando o usuário não registrar uma interação manual.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR, conforme ação realizada.

**Critérios de aceitação:**

- O sistema deve registrar automaticamente mudanças de status do lead.

- O sistema deve registrar automaticamente trocas de responsável pelo lead.

- O sistema deve registrar automaticamente arquivamento ou inativação do lead.

- O sistema pode registrar automaticamente a criação de tarefas relevantes relacionadas ao lead, conforme regra definida posteriormente.

- Cada registro automático deve indicar o tipo de evento ocorrido.

- Cada registro automático deve indicar o usuário responsável pela ação, quando aplicável.

- Cada registro automático deve indicar data e hora do evento.

- O registro automático deve ser exibido no histórico do lead.

- O registro automático deve preservar o contexto da alteração realizada.

- O histórico do lead não deve depender exclusivamente de registros manuais feitos pelos usuários.

### RF037 - Listagem do histórico do lead

O sistema deve permitir listar as interações manuais e eventos automáticos registrados em um lead.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- A página de detalhes do lead deve exibir o histórico do lead.

- O histórico deve incluir interações manuais.

- O histórico deve incluir eventos automáticos importantes.

- Os registros devem ser exibidos em ordem cronológica.

- Cada registro deve exibir tipo, descrição, data e usuário responsável, quando aplicável.

- O histórico deve ser acessível apenas para usuários com permissão sobre o lead.

- O histórico deve preservar os registros realizados anteriormente.

- O histórico deve exibir apenas registros pertencentes à organização atual.

### RF038 - Registro manual do histórico sem integrações externas

O sistema deve manter o histórico de interações de forma manual no MVP, sem integração automática com canais externos.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O usuário deve registrar manualmente contatos realizados fora do sistema.

- O sistema não deve depender de integração automática com WhatsApp, e-mail ou ferramentas externas.

- O histórico deve servir como registro interno do acompanhamento comercial.

- O sistema deve permitir consultar o contexto anterior do atendimento.

- Eventos internos importantes do próprio sistema devem ser registrados automaticamente, conforme requisito específico.

## 4.6 Tarefas e Lembretes

### RF039 - Criação de tarefas

O sistema deve permitir a criação de tarefas relacionadas aos leads.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O usuário autorizado deve conseguir criar uma tarefa para um lead.

- A tarefa deve estar vinculada a um lead.

- A tarefa deve estar vinculada à organização atual.

- A tarefa deve possuir título.

- A tarefa deve permitir descrição.

- A tarefa deve possuir responsável.

- A tarefa deve possuir data de vencimento.

- A tarefa deve possuir status.

- A tarefa deve possuir data de criação.

- O sistema deve respeitar as permissões do usuário autenticado.

- A criação de tarefas relevantes poderá gerar registro automático no histórico do lead, conforme regra definida posteriormente.

### RF040 - Edição de tarefas

O sistema deve permitir editar tarefas relacionadas aos leads.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O usuário autorizado deve conseguir editar uma tarefa.

- O Administrador deve conseguir editar tarefas da organização atual.

- O Gestor Comercial deve conseguir editar tarefas da equipe.

- O Vendedor / SDR deve conseguir editar tarefas relacionadas aos seus próprios leads.

- O sistema deve impedir edição de tarefas por usuários sem permissão.

- O sistema deve validar informações obrigatórias da tarefa.

- O sistema deve impedir edição de tarefas fora da organização atual.

### RF041 - Conclusão de tarefas

O sistema deve permitir marcar tarefas como concluídas.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O usuário autorizado deve conseguir marcar uma tarefa como concluída.

- A tarefa concluída deve deixar de ser considerada pendente.

- A tarefa concluída deve registrar data de conclusão.

- O sistema deve preservar o histórico da tarefa.

- O sistema deve impedir conclusão de tarefas por usuários sem permissão.

### RF042 - Status de tarefas

O sistema deve permitir controlar o status das tarefas.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- A tarefa deve possuir status Pendente.

- A tarefa deve possuir status Concluída.

- Toda nova tarefa deve iniciar com status adequado ao fluxo definido.

- O status da tarefa deve ser atualizado quando ela for concluída.

- O status da tarefa deve ser exibido nas telas relacionadas.

### RF043 - Listagem de tarefas por lead

O sistema deve permitir listar as tarefas vinculadas a um lead.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- A página de detalhes do lead deve exibir as tarefas vinculadas.

- Cada tarefa deve exibir título, responsável, vencimento e status.

- O sistema deve permitir identificar tarefas pendentes.

- O sistema deve permitir identificar tarefas concluídas.

- A visualização deve respeitar as permissões do usuário autenticado.

- A visualização deve considerar apenas tarefas da organização atual.

### RF044 - Visualização de tarefas pendentes

O sistema deve permitir visualizar tarefas pendentes.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O Administrador deve conseguir visualizar tarefas pendentes da organização atual.

- O Gestor Comercial deve conseguir visualizar tarefas pendentes da equipe.

- O Vendedor / SDR deve conseguir visualizar tarefas pendentes relacionadas aos seus próprios leads.

- O sistema deve diferenciar tarefas pendentes de tarefas concluídas.

- A visualização deve respeitar as permissões do usuário autenticado.

### RF045 - Identificação de tarefas atrasadas

O sistema deve identificar tarefas atrasadas com base na data de vencimento.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- Uma tarefa pendente deve ser considerada atrasada quando a data de vencimento tiver passado.

- Tarefas concluídas não devem ser consideradas atrasadas.

- O sistema deve exibir indicação visual de atraso.

- O Administrador deve conseguir visualizar tarefas atrasadas da organização atual.

- O Gestor Comercial deve conseguir visualizar tarefas atrasadas da equipe.

- O Vendedor / SDR deve conseguir visualizar tarefas atrasadas relacionadas aos seus próprios leads.

### RF046 - Lembrete simples por data de vencimento

O sistema deve tratar lembretes de forma simples no MVP, utilizando a data de vencimento da tarefa e indicação de atraso.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- A tarefa deve possuir data de vencimento.

- O sistema deve indicar quando uma tarefa estiver atrasada.

- O MVP não deve exigir notificações automáticas.

- O MVP não deve exigir alertas por e-mail, push ou integrações externas.

- O lembrete deve ser representado pelo controle visual da tarefa e seu vencimento.

### RF047 - Criação de tarefas para vendedores

O sistema deve permitir que usuários com permissão criem tarefas para vendedores.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

**Critérios de aceitação:**

- O Administrador deve conseguir criar tarefas para vendedores.

- O Gestor Comercial deve conseguir criar tarefas para vendedores da equipe.

- A tarefa deve possuir responsável.

- O vendedor responsável deve conseguir visualizar a tarefa conforme seu escopo.

- O Vendedor / SDR não deve criar tarefas para outros usuários.

- O responsável pela tarefa deve possuir vínculo ativo com a organização atual.

## 4.7 Dashboard

### RF048 - Dashboard geral

O sistema deve disponibilizar um dashboard geral com indicadores básicos da operação comercial.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

**Critérios de aceitação:**

- O Administrador deve conseguir visualizar o dashboard geral da organização atual.

- O Gestor Comercial deve conseguir visualizar o dashboard geral da equipe.

- O dashboard deve exibir indicadores básicos da operação.

- O dashboard deve ser simples e objetivo.

- O dashboard deve apoiar a tomada rápida de decisão.

- O dashboard deve considerar apenas dados da organização atual.

### RF049 - Dashboard individual

O sistema deve disponibilizar um dashboard individual para acompanhamento das oportunidades do próprio usuário.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O Vendedor / SDR deve conseguir visualizar indicadores relacionados aos seus próprios leads.

- O Gestor Comercial deve conseguir visualizar seu dashboard individual, quando aplicável.

- O Administrador deve conseguir visualizar seu dashboard individual, quando aplicável.

- O dashboard individual deve respeitar o escopo de acesso do usuário.

- O dashboard individual não deve exibir dados de leads sem permissão.

- O dashboard individual deve considerar apenas dados da organização atual.

### RF050 - Indicadores do dashboard

O sistema deve exibir indicadores básicos relacionados aos leads, tarefas e oportunidades.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR, conforme escopo individual.

**Critérios de aceitação:**

- O dashboard deve exibir total de leads cadastrados.

- O dashboard deve exibir leads novos no mês.

- O dashboard deve exibir leads ganhos.

- O dashboard deve exibir leads perdidos.

- O dashboard deve exibir taxa de conversão.

- O dashboard deve exibir tarefas atrasadas.

- O dashboard deve exibir leads por status.

- O dashboard deve exibir leads por origem.

- O dashboard deve exibir evolução de oportunidades ao longo do tempo.

- Os indicadores devem respeitar o perfil do usuário autenticado.

### RF051 - Cards e gráficos básicos

O sistema deve apresentar os dados do dashboard por meio de cards, contadores e gráficos simples.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR, conforme escopo individual.

**Critérios de aceitação:**

- O dashboard deve apresentar cards com números principais.

- O dashboard pode apresentar gráficos básicos para distribuição de leads.

- O dashboard deve evitar relatórios analíticos avançados no MVP.

- O dashboard deve priorizar clareza e leitura rápida.

- Os dados exibidos devem respeitar as permissões do usuário autenticado.

## 4.8 Formulário Público de Captura

### RF052 - Exibição do formulário público

O sistema deve disponibilizar um formulário público para captura de leads.

**Perfis envolvidos:**

- Visitante público.

**Critérios de aceitação:**

- O formulário deve ser acessível sem login.

- O formulário deve permitir que um possível cliente envie seus dados.

- O formulário deve funcionar como página de contato ou solicitação de orçamento.

- O formulário deve ser separado da área interna do CRM.

- O formulário deve exibir confirmação visual após envio bem-sucedido.

### RF053 - Campos do formulário público

O formulário público deve conter os campos necessários para cadastrar um lead inicial no CRM.

**Perfis envolvidos:**

- Visitante público.

**Critérios de aceitação:**

- O formulário deve solicitar nome.

- O formulário deve solicitar e-mail.

- O formulário deve solicitar telefone.

- O formulário deve permitir informar empresa.

- O formulário deve permitir informar interesse demonstrado.

- O formulário deve permitir informar mensagem ou observação.

- O sistema deve validar os campos obrigatórios antes do envio.

### RF054 - Cadastro automático de lead pelo formulário público

O sistema deve criar automaticamente um lead no CRM quando o formulário público for enviado com sucesso.

**Perfis envolvidos:**

- Visitante público.

- Administrador.

- Gestor Comercial.

- Vendedor / SDR, conforme atribuição futura.

**Critérios de aceitação:**

- O visitante deve conseguir enviar o formulário público.

- Após o envio, o sistema deve criar um novo lead.

- O lead criado deve ficar disponível na área interna do CRM.

- O sistema deve impedir cadastro quando campos obrigatórios estiverem inválidos.

- O sistema deve exibir mensagem de confirmação após o envio.

- O lead criado deve estar vinculado à organização principal do MVP.

### RF055 - Origem automática do lead público

O sistema deve definir automaticamente a origem como Site para leads cadastrados pelo formulário público.

**Perfis envolvidos:**

- Visitante público.

- Administrador.

- Gestor Comercial.

**Critérios de aceitação:**

- Todo lead criado pelo formulário público deve entrar com origem Site.

- O visitante não deve precisar selecionar a origem.

- A origem Site deve aparecer nos detalhes do lead.

- A origem Site deve permitir uso em filtros e indicadores do dashboard.

### RF056 - Status inicial do lead público

O sistema deve definir automaticamente o status Novo para leads cadastrados pelo formulário público.

**Perfis envolvidos:**

- Visitante público.

- Administrador.

- Gestor Comercial.

**Critérios de aceitação:**

- Todo lead criado pelo formulário público deve entrar com status Novo.

- O lead deve aparecer na coluna Novo do Kanban.

- O lead deve aparecer nas listagens conforme permissões dos usuários.

- O status inicial deve poder ser alterado posteriormente por usuário autorizado.

### RF057 - Responsável inicial do lead público

O sistema deve permitir que leads vindos do formulário público sejam criados sem responsável definido ou atribuídos conforme regra inicial do sistema.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

**Critérios de aceitação:**

- O lead criado pelo formulário público pode iniciar sem responsável.

- O sistema pode atribuir um responsável conforme regra inicial definida posteriormente.

- O Administrador deve conseguir atribuir responsável ao lead.

- O Gestor Comercial deve conseguir atribuir responsável ao lead conforme permissões.

- O lead deve permanecer disponível para acompanhamento mesmo sem responsável definido.

- Leads públicos sem responsável devem ficar visíveis para Administrador e Gestor Comercial em listagem ou filtro específico de leads sem responsável.

## 4.9 Permissões e Controle de Acesso

### RF058 - Controle de acesso por perfil na organização

O sistema deve controlar o acesso às funcionalidades conforme o perfil do usuário autenticado na organização atual.

**Perfis envolvidos:**

- Administrador.

- Gestor Comercial.

- Vendedor / SDR.

**Critérios de aceitação:**

- O sistema deve diferenciar permissões entre Administrador, Gestor Comercial e Vendedor / SDR.

- Cada perfil deve acessar apenas as funcionalidades permitidas dentro da organização atual.

- O sistema deve impedir ações não autorizadas.

- O sistema deve restringir dados conforme o perfil.

- A autorização deve ser aplicada nas telas e nas ações internas do sistema.

- As permissões devem ser baseadas no vínculo do usuário com a organização.

### RF059 - Permissões do Administrador

O sistema deve permitir que o Administrador tenha acesso amplo às funcionalidades administrativas e operacionais da organização atual.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- O Administrador deve conseguir criar ou vincular usuários à organização atual.

- O Administrador deve conseguir gerenciar vínculos de usuários com a organização atual.

- O Administrador deve conseguir definir perfis de acesso na organização atual.

- O Administrador deve conseguir visualizar todos os leads da organização atual.

- O Administrador deve conseguir visualizar leads sem responsável.

- O Administrador deve conseguir criar e editar leads.

- O Administrador deve conseguir atribuir e trocar responsáveis.

- O Administrador deve conseguir acessar o pipeline completo.

- O Administrador deve conseguir mover qualquer lead no Kanban.

- O Administrador deve conseguir registrar interações manuais.

- O Administrador deve conseguir visualizar eventos automáticos no histórico do lead.

- O Administrador deve conseguir criar tarefas.

- O Administrador deve conseguir criar tarefas para vendedores.

- O Administrador deve conseguir visualizar dashboard geral.

- O Administrador deve conseguir gerenciar configurações básicas.

- O Administrador deve conseguir arquivar ou inativar leads.

### RF060 - Permissões do Gestor Comercial

O sistema deve permitir que o Gestor Comercial acompanhe a operação comercial e gerencie leads da equipe na organização atual.

**Perfis envolvidos:**

- Gestor Comercial.

**Critérios de aceitação:**

- O Gestor Comercial deve conseguir visualizar leads da equipe.

- O Gestor Comercial deve conseguir visualizar leads sem responsável.

- O Gestor Comercial deve conseguir criar leads.

- O Gestor Comercial deve conseguir editar leads da equipe.

- O Gestor Comercial deve conseguir atribuir leads a vendedores.

- O Gestor Comercial deve conseguir trocar responsáveis por leads.

- O Gestor Comercial deve conseguir acompanhar o pipeline completo da equipe.

- O Gestor Comercial deve conseguir mover leads da equipe no Kanban.

- O Gestor Comercial deve conseguir filtrar leads por responsável, origem e status.

- O Gestor Comercial deve conseguir registrar interações manuais.

- O Gestor Comercial deve conseguir visualizar eventos automáticos no histórico do lead.

- O Gestor Comercial deve conseguir criar tarefas.

- O Gestor Comercial deve conseguir criar tarefas para vendedores.

- O Gestor Comercial deve conseguir visualizar tarefas pendentes e atrasadas da equipe.

- O Gestor Comercial deve conseguir visualizar dashboard geral e individual.

- O Gestor Comercial não deve gerenciar usuários ou perfis de acesso.

### RF061 - Permissões do Vendedor / SDR

O sistema deve permitir que o Vendedor / SDR acompanhe seus próprios leads e oportunidades dentro da organização atual.

**Perfis envolvidos:**

- Vendedor / SDR.

**Critérios de aceitação:**

- O Vendedor / SDR deve conseguir cadastrar novos leads.

- Leads cadastrados pelo Vendedor / SDR devem ser atribuídos automaticamente a ele, salvo regra diferente definida posteriormente.

- O Vendedor / SDR deve conseguir visualizar leads atribuídos a ele.

- O Vendedor / SDR deve conseguir visualizar leads cadastrados por ele próprio.

- O Vendedor / SDR deve conseguir editar informações dos seus próprios leads.

- O Vendedor / SDR deve conseguir registrar interações manuais nos próprios leads.

- O Vendedor / SDR deve conseguir visualizar eventos automáticos no histórico dos próprios leads.

- O Vendedor / SDR deve conseguir criar tarefas nos próprios leads.

- O Vendedor / SDR deve conseguir alterar o status das suas próprias oportunidades.

- O Vendedor / SDR deve conseguir mover seus próprios leads no Kanban.

- O Vendedor / SDR deve conseguir utilizar filtros e busca dentro da sua carteira.

- O Vendedor / SDR deve conseguir visualizar dashboard individual.

- O Vendedor / SDR não deve visualizar leads de outros usuários sem permissão.

- O Vendedor / SDR não deve visualizar leads sem responsável, salvo regra específica definida posteriormente.

### RF062 - Restrição de acesso aos leads do vendedor

O sistema deve restringir o acesso do Vendedor / SDR aos leads atribuídos a ele ou cadastrados por ele próprio.

**Perfis envolvidos:**

- Vendedor / SDR.

**Critérios de aceitação:**

- O Vendedor / SDR deve visualizar apenas leads atribuídos a ele.

- O Vendedor / SDR deve visualizar leads que ele próprio cadastrou.

- O Vendedor / SDR não deve visualizar leads atribuídos a outros vendedores.

- O Vendedor / SDR não deve editar leads fora do seu escopo.

- O Vendedor / SDR não deve mover no Kanban leads fora do seu escopo.

- O sistema deve aplicar essa restrição na listagem, no Kanban, nos detalhes, nas tarefas e nas interações.

- A restrição deve ser aplicada dentro da organização atual.

### RF063 - Acesso do Gestor Comercial às tarefas da equipe

O sistema deve permitir que o Gestor Comercial visualize tarefas pendentes e atrasadas da equipe.

**Perfis envolvidos:**

- Gestor Comercial.

**Critérios de aceitação:**

- O Gestor Comercial deve conseguir visualizar tarefas pendentes da equipe.

- O Gestor Comercial deve conseguir visualizar tarefas atrasadas da equipe.

- O Gestor Comercial deve conseguir identificar o responsável por cada tarefa.

- O Gestor Comercial deve conseguir acessar o lead relacionado à tarefa conforme permissão.

- O sistema deve permitir que o Gestor Comercial acompanhe follow-ups da equipe.

- O sistema deve considerar apenas tarefas da organização atual.

## 4.10 Configurações Básicas

### RF064 - Gerenciamento de configurações básicas da organização

O sistema deve permitir que o Administrador gerencie configurações básicas da organização atual.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- O Administrador deve conseguir acessar uma área de configurações básicas.

- As configurações devem apoiar a organização inicial do sistema.

- O acesso às configurações deve ser restrito ao Administrador.

- Configurações avançadas não serão priorizadas no MVP.

- O sistema deve manter simplicidade na administração inicial.

- As configurações devem estar vinculadas à organização atual.

### RF065 - Dados básicos da organização

O sistema deve permitir que o Administrador visualize e edite dados básicos da organização atual.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- O Administrador deve conseguir visualizar o nome da organização.

- O Administrador deve conseguir editar dados básicos da organização, conforme campos definidos para o MVP.

- O sistema deve manter esses dados vinculados à organização atual.

- O sistema não deve exigir configurações complexas de empresa no MVP.

- A edição de dados básicos não deve afetar dados de usuários, leads, tarefas ou interações de forma indevida.

### RF066 - Visualização de origens padrão

O sistema deve permitir que o Administrador visualize as origens padrão de leads disponíveis no MVP.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- O Administrador deve conseguir visualizar as origens padrão utilizadas no cadastro de leads.

- As origens iniciais devem incluir Site, Instagram, LinkedIn, Indicação, Google Ads, Eventos, WhatsApp e Outro.

- A visualização das origens deve apoiar a organização operacional do CRM.

- O MVP pode permitir controle simples dessas origens, desde que não gere complexidade administrativa excessiva.

- O sistema não deve incluir personalização avançada de origens no MVP, salvo decisão posterior.

### RF067 - Limites das configurações básicas

O sistema deve manter as configurações básicas do MVP limitadas a necessidades operacionais simples.

**Perfis envolvidos:**

- Administrador.

**Critérios de aceitação:**

- As configurações básicas não devem incluir personalização avançada de pipeline.

- As configurações básicas não devem incluir permissões complexas.

- As configurações básicas não devem incluir múltiplas organizações pela interface.

- As configurações básicas não devem incluir cobrança, planos ou assinatura.

- As configurações básicas não devem incluir módulos administrativos extensos.

- Qualquer configuração avançada deverá ser avaliada para versões futuras.

## 5. Requisitos Fora do Escopo Funcional do MVP

As funcionalidades abaixo não fazem parte dos requisitos funcionais da primeira versão do LeadFlow CRM.

Elas poderão ser avaliadas em versões futuras, conforme evolução do produto e novas necessidades do negócio.

Funcionalidades fora do MVP:

- Integração real com WhatsApp.

- Envio automático de e-mails.

- Integração com ferramentas externas de e-mail marketing.

- Integração com redes sociais.

- Integração com LinkedIn, Instagram ou Google Ads.

- Integração com gateways de pagamento.

- Automações avançadas de funil.

- Recursos de inteligência artificial.

- Chat interno.

- Discador telefônico.

- Relatórios comerciais complexos.

- Previsão avançada de vendas.

- Gestão financeira.

- Gestão de contratos.

- Gestão de propostas com assinatura eletrônica.

- Aplicativo mobile.

- Notificações push.

- API pública para terceiros.

- Importação em massa por planilha.

- Exportação avançada de dados.

- Múltiplas empresas ou multi-tenant completo.

- Personalização avançada de pipeline.

- Permissões avançadas e altamente customizáveis.

- Módulos administrativos complexos.

- Exclusão definitiva de leads como fluxo comum.

## 6. Observações sobre Preparação para Multi-tenant

O MVP do LeadFlow CRM não contemplará multi-tenant completo nesta primeira versão.

Isso significa que o sistema não deverá incluir, neste momento, recursos como múltiplas empresas utilizando a plataforma em modelo SaaS, subdomínios por empresa, planos de assinatura, cobrança recorrente, painel de tenants, provisionamento automático de organizações ou isolamento avançado entre bases de clientes.

Apesar disso, os requisitos funcionais foram descritos considerando o conceito de organização atual, para facilitar uma evolução futura do sistema.

No contexto de usuários, o sistema deve considerar conceitualmente duas camadas:

- Conta de usuário.

- Vínculo do usuário com a organização.

A conta de usuário representa a identidade de login da pessoa, contendo dados como nome, e-mail e credenciais de acesso.

O vínculo do usuário com a organização representa sua participação em uma empresa específica, contendo perfil, permissões e status dentro daquela organização.

No MVP, o Administrador poderá criar usuários para a organização principal. Porém, essa operação deverá ser compreendida como criação de uma conta e vínculo dessa conta à organização atual.

Em uma evolução futura para multi-tenant, essa mesma estrutura poderá permitir que um usuário já existente seja vinculado a outra organização, com outro perfil de acesso, sem duplicação da identidade global do usuário.

Dessa forma, um mesmo usuário poderá futuramente atuar como Vendedor / SDR em uma empresa e Administrador em outra, utilizando o mesmo e-mail de login, desde que possua vínculos diferentes em cada organização.

No MVP, essa complexidade deve permanecer invisível para o usuário final. A interface do Administrador deve continuar simples e objetiva, apresentando ações como adicionar usuário, definir perfil e definir status, enquanto o sistema trata internamente a criação ou vinculação da conta à organização atual.

## 7. Observações Finais

Este documento descreve os requisitos funcionais do MVP do LeadFlow CRM.

Os requisitos aqui definidos devem ser utilizados como base para os próximos documentos de planejamento, especialmente:

- Requisitos não funcionais.

- Regras de negócio.

- Modelagem de banco de dados.

- Arquitetura.

- API endpoints.

- Telas e fluxos.

- Backlog.

- Plano de desenvolvimento.

- Plano de testes.

As regras específicas de funcionamento, como condições para arquivamento ou inativação de leads, restrições detalhadas de mudança de status, regras de responsabilidade, regras de vínculo de usuários, regras para eventos automáticos no histórico e critérios operacionais mais específicos, deverão ser detalhadas posteriormente no documento de regras de negócio.

O MVP deve priorizar simplicidade, clareza visual e funcionamento completo do fluxo principal de gestão de leads, mantendo o foco em entregar uma primeira versão funcional, organizada e coerente com a proposta do produto.

A preparação para multi-tenant não deve aumentar a complexidade de uso do MVP, mas deve orientar a modelagem funcional para evitar decisões que dificultem a evolução futura do LeadFlow CRM.

O histórico do lead deve combinar registros manuais feitos pelos usuários com registros automáticos de eventos importantes do próprio sistema, garantindo maior rastreabilidade do acompanhamento comercial sem depender exclusivamente da disciplina operacional da equipe.

Leads sem responsável devem ser visíveis para Administrador e Gestor Comercial, para evitar que oportunidades vindas do formulário público ou de outros fluxos fiquem sem acompanhamento.
