\# Escopo do MVP



\## 1. Objetivo do Documento



Este documento tem como objetivo definir o escopo do MVP do \*\*LeadFlow CRM\*\*, estabelecendo quais funcionalidades deverão fazer parte da primeira versão funcional do sistema e quais recursos ficarão fora deste primeiro ciclo de desenvolvimento.



O escopo do MVP serve como referência para orientar o planejamento, a priorização, o desenvolvimento, os testes e a validação inicial do produto.



Este documento também tem a função de evitar aumento indevido de escopo, mantendo o foco nas funcionalidades essenciais para validar a proposta principal do sistema: centralizar, organizar e acompanhar leads em uma pequena equipe comercial.



\## 2. Contexto do MVP



O LeadFlow CRM será desenvolvido para atender pequenas equipes comerciais que atualmente recebem leads por diferentes canais, como site, Instagram, LinkedIn, indicação, Google Ads, eventos e WhatsApp.



Atualmente, esses contatos ficam espalhados em planilhas, conversas, anotações soltas e ferramentas desconectadas. Isso dificulta o acompanhamento das oportunidades, prejudica a distribuição de responsabilidades e aumenta o risco de leads serem esquecidos ou mal acompanhados.



O MVP deve resolver esse problema central por meio de uma solução web simples, organizada e funcional, permitindo que a equipe cadastre leads, acompanhe o andamento das oportunidades, registre interações, crie tarefas de acompanhamento e visualize indicadores básicos da operação comercial.



\## 3. Objetivo do MVP



O objetivo do MVP é entregar uma primeira versão funcional do LeadFlow CRM, capaz de validar o fluxo principal de gestão de leads.



Nesta primeira versão, o sistema deve permitir que uma pequena equipe comercial consiga:



\* Centralizar os leads em um único sistema.

\* Cadastrar e consultar informações dos leads.

\* Acompanhar oportunidades em um pipeline visual.

\* Mover leads entre etapas do processo comercial.

\* Registrar interações realizadas com cada lead.

\* Criar tarefas e lembretes de acompanhamento.

\* Visualizar indicadores básicos da operação comercial.

\* Capturar leads por meio de um formulário público.

\* Controlar o acesso dos usuários conforme seus perfis.



O MVP não tem como objetivo entregar uma plataforma completa de automação comercial, mas sim validar a estrutura principal de um CRM funcional e bem organizado.



\## 4. Funcionalidades Incluídas no MVP



\## 4.1 Autenticação e Usuários



O sistema deverá possuir autenticação de usuários para permitir acesso seguro à área interna do CRM.



O MVP deverá permitir que usuários acessem o sistema por meio de login e senha, com controle básico de sessão.



Também deverá existir uma estrutura inicial de usuários com perfis de acesso, permitindo diferenciar as permissões entre Administrador, Gestor Comercial e Vendedor / SDR.



Funcionalidades previstas:



\* Login de usuários.

\* Logout de usuários.

\* Proteção de rotas internas.

\* Cadastro de usuários.

\* Edição de usuários.

\* Definição de perfil de acesso.

\* Controle básico de permissões por perfil.



\## 4.2 Gestão de Leads



O sistema deverá permitir o cadastro e gerenciamento dos leads recebidos pela equipe comercial.



Cada lead deverá conter as informações principais necessárias para identificação, acompanhamento e qualificação da oportunidade.



Campos mínimos previstos para o lead:



\* Nome.

\* E-mail.

\* Telefone.

\* Empresa.

\* Origem do contato.

\* Interesse demonstrado.

\* Responsável pelo atendimento.

\* Observações.

\* Status atual.

\* Data de cadastro.

\* Data da última atualização.



Origens iniciais previstas:



\* Site.

\* Instagram.

\* LinkedIn.

\* Indicação.

\* Google Ads.

\* Eventos.

\* WhatsApp.

\* Outro.



Funcionalidades previstas:



\* Cadastro de leads.

\* Edição de leads.

\* Visualização de leads.

\* Listagem de leads.

\* Busca por nome, e-mail, telefone ou empresa.

\* Filtro por status.

\* Filtro por origem.

\* Filtro por responsável.

\* Definição ou alteração do responsável pelo lead, conforme permissão do usuário.

\* Arquivamento ou inativação de leads, quando necessário.



A exclusão definitiva de leads não será priorizada no MVP. Quando um lead não precisar mais aparecer no fluxo ativo, o sistema deverá preferencialmente permitir seu arquivamento ou inativação.



\## 4.3 Pipeline Kanban



O sistema deverá possuir um pipeline visual em formato Kanban para acompanhamento das oportunidades comerciais.



O Kanban será uma das principais telas do MVP, permitindo que a equipe visualize rapidamente em qual etapa cada lead está e quais oportunidades precisam de atenção.



Status iniciais do pipeline:



\* Novo.

\* Em contato.

\* Qualificado.

\* Proposta enviada.

\* Negociação.

\* Ganho.

\* Perdido.



Funcionalidades previstas:



\* Visualização dos leads separados por status.

\* Movimentação de leads entre etapas do pipeline.

\* Atualização automática do status ao mover um lead.

\* Visualização resumida dos dados principais do lead no card.

\* Acesso aos detalhes do lead a partir do card.

\* Respeito às permissões de cada perfil de usuário.



O Vendedor / SDR deverá visualizar e mover apenas os leads atribuídos a ele ou cadastrados por ele, conforme regra de permissão.



O Gestor Comercial e o Administrador deverão ter acesso ao pipeline geral, podendo visualizar e mover leads da equipe.



\## 4.4 Página de Detalhes do Lead



Cada lead deverá possuir uma página de detalhes com informações completas da oportunidade.



Essa página deverá permitir que usuários autorizados entendam o contexto do lead antes de realizar novos contatos ou atualizações.



Informações previstas:



\* Dados principais do lead.

\* Origem do contato.

\* Interesse demonstrado.

\* Responsável atual.

\* Status atual.

\* Observações gerais.

\* Histórico de interações.

\* Tarefas relacionadas.

\* Datas importantes, como cadastro e última atualização.



Funcionalidades previstas:



\* Visualizar informações completas do lead.

\* Editar informações do lead, conforme permissão.

\* Consultar histórico de interações.

\* Consultar tarefas vinculadas ao lead.

\* Registrar novas interações.

\* Criar novas tarefas relacionadas ao lead.

\* Alterar status da oportunidade, conforme permissão.



\## 4.5 Histórico de Interações



O sistema deverá permitir o registro de interações realizadas com cada lead.



O histórico será usado para manter o contexto do atendimento e evitar perda de informações importantes durante o processo comercial.



Tipos de interação previstos:



\* Ligação.

\* WhatsApp.

\* E-mail.

\* Reunião.

\* Observação interna.

\* Envio de proposta.

\* Mudança de status.

\* Outro tipo de contato.



Informações mínimas da interação:



\* Tipo de interação.

\* Descrição.

\* Usuário responsável pelo registro.

\* Data e hora do registro.

\* Lead relacionado.



Funcionalidades previstas:



\* Registrar interação em um lead.

\* Listar interações em ordem cronológica.

\* Visualizar quem registrou cada interação.

\* Visualizar quando cada interação foi registrada.

\* Registrar observações relevantes sobre o atendimento.



No MVP, o histórico será manual. Não haverá integração automática com WhatsApp, e-mail ou outras ferramentas externas.



\## 4.6 Tarefas e Lembretes



O sistema deverá permitir a criação de tarefas relacionadas aos leads.



As tarefas servirão para organizar follow-ups, retornos, reuniões, envio de propostas e outras ações comerciais necessárias durante o acompanhamento da oportunidade.



Informações mínimas da tarefa:



\* Título.

\* Descrição.

\* Lead relacionado.

\* Responsável pela tarefa.

\* Data de vencimento.

\* Status da tarefa.

\* Data de criação.

\* Data de conclusão, quando aplicável.



Status iniciais da tarefa:



\* Pendente.

\* Concluída.



Funcionalidades previstas:



\* Criar tarefa para um lead.

\* Editar tarefa.

\* Marcar tarefa como concluída.

\* Listar tarefas vinculadas a um lead.

\* Visualizar tarefas pendentes.

\* Identificar tarefas atrasadas.

\* Filtrar tarefas por responsável, quando aplicável.



O Vendedor / SDR deverá criar e acompanhar tarefas relacionadas aos próprios leads.



O Gestor Comercial deverá visualizar tarefas pendentes e atrasadas da equipe, além de poder criar tarefas para vendedores.



O Administrador deverá ter acesso amplo às tarefas do sistema.



No MVP, o lembrete será tratado de forma simples, por meio da data de vencimento da tarefa e da indicação visual de atraso quando a tarefa não for concluída dentro do prazo. Notificações automáticas, alertas por e-mail, push ou integrações externas de lembrete não fazem parte desta primeira versão.



\## 4.7 Dashboard Básico



O sistema deverá possuir um dashboard inicial com indicadores básicos da operação comercial.



O objetivo do dashboard no MVP é oferecer uma visão rápida da situação dos leads, sem a necessidade de relatórios avançados ou análises complexas.



Indicadores previstos:



\* Total de leads cadastrados.

\* Leads novos no mês.

\* Leads ganhos.

\* Leads perdidos.

\* Taxa de conversão.

\* Tarefas atrasadas.

\* Leads por status.

\* Leads por origem.

\* Evolução de oportunidades ao longo do tempo.



Funcionalidades previstas:



\* Visualização de indicadores gerais.

\* Visualização de gráficos ou cards simples.

\* Filtros básicos, quando necessário.

\* Dashboard geral para Administrador e Gestor Comercial.

\* Dashboard individual para Vendedor / SDR.



No MVP, o dashboard deverá ser simples e objetivo, composto por cards, contadores e gráficos básicos. Relatórios analíticos avançados, painéis altamente customizáveis e análises comerciais complexas ficarão fora do escopo inicial.



\## 4.8 Formulário Público de Captura



O sistema deverá possuir um formulário público de captura de leads.



Esse formulário poderá ser usado como página de contato ou solicitação de orçamento, permitindo que um possível cliente envie seus dados sem precisar acessar a área interna do CRM.



Campos mínimos previstos no formulário público:



\* Nome.

\* E-mail.

\* Telefone.

\* Empresa.

\* Interesse demonstrado.

\* Mensagem ou observação.



Comportamento esperado:



\* Ao preencher o formulário, um novo lead deverá ser criado automaticamente no CRM.

\* A origem do lead deverá ser definida como Site.

\* O lead deverá entrar inicialmente com status Novo.

\* O lead poderá ficar sem responsável definido ou ser atribuído conforme regra inicial do sistema.



Funcionalidades previstas:



\* Exibição de formulário público.

\* Validação dos campos obrigatórios.

\* Cadastro automático do lead.

\* Confirmação visual após envio.

\* Registro da origem como Site.



No MVP, o formulário público não terá integração com ferramentas externas, campanhas, automações de marketing ou envio automático de e-mails.



\## 4.9 Permissões Básicas



O MVP deverá possuir controle básico de permissões considerando três perfis principais:



\* Administrador.

\* Gestor Comercial.

\* Vendedor / SDR.



\## 4.9.1 Administrador



O Administrador será responsável por gerenciar o sistema, usuários e permissões.



Permissões previstas:



\* Gerenciar usuários.

\* Definir perfis de acesso.

\* Visualizar todos os leads.

\* Criar e editar leads.

\* Arquivar ou inativar leads.

\* Atribuir leads a vendedores.

\* Trocar responsável por leads.

\* Acessar o pipeline completo.

\* Mover qualquer lead no Kanban.

\* Registrar interações.

\* Criar tarefas.

\* Criar tarefas para vendedores.

\* Visualizar dashboard geral.

\* Visualizar dashboard individual.

\* Gerenciar configurações básicas do sistema.



\## 4.9.2 Gestor Comercial



O Gestor Comercial será responsável por acompanhar a operação comercial e gerenciar a distribuição dos leads entre os vendedores.



Permissões previstas:



\* Visualizar todos os leads da equipe.

\* Criar leads.

\* Editar leads da equipe.

\* Atribuir leads a vendedores.

\* Trocar responsável por leads.

\* Acompanhar o pipeline completo.

\* Mover leads da equipe no Kanban.

\* Filtrar leads por responsável, origem e status.

\* Registrar interações.

\* Criar tarefas.

\* Criar tarefas para vendedores.

\* Visualizar tarefas pendentes da equipe.

\* Visualizar tarefas atrasadas da equipe.

\* Acompanhar a distribuição de leads entre vendedores.

\* Visualizar dashboard geral.

\* Visualizar dashboard individual.



\## 4.9.3 Vendedor / SDR



O Vendedor / SDR será responsável pelo atendimento direto dos leads atribuídos a ele ou cadastrados por ele próprio.



Permissões previstas:



\* Cadastrar novos leads.

\* Visualizar leads atribuídos a ele.

\* Visualizar leads cadastrados por ele próprio.

\* Editar informações dos seus próprios leads.

\* Registrar interações nos próprios leads.

\* Criar tarefas nos próprios leads.

\* Alterar o status das suas próprias oportunidades.

\* Mover seus próprios leads no pipeline Kanban.

\* Utilizar filtros e busca dentro da sua carteira de leads.

\* Visualizar dashboard individual.



\## 5. Funcionalidades Fora do Escopo do MVP



As funcionalidades abaixo não farão parte da primeira versão do sistema.



Elas poderão ser avaliadas futuramente, após a validação do MVP e conforme novas necessidades do negócio forem identificadas.



Fora do escopo inicial:



\* Integração real com WhatsApp.

\* Envio automático de e-mails.

\* Integração com ferramentas externas de e-mail marketing.

\* Integração com redes sociais.

\* Integração com LinkedIn, Instagram ou Google Ads.

\* Integração com gateways de pagamento.

\* Automações avançadas de funil.

\* Recursos de inteligência artificial.

\* Chat interno.

\* Discador telefônico.

\* Relatórios comerciais complexos.

\* Previsão avançada de vendas.

\* Gestão financeira.

\* Gestão de contratos.

\* Gestão de propostas com assinatura eletrônica.

\* Aplicativo mobile.

\* Notificações push.

\* API pública para terceiros.

\* Importação em massa por planilha.

\* Exportação avançada de dados.

\* Múltiplas empresas ou multi-tenant.

\* Personalização avançada de pipeline.

\* Exclusão definitiva de leads como fluxo comum.



\## 5.1 Observação sobre Multi-tenant



O MVP do LeadFlow CRM não contemplará multi-tenant completo nesta primeira versão.



Isso significa que o sistema não deverá incluir, neste momento, recursos como múltiplas empresas utilizando a plataforma em modelo SaaS, subdomínios por empresa, planos de assinatura, cobrança recorrente, painel de tenants, provisionamento automático de organizações ou isolamento avançado entre bases de clientes.



Apesar disso, a arquitetura do banco de dados e do software deverá nascer preparada para uma possível evolução futura para um modelo multi-tenant.



Mesmo operando inicialmente com uma única empresa, as principais entidades do sistema deverão ser modeladas com vínculo a uma empresa ou organização. Isso inclui, principalmente:



\* Usuários.

\* Leads.

\* Tarefas.

\* Interações.

\* Configurações.



Essa decisão tem como objetivo evitar complexidade desnecessária no MVP, mantendo o foco na validação do fluxo principal do CRM, mas reduzindo o risco de uma grande refatoração estrutural caso o LeadFlow evolua futuramente para um modelo SaaS ou multi-tenant.



\## 6. Regras Gerais do MVP



O MVP deverá seguir algumas regras gerais para manter o produto simples, funcional e coerente com sua proposta inicial.



Regras gerais:



\* O sistema deve ser web.

\* O foco principal é a gestão de leads.

\* O pipeline Kanban deve ser uma funcionalidade central do produto.

\* Todo lead deve possuir um status.

\* Todo lead deve possuir uma origem.

\* Todo lead pode ter um responsável.

\* Todo lead pode possuir interações.

\* Todo lead pode possuir tarefas.

\* Tarefas devem permitir identificação de atraso.

\* Vendedores devem acessar apenas leads atribuídos a eles ou cadastrados por eles.

\* Gestores Comerciais devem acompanhar a equipe e redistribuir leads quando necessário.

\* Administradores devem gerenciar usuários, permissões e configurações básicas.

\* Exclusão definitiva de leads deve ser evitada no MVP.

\* Leads que não devem aparecer no fluxo ativo devem ser arquivados ou inativados.

\* As condições específicas para arquivamento ou inativação de leads, incluindo quando essa ação poderá ser realizada por um Gestor Comercial e quando deverá ficar restrita ao Administrador, deverão ser detalhadas posteriormente no documento de regras de negócio.

\* Integrações externas devem ser simuladas ou deixadas para versões futuras.

\* O sistema deve priorizar clareza, simplicidade e organização.



\## 7. Perfis Atendidos no MVP



O MVP do LeadFlow CRM atenderá inicialmente três perfis de usuário.



| Perfil           | Papel principal                                      |

| ---------------- | ---------------------------------------------------- |

| Administrador    | Gerenciar sistema, usuários e permissões             |

| Gestor Comercial | Gerenciar a operação comercial e acompanhar a equipe |

| Vendedor / SDR   | Atender e acompanhar os próprios leads               |



\## 7.1 Administrador



O Administrador será atendido pelo MVP se conseguir gerenciar usuários, controlar permissões, visualizar o sistema de forma ampla e manter os dados operacionais organizados.



\## 7.2 Gestor Comercial



O Gestor Comercial será atendido pelo MVP se conseguir visualizar o pipeline completo, acompanhar a equipe, identificar tarefas pendentes ou atrasadas, atribuir leads e trocar responsáveis quando necessário.



\## 7.3 Vendedor / SDR



O Vendedor / SDR será atendido pelo MVP se conseguir cadastrar leads, acompanhar suas oportunidades, registrar interações, criar tarefas, mover leads no Kanban e visualizar sua carteira de forma clara.



\## 8. Critérios de Aceitação do MVP



O MVP será considerado funcional quando permitir a execução dos principais fluxos de uso definidos para o LeadFlow CRM.



Critérios mínimos de aceitação:



\* O usuário consegue acessar o sistema por login.

\* O Administrador consegue cadastrar e gerenciar usuários.

\* O sistema diferencia permissões entre Administrador, Gestor Comercial e Vendedor / SDR.

\* O usuário autorizado consegue cadastrar um lead.

\* O usuário autorizado consegue editar um lead.

\* O usuário autorizado consegue visualizar uma lista de leads.

\* A listagem permite busca e filtros básicos.

\* O lead possui status, origem e responsável.

\* O usuário autorizado consegue visualizar o pipeline Kanban.

\* O usuário autorizado consegue mover leads entre etapas do Kanban.

\* A mudança no Kanban atualiza o status do lead.

\* O usuário autorizado consegue acessar a página de detalhes do lead.

\* O usuário autorizado consegue registrar interações no lead.

\* O usuário autorizado consegue criar tarefas relacionadas ao lead.

\* O sistema indica tarefas pendentes.

\* O sistema indica tarefas atrasadas.

\* O dashboard exibe indicadores básicos da operação.

\* O formulário público permite cadastrar um lead automaticamente.

\* Leads enviados pelo formulário público entram com origem Site.

\* O Vendedor / SDR visualiza apenas leads atribuídos a ele ou cadastrados por ele.

\* O Gestor Comercial consegue visualizar leads e tarefas da equipe.

\* O Administrador consegue visualizar e gerenciar os dados principais do sistema.

\* O sistema permite arquivar ou inativar leads.

\* O sistema evita exclusão definitiva de leads como fluxo comum do MVP.



\## 9. Critérios de Sucesso



O MVP será considerado bem-sucedido se permitir que uma pequena equipe comercial substitua controles manuais espalhados por um sistema único e organizado.



Critérios de sucesso:



\* A equipe consegue cadastrar e consultar leads em um único lugar.

\* Os vendedores conseguem acompanhar suas oportunidades sem depender de planilhas.

\* O gestor consegue visualizar o andamento geral do pipeline.

\* A equipe consegue identificar leads sem acompanhamento.

\* A equipe consegue registrar o histórico básico de contatos.

\* A equipe consegue criar tarefas de follow-up.

\* O sistema ajuda a reduzir esquecimentos e atrasos no atendimento.

\* O dashboard oferece uma visão básica da operação comercial.

\* O formulário público simula um fluxo real de entrada de leads.

\* O sistema transmite a sensação de um produto real, com fluxo claro e interface organizada.



\## 10. Observações



Este documento define o escopo inicial do MVP do LeadFlow CRM.



As funcionalidades descritas aqui deverão orientar os próximos documentos de planejamento, como requisitos funcionais, requisitos não funcionais, regras de negócio, modelagem de banco de dados, arquitetura, endpoints, telas, backlog e plano de desenvolvimento.



Qualquer funcionalidade não descrita como parte do MVP deverá ser considerada fora do escopo inicial, salvo decisão posterior registrada em documento próprio.



O objetivo desta primeira versão é validar o fluxo principal de gestão de leads, mantendo o produto simples, funcional e alinhado às necessidades de uma pequena equipe comercial.



O escopo do MVP foi aprovado pelo cliente como representação adequada da primeira versão do LeadFlow CRM, estando coerente com o briefing, com as personas definidas e com a proposta de MVP. As observações realizadas pelo cliente foram incorporadas como refinamentos pontuais, sem alteração estrutural do escopo aprovado.



