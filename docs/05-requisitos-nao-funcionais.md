# Requisitos Não Funcionais

## 1. Objetivo do Documento

Este documento tem como objetivo definir os requisitos não funcionais do **LeadFlow CRM**, estabelecendo critérios de qualidade, segurança, usabilidade, desempenho, disponibilidade, manutenção e evolução técnica esperados para o MVP.

Os requisitos não funcionais descrevem como o sistema deve se comportar, complementando os requisitos funcionais e ajudando a orientar decisões de arquitetura, desenvolvimento, testes e validação do produto.

## 2. Contexto

O LeadFlow CRM será um sistema web voltado para pequenas equipes comerciais que precisam centralizar, organizar e acompanhar leads recebidos por diferentes canais.

O MVP deverá entregar uma solução simples, funcional e organizada, com login, gestão de leads, pipeline Kanban, histórico de interações, tarefas, dashboard básico, formulário público de captura e controle simples de permissões.

Por se tratar de um sistema que armazenará dados comerciais e informações de contato de possíveis clientes, é importante que a primeira versão já considere requisitos mínimos de segurança, confiabilidade, organização técnica, proteção dos dados e preservação das informações principais do sistema.

## 3. Requisitos Não Funcionais

## RNF001 - Sistema Web

O LeadFlow CRM deverá ser desenvolvido como uma aplicação web, acessível por navegador.

O sistema deverá funcionar sem necessidade de instalação local por parte dos usuários finais.

Critérios esperados:

- Acesso por navegador moderno.

- Interface web para todos os perfis de usuário.

- Área interna protegida por autenticação.

- Formulário público acessível sem login.

## RNF002 - Interface Simples e Objetiva

A interface do sistema deverá ser simples, clara e objetiva, considerando que o público-alvo é uma pequena equipe comercial e não usuários técnicos.

O sistema deve priorizar facilidade de uso, clareza visual e rapidez na execução das ações principais.

Critérios esperados:

- Telas organizadas e fáceis de entender.

- Botões e ações com nomes claros.

- Fluxos simples para cadastro, edição e acompanhamento de leads.

- Redução de etapas desnecessárias para tarefas recorrentes.

- Informações principais visíveis sem excesso de complexidade.

## RNF003 - Usabilidade do Pipeline Kanban

O pipeline Kanban deverá oferecer uma experiência visual clara para acompanhamento dos leads por status.

Como o Kanban é uma funcionalidade central do produto, sua usabilidade deve ser priorizada no MVP.

Critérios esperados:

- Colunas bem identificadas por status.

- Cards de leads com informações resumidas e relevantes.

- Movimentação simples de leads entre etapas.

- Atualização visual clara após mudança de status.

- Acesso fácil aos detalhes do lead a partir do card.

- Comportamento coerente com as permissões do usuário logado.

## RNF004 - Responsividade Básica

O sistema deverá possuir responsividade básica para permitir uso em diferentes tamanhos de tela.

O foco principal do MVP será o uso em desktop ou notebook, mas a interface não deverá quebrar em telas menores.

Critérios esperados:

- Boa experiência em desktop e notebook.

- Layout minimamente adaptável para tablets.

- Telas principais acessíveis em dispositivos móveis, ainda que não otimizadas como aplicativo.

- Menus, tabelas, cards e formulários sem sobreposição grave de elementos.

## RNF005 - Compatibilidade com Navegadores Modernos

O sistema deverá funcionar corretamente nos principais navegadores modernos.

Critérios esperados:

- Compatibilidade com versões recentes do Google Chrome.

- Compatibilidade com versões recentes do Microsoft Edge.

- Compatibilidade com versões recentes do Mozilla Firefox.

- Uso de recursos web estáveis e amplamente suportados.

- Evitar dependência de funcionalidades experimentais do navegador.

## RNF006 - Desempenho Geral

O sistema deverá apresentar desempenho adequado para uma pequena equipe comercial utilizando o MVP.

As principais telas devem carregar em poucos segundos em condições normais de uso do MVP, considerando volume inicial compatível com uma pequena operação comercial.

Critérios esperados:

- Login com resposta rápida.

- Listagem de leads carregando em poucos segundos em condições normais de uso.

- Filtros e buscas com resposta em poucos segundos para o volume esperado do MVP.

- Pipeline Kanban carregando sem lentidão excessiva para uma pequena equipe comercial.

- Dashboard com indicadores básicos sem processamento pesado.

- Evitar consultas desnecessárias ou carregamento excessivo de dados.

- Priorizar paginação, filtros ou carregamento controlado quando houver crescimento da base de leads.

## RNF007 - Volume Inicial de Dados

O MVP deverá ser planejado para atender uma pequena operação comercial.

Não é necessário otimizar a primeira versão para grandes volumes empresariais, mas o sistema não deve nascer limitado a poucos registros.

Critérios esperados:

- Suportar uma pequena equipe de usuários.

- Suportar centenas ou poucos milhares de leads sem degradação grave.

- Permitir crescimento gradual da base de leads.

- Estrutura de dados organizada para evolução futura.

## RNF008 - Segurança de Acesso

O sistema deverá proteger a área interna por meio de autenticação de usuários.

Usuários não autenticados não poderão acessar telas internas, dados de leads, tarefas, dashboards ou configurações administrativas.

Critérios esperados:

- Login obrigatório para área interna.

- Logout disponível para todos os usuários autenticados.

- Proteção de rotas internas.

- Sessões de usuário controladas.

- Redirecionamento de usuários não autenticados para a tela de login.

- Senhas de usuários armazenadas de forma segura, utilizando práticas adequadas de proteção.

- Senhas nunca exibidas em texto puro.

- Senhas não armazenadas de forma visível ou reversível.

## RNF009 - Controle de Permissões

O sistema deverá respeitar as permissões definidas para os perfis de usuário do MVP: Administrador, Gestor Comercial e Vendedor / SDR.

As permissões devem ser aplicadas tanto na interface quanto no backend, evitando que usuários acessem dados ou executem ações fora do seu perfil.

Critérios esperados:

- Administrador com acesso amplo ao sistema.

- Gestor Comercial com acesso à operação comercial e leads da equipe.

- Vendedor / SDR com acesso restrito aos leads atribuídos a ele ou cadastrados por ele.

- Bloqueio de ações não permitidas.

- Ocultação ou desabilitação de opções indevidas na interface.

- Validação de permissão no servidor, não apenas na tela.

## RNF010 - Proteção de Dados Comerciais

O sistema deverá proteger os dados comerciais cadastrados, incluindo informações dos leads, histórico de interações, tarefas e dados de usuários.

Critérios esperados:

- Usuários devem visualizar apenas dados permitidos pelo seu perfil.

- Dados sensíveis não devem ser expostos em URLs, mensagens de erro ou telas indevidas.

- Acesso ao formulário público não deve permitir consulta de dados internos.

- Informações de leads devem ser preservadas sempre que possível.

- Exclusão definitiva de leads deve ser evitada como fluxo comum do MVP.

## RNF011 - Tratamento Básico de Dados Pessoais

Como o sistema armazenará dados de contato de leads, o MVP deverá adotar cuidados básicos com dados pessoais.

O objetivo neste momento não é implementar uma camada jurídica completa de conformidade, mas garantir boas práticas mínimas de proteção e uso responsável das informações.

Critérios esperados:

- Coletar apenas dados necessários para o processo comercial.

- Evitar exposição indevida de nome, e-mail, telefone e empresa.

- Restringir acesso aos dados conforme perfil do usuário.

- Preservar histórico comercial de forma controlada.

- Evitar exclusão acidental ou perda indevida de informações.

- O formulário público deve informar de forma simples que os dados enviados serão utilizados para retorno comercial.

- O aviso de uso dos dados deve ser apresentado antes do envio do formulário público.

- A mensagem deve ser clara e objetiva, sem exigir uma estrutura jurídica complexa no MVP.

## RNF012 - Integridade dos Dados

O sistema deverá manter a consistência dos dados cadastrados.

As principais entidades do sistema, como leads, usuários, tarefas e interações, devem manter vínculos corretos entre si.

Critérios esperados:

- Todo lead deve possuir status válido.

- Todo lead deve possuir origem válida.

- Tarefas devem estar vinculadas a um lead quando aplicável.

- Interações devem estar vinculadas a um lead.

- Responsáveis por leads e tarefas devem ser usuários válidos.

- Alterações importantes não devem deixar registros inconsistentes.

## RNF013 - Validação de Formulários

Os formulários do sistema deverão possuir validações básicas para evitar cadastro de informações inválidas ou incompletas.

Critérios esperados:

- Campos obrigatórios devem ser validados.

- E-mails devem seguir formato válido.

- Datas de vencimento de tarefas devem ser tratadas corretamente.

- Mensagens de erro devem ser claras.

- O usuário deve entender o que precisa corrigir antes de salvar.

- O formulário público deve validar os campos necessários antes de criar o lead.

## RNF014 - Mensagens de Erro e Feedback ao Usuário

O sistema deverá fornecer feedback claro após ações importantes, como cadastro, edição, movimentação no Kanban, criação de tarefas e envio do formulário público.

Critérios esperados:

- Exibir confirmação após ações concluídas com sucesso.

- Exibir mensagens claras em caso de erro.

- Evitar mensagens técnicas para o usuário final.

- Informar quando uma ação não puder ser realizada por falta de permissão.

- Indicar visualmente tarefas atrasadas.

- Indicar visualmente estados importantes, como lead arquivado ou inativo.

## RNF015 - Disponibilidade Esperada para o MVP

O sistema deverá estar disponível para uso durante o período normal de trabalho da equipe comercial.

Por se tratar de um MVP, não é exigida alta disponibilidade complexa, infraestrutura distribuída ou redundância avançada.

Critérios esperados:

- Sistema disponível para uso interno da equipe.

- Evitar indisponibilidades frequentes durante o uso comum.

- Possibilidade de manutenção planejada quando necessário.

- Estrutura simples, compatível com o estágio inicial do produto.

## RNF016 - Recuperação, Backup e Preservação de Dados

O sistema deverá considerar mecanismos básicos para reduzir risco de perda de dados importantes.

Mesmo no MVP, dados de leads, usuários, interações e tarefas devem ser tratados como informações relevantes para a operação comercial.

Critérios esperados:

- Evitar exclusão definitiva como comportamento padrão.

- Preferir arquivamento ou inativação de leads.

- Preservar histórico de interações.

- Preservar tarefas vinculadas aos leads.

- Permitir ou prever rotina básica de backup dos dados principais do MVP.

- A rotina básica de backup deve considerar, principalmente, usuários, leads, tarefas e interações.

- Não será necessário painel de backup ou restauração avançada no MVP.

- Evitar que ações simples do usuário causem perda irreversível de dados.

- A estratégia de backup e recuperação poderá ser detalhada posteriormente no documento de arquitetura ou plano de infraestrutura.

## RNF017 - Rastreabilidade de Ações Importantes

O sistema deverá permitir rastrear, de forma básica, ações relevantes realizadas no contexto dos leads.

A rastreabilidade ajuda a equipe a entender o histórico da oportunidade e reduz dependência de registros manuais.

Critérios esperados:

- Registrar quem criou o lead.

- Registrar datas de criação e atualização.

- Registrar quem criou uma interação.

- Registrar quem criou ou concluiu uma tarefa.

- Registrar mudanças importantes no histórico do lead quando aplicável.

- Manter contexto mínimo das ações comerciais realizadas.

## RNF018 - Manutenibilidade do Código

O sistema deverá ser desenvolvido com organização suficiente para permitir manutenção e evolução após o MVP.

Critérios esperados:

- Separação clara entre responsabilidades do sistema.

- Código organizado por domínio ou módulo funcional.

- Nomes claros para entidades, rotas, telas e componentes.

- Evitar duplicações desnecessárias.

- Facilitar futuras alterações em leads, tarefas, permissões e dashboard.

- Manter estrutura preparada para documentação técnica posterior.

## RNF019 - Evolução Futura da Arquitetura

Mesmo que o MVP seja simples, a estrutura técnica deverá permitir evolução futura do produto.

O sistema não deve implementar recursos avançados antes da validação do MVP, mas também não deve ser construído de forma que dificulte melhorias posteriores.

Critérios esperados:

- Estrutura preparada para novos status de lead no futuro.

- Possibilidade de adicionar novas origens de lead.

- Possibilidade de evoluir permissões.

- Possibilidade de adicionar integrações externas futuramente.

- Possibilidade de evoluir o dashboard.

- Possibilidade de preparar o sistema para multi-tenant no futuro, sem implementar multi-tenant completo no MVP.

## RNF020 - Preparação para Multi-tenant Futuro

O MVP não contemplará multi-tenant completo, mas a modelagem e a arquitetura deverão evitar decisões que tornem essa evolução muito custosa.

Critérios esperados:

- Considerar vínculo das principais entidades a uma empresa ou organização.

- Evitar acoplamento rígido a uma única operação comercial.

- Não implementar subdomínios, cobrança, planos ou painel de tenants no MVP.

- Não aumentar a complexidade operacional da primeira versão.

- Manter a possibilidade de evolução futura para modelo SaaS.

## RNF021 - Simplicidade Operacional

O sistema deverá ser simples de operar e administrar no contexto de uma pequena equipe.

Critérios esperados:

- Administração básica de usuários.

- Perfis de acesso claros.

- Configurações iniciais simples.

- Baixa dependência de configurações técnicas por parte do usuário final.

- Fluxos administrativos objetivos.

## RNF022 - Consistência Visual

O sistema deverá manter consistência visual entre suas principais telas.

Critérios esperados:

- Padrão visual coerente entre listagem, Kanban, detalhes, tarefas e dashboard.

- Botões e ações semelhantes com comportamento semelhante.

- Cores, espaçamentos e componentes usados de forma consistente.

- Cards, tabelas e formulários com leitura clara.

- Interface com aparência de produto real.

## RNF023 - Acessibilidade Básica

O MVP deverá considerar boas práticas básicas de acessibilidade, mesmo sem exigir conformidade avançada neste primeiro momento.

Critérios esperados:

- Textos legíveis.

- Contraste adequado entre texto e fundo.

- Campos de formulário com rótulos claros.

- Botões identificáveis.

- Navegação compreensível.

- Mensagens de erro visíveis e objetivas.

## RNF024 - Logs e Diagnóstico Básico

O sistema deverá possuir condições mínimas para diagnóstico de problemas técnicos.

Critérios esperados:

- Erros relevantes devem ser registrados em ambiente apropriado.

- Falhas inesperadas não devem expor detalhes técnicos ao usuário final.

- Mensagens técnicas devem ficar restritas ao ambiente de desenvolvimento ou logs internos.

- Logs devem apoiar correções durante o desenvolvimento e homologação do MVP.

## RNF025 - Proteção Básica do Formulário Público Contra Abuso

O formulário público de captura deverá possuir medidas básicas para reduzir envios abusivos, automatizados ou caracterizados como spam.

Não é necessário implementar uma solução avançada no MVP, mas o sistema deve prever proteção mínima para evitar que o formulário público seja explorado indevidamente.

Critérios esperados:

- O formulário público deve possuir validações obrigatórias.

- O sistema deve prever medida básica contra envios excessivos.

- A solução técnica poderá utilizar rate limit, captcha simples, honeypot, bloqueio temporário ou outra estratégia definida posteriormente.

- O formulário público não deve permitir criação ilimitada e abusiva de leads em curto intervalo de tempo.

- Falhas ou bloqueios por proteção contra abuso devem exibir mensagem compreensível ao usuário.

- A proteção contra spam não deve impedir o uso normal do formulário por visitantes legítimos.

## RNF026 - Qualidade para Homologação

O MVP deverá ser entregue em condição adequada para testes e validação pelo cliente.

Critérios esperados:

- Principais fluxos funcionando de ponta a ponta.

- Telas sem erros visuais graves.

- Permissões básicas respeitadas.

- Dados cadastrados persistindo corretamente.

- Kanban atualizando status corretamente.

- Dashboard exibindo dados coerentes.

- Formulário público criando leads corretamente.

- Formulário público exibindo aviso simples sobre uso dos dados para contato comercial.

- Formulário público com proteção básica contra abuso ou spam.

- Tarefas indicando pendência, conclusão e atraso.

- Senhas tratadas de forma segura, sem armazenamento ou exibição em texto puro.

- Dados principais contemplados por rotina ou previsão básica de backup.

## 4. Restrições Não Funcionais do MVP

Alguns requisitos avançados não serão obrigatórios nesta primeira versão.

Não fazem parte dos requisitos não funcionais obrigatórios do MVP:

- Alta disponibilidade com múltiplos servidores.

- Balanceamento de carga.

- Infraestrutura distribuída.

- Aplicativo mobile nativo.

- Funcionamento offline.

- Notificações push.

- Integrações automáticas com WhatsApp, e-mail, redes sociais ou ferramentas externas.

- Relatórios analíticos avançados.

- Monitoramento avançado em tempo real.

- Multi-tenant completo.

- Painel avançado de backup e restauração.

- Criptografia avançada além das práticas padrão da aplicação.

- Customização avançada de interface por empresa.

- Automação comercial avançada.

Esses pontos poderão ser avaliados em versões futuras, conforme evolução do produto e validação do MVP.

## 5. Critérios Gerais de Aceitação

Os requisitos não funcionais serão considerados atendidos no MVP quando:

- O sistema puder ser acessado por navegador moderno.

- A área interna estiver protegida por login.

- As senhas forem armazenadas de forma segura e nunca exibidas em texto puro.

- As permissões básicas forem respeitadas.

- Vendedores não conseguirem acessar leads fora do seu escopo permitido.

- O pipeline Kanban for simples e utilizável.

- As principais telas carregarem em poucos segundos em condições normais de uso do MVP.

- Os dados principais forem preservados corretamente.

- Existir rotina ou previsão básica de backup para os dados principais do MVP.

- Os formulários validarem informações obrigatórias.

- O formulário público informar que os dados serão usados para retorno comercial.

- O formulário público possuir medida básica contra abuso ou spam.

- As mensagens de erro e sucesso forem compreensíveis.

- A interface for clara, consistente e adequada para uma pequena equipe comercial.

- O sistema estiver tecnicamente organizado para manutenção e evolução futura.

## 6. Observações

Os requisitos não funcionais descritos neste documento devem orientar decisões técnicas e de experiência do usuário durante o desenvolvimento do MVP do LeadFlow CRM.

O objetivo não é criar uma infraestrutura complexa ou uma plataforma corporativa avançada na primeira versão, mas garantir que o MVP seja seguro, organizado, utilizável, consistente e preparado para evoluir.

Sempre que houver conflito entre simplicidade e complexidade técnica, o MVP deverá priorizar simplicidade, desde que isso não comprometa segurança básica, integridade dos dados, controle de permissões, proteção mínima dos dados, preservação das informações principais e possibilidade razoável de evolução futura.

O documento foi aprovado com ajustes pontuais pelo cliente, com reforços relacionados a backup básico, proteção de senhas, prevenção de spam no formulário público, expectativa mínima de desempenho e aviso simples de uso dos dados no formulário público.
