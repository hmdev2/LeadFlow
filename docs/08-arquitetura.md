# Arquitetura do Sistema

## 1. Objetivo do Documento

Este documento tem como objetivo definir a arquitetura técnica do **LeadFlow CRM**, descrevendo como o sistema deverá ser organizado para atender ao MVP de forma simples, segura, manutenível e preparada para evolução futura.

A arquitetura definida neste documento deverá orientar as decisões de desenvolvimento, organização do código, comunicação entre camadas, aplicação de permissões, acesso aos dados, proteção das informações, tratamento dos principais fluxos do sistema e preparação para futuras versões.

Este documento não tem como objetivo detalhar todos os endpoints, telas, componentes visuais ou tarefas de desenvolvimento. Esses pontos deverão ser descritos nos documentos específicos de API, telas e fluxos, backlog, plano de desenvolvimento e plano de testes.

## 2. Contexto

O LeadFlow CRM será um sistema web voltado para pequenas equipes comerciais que precisam centralizar, organizar e acompanhar leads recebidos por diferentes canais.

O MVP deverá permitir autenticação de usuários, cadastro e gerenciamento de leads, listagem com filtros, pipeline Kanban, página de detalhes do lead, histórico de interações, tarefas de acompanhamento, dashboard básico, formulário público de captura e controle simples de permissões.

O sistema será utilizado inicialmente por uma única organização principal. Apesar disso, a arquitetura deverá considerar desde o início o conceito de organização atual, garantindo que usuários, leads, tarefas, interações, status, origens e configurações estejam vinculados à organização correta.

Essa decisão prepara o sistema para uma possível evolução futura para multi-tenant, sem expor essa complexidade ao usuário final no MVP.

## 3. Objetivos da Arquitetura

A arquitetura do LeadFlow CRM deverá atender aos seguintes objetivos:

- Manter o MVP simples e viável de desenvolver.
- Organizar o código por responsabilidades claras.
- Garantir autenticação e controle de permissões.
- Aplicar o escopo da organização atual nas consultas e ações internas.
- Proteger dados comerciais e dados pessoais básicos dos leads.
- Preservar histórico, tarefas e informações comerciais importantes.
- Favorecer manutenção e evolução após o MVP.
- Evitar decisões que dificultem uma futura evolução para multi-tenant.
- Evitar complexidade desnecessária, como microsserviços, filas obrigatórias, infraestrutura distribuída ou automações avançadas no MVP.

## 4. Tipo de Arquitetura Adotada

Para o MVP, o LeadFlow CRM deverá adotar uma **arquitetura monolítica modular**.

Nessa abordagem, o sistema será desenvolvido como uma única aplicação web, mas seu código deverá ser organizado em módulos ou domínios funcionais bem separados.

Essa decisão é adequada para o MVP porque reduz a complexidade inicial, facilita o desenvolvimento, simplifica testes e implantação, e ainda permite boa organização interna do sistema.

Não deverão ser adotados microsserviços no MVP. A divisão em múltiplos serviços, aplicações independentes ou infraestrutura distribuída aumentaria a complexidade sem necessidade para a primeira versão do produto.

## 5. Visão Geral da Arquitetura

A arquitetura geral do sistema poderá ser representada da seguinte forma:

```text
Usuário / Visitante
        |
        v
Navegador Web
        |
        v
Aplicação Web LeadFlow CRM
        |
        |-- Camada de Interface
        |-- Camada de Rotas e Controllers
        |-- Camada de Validação
        |-- Camada de Serviços de Aplicação
        |-- Camada de Regras de Domínio
        |-- Camada de Autorização e Permissões
        |-- Camada de Persistência
        |
        v
Banco de Dados Relacional
```

A área interna do CRM deverá ser protegida por autenticação. O formulário público de captura deverá ser acessível sem login, mas separado das rotas internas e com proteção básica contra abuso.

## 6. Premissas Técnicas

A arquitetura do MVP deverá seguir as premissas abaixo:

- O sistema será uma aplicação web acessível por navegador.
- A área interna será protegida por login e sessão autenticada.
- O formulário público será acessível sem autenticação.
- O backend deverá validar permissões em todas as ações sensíveis.
- A interface poderá ocultar ações não permitidas, mas não deverá ser a única camada de segurança.
- As principais entidades deverão estar vinculadas à organização atual.
- O MVP utilizará uma organização principal, sem tela de seleção ou troca de organização.
- O banco de dados deverá ser relacional.
- O código deverá ser organizado por módulos ou domínios funcionais.
- As regras de negócio não deverão ficar concentradas apenas em controllers ou telas.
- Operações que alteram dados importantes deverão preservar rastreabilidade.
- Exclusão definitiva de leads não deverá ser tratada como fluxo comum.
- Integrações externas reais não fazem parte do MVP.

## 7. Camadas da Aplicação

## 7.1 Camada de Interface

A camada de interface será responsável por apresentar as telas, formulários, listas, cards, dashboard e pipeline Kanban para os usuários.

Responsabilidades:

- Exibir informações conforme o perfil do usuário.
- Apresentar formulários de cadastro e edição.
- Exibir mensagens de sucesso e erro.
- Ocultar ou desabilitar ações que o usuário não pode executar.
- Indicar visualmente tarefas atrasadas.
- Indicar visualmente leads arquivados quando aplicável.
- Manter consistência visual entre listagem, Kanban, detalhes, tarefas e dashboard.

A interface não deverá conter sozinha as regras de permissão. Toda ação sensível deverá ser validada também no backend.

## 7.2 Camada de Rotas e Controllers

A camada de rotas e controllers será responsável por receber requisições, direcionar ações e retornar respostas adequadas para a interface.

Responsabilidades:

- Receber dados enviados por formulários ou ações da interface.
- Acionar validações.
- Chamar serviços de aplicação.
- Redirecionar o usuário após ações concluídas.
- Retornar mensagens de erro ou sucesso.
- Separar rotas públicas de rotas internas autenticadas.

Controllers não deverão concentrar regras complexas de negócio. Sempre que uma ação envolver validação de permissão, alteração de status, troca de responsável, arquivamento, criação de histórico ou regras de escopo, essa lógica deverá ser delegada para serviços, policies, middlewares ou componentes equivalentes.

## 7.3 Camada de Validação

A camada de validação será responsável por garantir que os dados recebidos estejam corretos antes da execução das regras do sistema.

Responsabilidades:

- Validar campos obrigatórios.
- Validar formato de e-mail.
- Validar datas de vencimento de tarefas.
- Validar presença de pelo menos um dado de contato do lead, quando aplicável.
- Validar status, origem e responsável informados.
- Validar dados enviados pelo formulário público.
- Retornar mensagens compreensíveis para o usuário.

As validações devem ser aplicadas tanto na área interna quanto no formulário público.

## 7.4 Camada de Serviços de Aplicação

A camada de serviços de aplicação será responsável por orquestrar os principais fluxos do sistema.

Exemplos de serviços esperados:

| Serviço                      | Responsabilidade                                                 |
| ---------------------------- | ---------------------------------------------------------------- |
| `LeadService`                | Cadastro, edição, arquivamento, reativação e atribuição de leads |
| `PipelineService`            | Movimentação de leads no Kanban e atualização de status          |
| `LeadInteractionService`     | Registro de interações manuais e eventos automáticos             |
| `TaskService`                | Criação, edição, conclusão e consulta de tarefas                 |
| `DashboardService`           | Cálculo dos indicadores básicos                                  |
| `OrganizationUserService`    | Gestão de usuários vinculados à organização                      |
| `PublicLeadCaptureService`   | Tratamento do formulário público de captura                      |
| `OrganizationContextService` | Resolução da organização atual no MVP e em evolução futura       |

A camada de serviços deverá reduzir duplicação de lógica e manter os controllers mais simples.

## 7.5 Camada de Regras de Domínio

A camada de regras de domínio representa os comportamentos essenciais do negócio.

Responsabilidades:

- Garantir que todo lead pertença a uma organização.
- Garantir que todo lead possua status e origem.
- Garantir que tarefas estejam vinculadas a leads.
- Garantir que responsáveis sejam usuários ativos da organização.
- Garantir que vendedores acessem apenas seus próprios leads.
- Garantir que movimentações no Kanban atualizem o status do lead.
- Garantir que mudanças importantes gerem histórico automático.
- Garantir que arquivamento preserve dados, tarefas e histórico.
- Garantir que tarefas pendentes não sejam apagadas automaticamente ao ganhar, perder ou arquivar um lead.

Essas regras deverão ser implementadas de forma centralizada, evitando comportamentos divergentes entre telas diferentes.

## 7.6 Camada de Autorização e Permissões

A camada de autorização será responsável por verificar se o usuário autenticado pode executar determinada ação ou acessar determinado dado.

Responsabilidades:

- Validar se o usuário está autenticado.
- Validar se o usuário possui vínculo ativo com a organização atual.
- Validar o perfil do usuário na organização.
- Restringir acesso conforme o escopo do dado.
- Impedir ações não autorizadas mesmo quando chamadas diretamente.
- Aplicar regras de acesso em leads, tarefas, interações, dashboard e configurações.

As permissões deverão considerar três elementos principais:

```text
Usuário autenticado
        +
Vínculo ativo com a organização
        +
Perfil dentro da organização
        =
Permissões disponíveis
```

## 7.7 Camada de Persistência

A camada de persistência será responsável por acessar e manipular os dados no banco.

Responsabilidades:

- Representar entidades como organizações, usuários, vínculos, leads, status, origens, interações, tarefas e configurações.
- Aplicar relacionamentos entre entidades.
- Apoiar consultas filtradas por organização.
- Apoiar listagens, buscas, filtros, Kanban e dashboard.
- Preservar dados importantes.
- Evitar inconsistências entre organização, lead, responsável, tarefa e histórico.

Sempre que a tecnologia utilizada possuir ORM ou models, essa camada deverá representar os relacionamentos definidos na modelagem de banco de dados.

## 8. Módulos Principais do Sistema

A aplicação deverá ser organizada em módulos funcionais. Essa divisão não significa aplicações separadas, mas sim separação lógica dentro do monólito modular.

| Módulo                | Responsabilidade principal                                             |
| --------------------- | ---------------------------------------------------------------------- |
| Autenticação          | Login, logout, sessão e proteção de rotas internas                     |
| Organizações          | Organização principal, contexto atual e configurações básicas          |
| Usuários e Permissões | Usuários, vínculos, perfis e status dentro da organização              |
| Leads                 | Cadastro, edição, listagem, filtros, busca, responsável e arquivamento |
| Pipeline Kanban       | Visualização por status e movimentação dos leads entre etapas          |
| Histórico             | Interações manuais e eventos automáticos do lead                       |
| Tarefas               | Criação, edição, conclusão, pendências e atrasos                       |
| Dashboard             | Indicadores gerais e individuais do MVP                                |
| Formulário Público    | Captura pública de leads com origem Site e status Novo                 |
| Configurações         | Dados básicos e configurações simples da organização                   |
| Logs e Diagnóstico    | Registro de erros técnicos e apoio à manutenção                        |
| Backup e Preservação  | Rotina ou previsão básica de backup dos dados principais               |

## 9. Arquitetura de Autenticação

A autenticação deverá proteger a área interna do CRM.

O usuário deverá acessar o sistema utilizando e-mail e senha. Após autenticação válida, o sistema deverá identificar o vínculo ativo do usuário com a organização atual.

Fluxo esperado:

![Diagrama BPMN do processo de login e acesso à área interna do LeadFlow. O usuário interno acessa a tela de login e informa e-mail e senha. O sistema valida as credenciais; se forem inválidas, o usuário retorna ao preenchimento dos dados. Se forem válidas, o sistema verifica o vínculo ativo com a organização. Caso não exista vínculo ativo, o acesso é bloqueado. Caso exista, o sistema identifica o perfil do usuário — Administrador, Gestor Comercial ou Vendedor/SDR — e libera o acesso à área interna conforme suas permissões.](./modelagem_processos/login.png)

Senhas deverão ser armazenadas de forma segura, utilizando práticas adequadas de proteção, e nunca deverão ser armazenadas ou exibidas em texto puro.

Usuários sem vínculo ativo com a organização atual não deverão acessar a área interna, mesmo que suas credenciais globais sejam válidas.

## 10. Arquitetura de Permissões

O controle de permissões deverá ser aplicado em duas camadas:

1. **Interface**, ocultando ou desabilitando ações não permitidas.
2. **Backend**, validando cada ação antes de executá-la.

A validação no backend é obrigatória, pois a interface não deve ser considerada uma barreira de segurança suficiente.

## 10.1 Perfis do MVP

| Perfil           | Acesso arquitetural esperado                                                                                  |
| ---------------- | ------------------------------------------------------------------------------------------------------------- |
| Administrador    | Acesso amplo à organização, usuários, permissões, leads, tarefas, dashboard e configurações                   |
| Gestor Comercial | Acesso à operação comercial, leads da equipe, tarefas da equipe, dashboard geral e atribuição de responsáveis |
| Vendedor / SDR   | Acesso restrito aos leads atribuídos a ele ou cadastrados por ele próprio                                     |

## 10.2 Escopo de Acesso por Dado

A arquitetura deverá aplicar escopo de acesso nos principais dados operacionais.

| Dado          | Regra arquitetural                                                      |
| ------------- | ----------------------------------------------------------------------- |
| Leads         | Sempre filtrados por organização e perfil do usuário                    |
| Tarefas       | Sempre filtradas por organização, lead e responsável conforme permissão |
| Interações    | Acessíveis apenas quando o usuário puder acessar o lead relacionado     |
| Dashboard     | Calculado conforme organização, perfil e escopo do usuário              |
| Configurações | Acessíveis apenas pelo Administrador                                    |
| Usuários      | Gerenciados apenas pelo Administrador                                   |

## 11. Organização Atual e Preparação para Multi-tenant

O MVP deverá operar com uma organização principal, sem expor ao usuário final telas de múltiplas empresas, troca de organização, painel de tenants, subdomínios, cobrança por organização ou planos de assinatura.

Apesar disso, a arquitetura deverá manter o conceito de organização atual como parte central da aplicação.

Todas as consultas internas deverão considerar a organização atual. Isso inclui:

- Leads.
- Tarefas.
- Interações.
- Status de leads.
- Origens de leads.
- Configurações.
- Usuários vinculados à organização.
- Indicadores do dashboard.

O sistema deverá possuir um mecanismo central para resolver a organização atual. No MVP, esse mecanismo poderá sempre retornar a organização principal. Em uma versão futura, esse mesmo ponto poderá evoluir para resolver a organização por subdomínio, rota, sessão, convite, seleção de empresa ou outro critério.

Essa decisão evita espalhar regras fixas de organização única por todo o sistema.

## 12. Arquitetura dos Principais Fluxos

## 12.1 Fluxo de Cadastro Interno de Lead

![Diagrama BPMN do processo de cadastro interno de lead no LeadFlow. O Administrador, Gestor ou Vendedor acessa a criação de lead; o sistema verifica vínculo ativo com a organização atual, ajusta o formulário conforme o perfil do usuário e valida os dados obrigatórios. Em seguida, define a organização atual, verifica o perfil do cadastrante, atribui automaticamente o lead ao próprio vendedor/SDR quando aplicável ou valida o responsável informado. O sistema também verifica possível duplicidade por e-mail ou telefone, valida a origem informada e, se tudo estiver correto, salva o lead e o disponibiliza na listagem, Kanban e dashboard conforme as permissões. Em caso de vínculo inválido, dados inválidos, responsável inválido, duplicidade ou origem inválida, o sistema exibe erro ou alerta operacional.](./modelagem_processos/cadastro_interno_de_lead.png)

Quando o lead for criado por Vendedor / SDR, ele deverá ser atribuído automaticamente ao próprio vendedor, salvo regra futura diferente.

## 12.2 Fluxo de Cadastro pelo Formulário Público

![Fluxo de captura de lead pelo formulário público no LeadFlow. O visitante acessa o formulário, visualiza o aviso de uso dos dados, preenche nome, contato, empresa, interesse e mensagem, e envia as informações. O sistema aplica proteção contra abuso ou spam. Se houver abuso, bloqueia temporariamente o envio, exibe uma mensagem ao visitante e encerra o processo. Se não houver abuso, valida os campos obrigatórios. Caso existam erros, exibe a mensagem no formulário e permite correção. Caso os campos sejam válidos, cria o lead na organização principal, define origem como Site, status como Novo, mantém responsável vazio quando não houver regra automática, exibe confirmação ao visitante e disponibiliza o lead para Administrador e Gestor Comercial na área interna.](./modelagem_processos/captura_lead_form_publico.png)

O formulário público não deverá permitir acesso a dados internos do CRM. Ele também não deverá disparar integrações externas no MVP.

## 12.3 Fluxo de Movimentação no Kanban

![Fluxo de movimentação de lead no Kanban do LeadFlow. O usuário interno acessa o Kanban e o sistema valida autenticação, vínculo ativo com a organização atual e perfil do usuário. Caso o usuário não esteja autenticado ou não possua vínculo ativo, ele é redirecionado para o login e o processo é encerrado. Com acesso válido, o sistema lista os leads ativos permitidos por organização e perfil. O usuário visualiza os leads e move um lead para outra coluna. O sistema valida a permissão sobre o lead e o status ou coluna de destino. Se a permissão ou o destino forem inválidos, a ação é bloqueada, um aviso é exibido, a tentativa é registrada em log e o processo termina. Se tudo estiver válido, o sistema aplica movimentação visual temporária, atualiza o status no banco e registra evento automático no histórico. Se a atualização falhar, a movimentação visual é revertida e um aviso é exibido. Se for concluída com sucesso, o Kanban atualizado é confirmado e o processo é finalizado.](./modelagem_processos/fluxo_movimentacao_kanban.png)

A movimentação de lead no Kanban deverá atualizar o status do lead e gerar registro automático no histórico.

## 12.4 Atribuição ou troca de responsável pelo lead

```text
Administrador ou Gestor Comercial seleciona novo responsável
        |
        v
Sistema valida permissão da ação
        |
        v
Sistema valida se o novo responsável possui vínculo ativo na organização
        |
        v
Sistema atualiza o responsável do lead
        |
        v
Sistema registra evento automático no histórico
        |
        v
Lead passa a aparecer no escopo do novo responsável
```

A troca de responsável não deverá apagar histórico, tarefas ou interações anteriores.

## 12.5 Fluxo de Registro de Interação

```text
Usuário acessa detalhes do lead
        |
        v
Sistema valida permissão sobre o lead
        |
        v
Usuário registra uma interação manual
        |
        v
Sistema valida tipo e descrição
        |
        v
Sistema registra usuário, data, tipo e lead relacionado
        |
        v
Interação aparece no histórico do lead
```

O histórico deverá combinar interações manuais e eventos automáticos gerados pelo próprio sistema.

## 12.6 Fluxo de Criação de Tarefa

```text
Usuário acessa detalhes do lead
        |
        v
Sistema valida permissão sobre o lead
        |
        v
Usuário cria tarefa vinculada ao lead
        |
        v
Sistema valida título, responsável e data de vencimento
        |
        v
Sistema salva tarefa como pendente
        |
        v
Sistema pode registrar evento automático no histórico, quando aplicável
        |
        v
Tarefa passa a aparecer nas telas e indicadores conforme escopo
```

Toda tarefa deverá estar vinculada a um lead e possuir responsável ativo na organização.

## 12.7 Fluxo de Conclusão de Tarefa

```text
Usuário autorizado marca tarefa como concluída
        |
        v
Sistema valida permissão sobre a tarefa
        |
        v
Sistema atualiza status para concluída
        |
        v
Sistema registra data de conclusão e usuário responsável pela conclusão
        |
        v
Tarefa deixa de ser considerada pendente ou atrasada
```

Tarefas concluídas não deverão ser consideradas atrasadas.

## 12.8 Fluxo de Arquivamento de Lead

```text
Administrador ou Gestor Comercial solicita arquivamento
        |
        v
Sistema valida permissão e escopo do lead
        |
        v
Sistema registra data de arquivamento
        |
        v
Sistema registra usuário responsável pelo arquivamento
        |
        v
Sistema pode registrar motivo do arquivamento
        |
        v
Sistema registra evento automático no histórico
        |
        v
Lead sai do fluxo ativo padrão
```

O arquivamento não deverá alterar o status comercial do lead. Um lead arquivado deverá preservar seus dados, tarefas e histórico.

## 12.9 Fluxo de Dashboard

```text
Usuário acessa dashboard
        |
        v
Sistema identifica organização atual
        |
        v
Sistema identifica perfil e escopo do usuário
        |
        v
Sistema executa consultas agregadas simples
        |
        v
Sistema retorna cards, contadores e gráficos básicos
```

O dashboard deverá priorizar indicadores simples e leitura rápida. Relatórios analíticos avançados não fazem parte do MVP.

## 13. Integração com Banco de Dados

A aplicação deverá utilizar banco de dados relacional para persistir os dados principais do MVP.

As principais entidades consideradas pela arquitetura são:

| Entidade                           | Tabela esperada         |
| ---------------------------------- | ----------------------- |
| Organização                        | `organizations`         |
| Usuário                            | `users`                 |
| Vínculo do usuário com organização | `organization_users`    |
| Lead                               | `leads`                 |
| Status do lead                     | `lead_statuses`         |
| Origem do lead                     | `lead_sources`          |
| Histórico do lead                  | `lead_interactions`     |
| Tarefa                             | `tasks`                 |
| Configurações da organização       | `organization_settings` |

A arquitetura deverá respeitar a modelagem definida no documento de banco de dados, principalmente quanto ao uso de `organization_id`, separação entre `users` e `organization_users`, uso de `organization_user_id` para responsáveis e registros operacionais, e preservação de dados por meio de arquivamento.

## 14. Transações e Consistência

Operações que alteram múltiplos dados relacionados deverão ser executadas de forma consistente.

Devem ser tratadas como operações transacionais, sempre que a tecnologia utilizada permitir:

- Criar lead e definir responsável.
- Mover lead no Kanban e registrar evento no histórico.
- Trocar responsável e registrar evento no histórico.
- Arquivar lead e registrar evento no histórico.
- Reativar lead e registrar evento no histórico.
- Criar tarefa e registrar evento relacionado, quando aplicável.
- Concluir tarefa e registrar responsável pela conclusão.

O objetivo é evitar situações em que o dado principal seja alterado, mas o histórico obrigatório não seja registrado.

## 15. Segurança e Proteção de Dados

A arquitetura deverá considerar segurança básica desde o MVP.

Critérios arquiteturais:

- Proteger a área interna com autenticação.
- Armazenar senhas de forma segura.
- Nunca exibir senhas em texto puro.
- Aplicar permissões no backend.
- Restringir consultas por organização.
- Restringir dados conforme perfil do usuário.
- Evitar exposição de dados sensíveis em URLs, mensagens de erro ou telas indevidas.
- Separar rotas públicas de rotas autenticadas.
- Impedir que o formulário público consulte dados internos.
- Validar todos os formulários antes de persistir dados.
- Exibir mensagens claras sem detalhes técnicos para usuários finais.

O MVP não exigirá uma camada jurídica completa de conformidade, mas deverá adotar cuidados básicos com dados pessoais, especialmente nome, e-mail, telefone e empresa dos leads.

## 16. Proteção do Formulário Público

O formulário público deverá possuir proteção básica contra abuso e spam.

A arquitetura deverá prever pelo menos uma estratégia simples, como:

- Rate limit por IP ou intervalo de tempo.
- Honeypot.
- Captcha simples.
- Bloqueio temporário em caso de excesso de envios.
- Registro técnico opcional de IP e user agent para diagnóstico e proteção contra abuso.

A proteção não deverá impedir o uso normal por visitantes legítimos.

O formulário também deverá exibir aviso simples informando que os dados enviados serão utilizados para retorno comercial.

## 17. Desempenho

O MVP deverá apresentar desempenho adequado para uma pequena equipe comercial.

Decisões arquiteturais esperadas:

- Utilizar paginação ou carregamento controlado em listagens.
- Evitar carregar todos os registros sem necessidade.
- Aplicar filtros no banco de dados, não apenas na interface.
- Utilizar índices recomendados na modelagem.
- Evitar consultas repetitivas desnecessárias.
- Evitar problemas de carregamento excessivo de relacionamentos.
- Manter o dashboard com agregações simples.
- Priorizar consultas por organização, status, origem, responsável, datas e arquivamento.

O MVP deverá ser adequado para pequenas equipes e volume inicial de centenas ou poucos milhares de leads, sem exigir otimizações próprias de grandes ambientes corporativos.

## 18. Logs e Diagnóstico

A aplicação deverá possuir registro básico de erros técnicos para apoiar desenvolvimento, homologação e manutenção.

Critérios esperados:

- Registrar falhas inesperadas em logs internos.
- Não exibir stack trace ou detalhes técnicos para usuários finais.
- Registrar erros relevantes de execução.
- Permitir diagnóstico de problemas em cadastro, autenticação, permissões, formulário público, Kanban e dashboard.
- Manter mensagens amigáveis na interface.

Monitoramento avançado em tempo real não faz parte do MVP.

## 19. Backup e Preservação de Dados

A arquitetura deverá prever rotina básica de backup dos dados principais do MVP.

Dados que deverão ser considerados prioritários:

- Usuários.
- Organizações.
- Vínculos de usuários com organização.
- Leads.
- Status e origens.
- Interações e eventos do histórico.
- Tarefas.
- Configurações da organização.

O MVP não exigirá painel de backup, restauração avançada ou infraestrutura complexa de recuperação. Porém, deverá existir previsão operacional para cópia periódica do banco de dados ou mecanismo equivalente definido no ambiente de implantação.

Além do backup, a própria arquitetura deverá favorecer preservação de dados por meio de:

- Arquivamento em vez de exclusão definitiva.
- Preservação de histórico do lead.
- Preservação de tarefas vinculadas.
- Registro de eventos automáticos para ações importantes.

## 20. Organização do Código

O código deverá ser organizado de forma clara, favorecendo manutenção e evolução.

Recomendações:

- Separar módulos por domínio funcional.
- Evitar controllers com regras de negócio extensas.
- Centralizar regras de permissão.
- Centralizar resolução da organização atual.
- Criar serviços para fluxos importantes.
- Usar validações específicas para formulários e ações.
- Nomear classes, rotas, métodos e componentes de forma clara.
- Evitar duplicação de lógica entre listagem, Kanban, detalhes e dashboard.
- Manter consistência entre modelos, banco de dados e regras de negócio.

Caso a implementação utilize um framework MVC, a arquitetura poderá ser mapeada para recursos como controllers, models, services, requests, policies, middlewares, migrations e views ou componentes equivalentes.

## 21. Estrutura Sugerida de Módulos

Uma estrutura lógica possível para a aplicação é:

```text
app/
    Auth/
    Organizations/
    OrganizationUsers/
    Leads/
    Pipeline/
    LeadInteractions/
    Tasks/
    Dashboard/
    PublicLeadCapture/
    Settings/
    Shared/
```

Essa estrutura é apenas uma orientação conceitual. A estrutura final poderá variar conforme a tecnologia escolhida, desde que preserve a separação de responsabilidades.

## 22. Decisões Arquiteturais do MVP

| Decisão                    | Diretriz                                                |
| -------------------------- | ------------------------------------------------------- |
| Tipo de aplicação          | Aplicação web                                           |
| Estilo arquitetural        | Monólito modular                                        |
| Banco de dados             | Relacional                                              |
| Multi-tenant               | Preparação estrutural, sem operação multi-tenant no MVP |
| Organização atual          | Organização principal resolvida de forma centralizada   |
| Permissões                 | Baseadas no vínculo do usuário com a organização        |
| Histórico                  | Interações manuais e eventos automáticos centralizados  |
| Tarefas                    | Sempre vinculadas a leads                               |
| Dashboard                  | Indicadores simples por consultas agregadas             |
| Formulário público         | Rota pública separada, com validação e proteção básica  |
| Backup                     | Rotina ou previsão básica, sem painel avançado          |
| Integrações externas       | Fora do MVP                                             |
| Microsserviços             | Fora do MVP                                             |
| Notificações automáticas   | Fora do MVP                                             |
| API pública para terceiros | Fora do MVP                                             |

## 23. Itens Fora da Arquitetura do MVP

Os itens abaixo não deverão ser implementados na arquitetura inicial do MVP:

- Microsserviços.
- Infraestrutura distribuída.
- Balanceamento de carga.
- Alta disponibilidade complexa.
- Aplicativo mobile nativo.
- Funcionamento offline.
- API pública para terceiros.
- Integrações reais com WhatsApp, Instagram, LinkedIn, Google Ads ou e-mail.
- Envio automático de e-mails.
- Notificações push.
- Automação avançada de funil.
- Inteligência artificial.
- Relatórios analíticos avançados.
- Painel de tenants.
- Subdomínios por organização.
- Planos de assinatura.
- Cobrança recorrente.
- Painel avançado de backup e restauração.
- Personalização avançada de permissões.
- Personalização avançada de pipeline.
- Exclusão definitiva de leads como fluxo comum.

Esses recursos poderão ser avaliados em versões futuras, após a validação do MVP.

## 24. Critérios de Validação da Arquitetura

A arquitetura será considerada adequada para o MVP quando permitir:

- Acessar o sistema por navegador moderno.
- Proteger a área interna por login.
- Separar rotas públicas de rotas autenticadas.
- Criar, autenticar e gerenciar usuários da organização.
- Diferenciar Administrador, Gestor Comercial e Vendedor / SDR.
- Aplicar permissões no backend e na interface.
- Impedir que Vendedor / SDR acesse leads fora do seu escopo.
- Manter todos os dados operacionais vinculados à organização atual.
- Cadastrar, editar, listar, filtrar e buscar leads.
- Exibir pipeline Kanban por status.
- Atualizar status ao mover lead no Kanban.
- Registrar evento automático ao mudar status, trocar responsável, arquivar ou reativar lead.
- Exibir página de detalhes do lead com dados, histórico e tarefas.
- Criar e concluir tarefas relacionadas a leads.
- Identificar tarefas pendentes e atrasadas.
- Calcular dashboard geral e individual conforme escopo de acesso.
- Criar lead automaticamente pelo formulário público.
- Aplicar origem Site e status Novo ao lead do formulário público.
- Permitir que leads públicos iniciem sem responsável.
- Preservar dados, histórico e tarefas em arquivamentos.
- Prever rotina básica de backup dos dados principais.
- Registrar erros técnicos sem expor detalhes ao usuário final.
- Manter organização técnica suficiente para manutenção e evolução futura.

## 25. Observações Finais

A arquitetura do LeadFlow CRM deverá priorizar simplicidade, clareza, segurança básica, organização técnica e preservação dos dados comerciais.

O MVP não deverá tentar resolver problemas de escala, automação ou integração que pertencem a versões futuras. A primeira versão deverá validar o fluxo principal de gestão de leads com uma base técnica sólida, mas sem complexidade desnecessária.

A preparação para multi-tenant deverá existir na estrutura do sistema, especialmente no uso de organização atual, vínculos organizacionais e escopo por `organization_id`. Porém, essa preparação não deverá aparecer como complexidade operacional para o usuário final.

Este documento deverá servir como referência para os próximos documentos técnicos, especialmente API endpoints, telas e fluxos, backlog, plano de desenvolvimento e plano de testes.
