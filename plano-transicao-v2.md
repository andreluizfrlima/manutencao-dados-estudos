Plano de Transição para Dados e IA Aplicada à Manutenção Industrial (4 Meses)
Versão 2.0 — revisada em 26/11/2026 (corrige inconsistências da v1; changelog no final)
Objetivo
Ao final de 4 meses, construir um portfólio sólido que demonstre capacidade de resolver problemas reais de manutenção industrial utilizando dados, automação e inteligência artificial.
Resultados Esperados
    • GitHub ativo e organizado
    • LinkedIn atualizado e alinhado ao novo posicionamento profissional (título inicial aplicado já na Semana 1)
    • 4 projetos relevantes publicados (corrigido: a v1 dizia 3, mas o roadmap entrega 4)
    • Conhecimento intermediário em SQL
    • Conhecimento funcional em Python
    • Capacidade de criar dashboards profissionais em Power BI
    • Construção de um sistema RAG (Retrieval-Augmented Generation)
    • Desenvolvimento de um agente de IA aplicado à manutenção industrial
    • Cada projeto aprovado nos seus critérios de aceite mensuráveis (novo)
    • Preparação para candidaturas em vagas de: Analista de Dados Jr, Analista BI Jr, Analista de Automação Jr, IA Aplicada Jr, Desenvolvedor de Soluções com IA Jr

Premissas
Disponibilidade semanal
Dia
Horas
Segunda a Sexta
3h/dia
Sábado
4h
Domingo
4h
Total semanal: 23 horas · Total em 16 semanas: ~368 horas
Premissas gerais (novo)
    • Todos os dados serão simulados ou anonimizados — nunca dados reais de empresa sem autorização formal.
    • Meses 3 e 4 usam APIs pagas: haverá orçamento limitado e controle de custos (ver seção Segurança e Custos de API).
    • O progresso será registrado semanalmente em log-progresso.md (ver Gestão de Progresso).

Visão Geral do Roadmap
Mês
Foco Principal
Projeto
Mês 1
SQL + Python + Git
Análise de Dados de Manutenção
Mês 2
Power BI + KPIs Industriais
Dashboard de Manutenção
Mês 3
IA Generativa + RAG
Assistente de Procedimentos
Mês 4
Agentes de IA + Automação
Classificador Inteligente de Falhas

MÊS 1 — Fundamentos de Dados
Objetivo: construir a base necessária para trabalhar com dados.
Semanas 1 e 2
SQL Básico: SELECT, WHERE, ORDER BY, GROUP BY, COUNT, SUM, AVG, DISTINCT, LIMIT Ferramentas: PostgreSQL, DBeaver
Exercícios — criar consultas para responder:
    • Quantas ordens de serviço foram abertas?
    • Qual equipamento apresentou mais falhas?
    • Quanto foi gasto por equipamento?
    • Quais são os equipamentos mais críticos?
Python Básico: variáveis, tipos de dados, listas, tuplas, dicionários, condicionais, loops, funções
Exercícios — criar scripts para: ler CSV, filtrar dados, gerar relatórios simples, calcular indicadores básicos.
Git e GitHub: criar conta; criar repositório manutencao-dados-estudos; aprender git init, add, commit, push, branch, merge. (Novo: criar .gitignore desde o primeiro commit — preparar o terreno para nunca versionar chaves de API nos meses 3–4.)
Semanas 3 e 4
SQL Intermediário: INNER JOIN, LEFT JOIN, RIGHT JOIN, CASE WHEN, CTE, Subqueries
Projeto do Mês — Análise de Dados de Manutenção
Modelo de Dados Simulado (corrigido e ampliado)
Tabela Equipamentos
text
ID (PK) | Tag | Descrição | Área | Criticidade
Tabela Ordens de Serviço
text
OS (PK) | Data_Abertura | Data_Fechamento | Equipamento (FK) | Tipo | Status
Tipo: Preventiva, Corretiva
Status: Aberta, Em Execução, Concluída, Cancelada
Tabela Falhas (correção: adicionado vínculo com a OS e data da falha — sem isso, era impossível relacionar falha → equipamento)
text
Falha (PK) | OS (FK) | Data_Falha | Categoria | Descrição | Impacto
Tabela Custos
text
OS (FK, única) | Mão de obra | Peças | Serviços
Tabela Registro de Operação (mensal) (nova — indispensável para MTBF e Disponibilidade)
text
Equipamento (FK) | Mês_Referência | Horas_Operacao
Premissas explícitas do dataset (novo)
    • Período simulado: 12 meses; volume mínimo: ~30 equipamentos, ~300 OS, ~100 falhas.
    • Regime de operação definido por equipamento (ex.: contínuo 24h/dia ou 16h/dia útil), registrado em Registro de Operação.
    • Falha = OS corretiva. Data_Falha = Data_Abertura da OS corretiva (a OS abre no momento da falha).
    • Tempo de reparo = Data_Fechamento − Data_Abertura da OS corretiva concluída.
Fórmulas oficiais (novo — vocabulário de domínio fixado para todos os projetos)
Indicador
Fórmula
MTBF
Σ Horas de operação ÷ Nº de falhas (por equipamento, no período)
MTTR
Σ Tempos de reparo ÷ Nº de OS corretivas concluídas
Disponibilidade
MTBF ÷ (MTBF + MTTR)
Taxa de falhas
Nº de falhas ÷ Σ Horas de operação
Backlog
Nº de OS com status ≠ Concluída/Cancelada (+ carga em horas, se estimada)
Custo total
Mão de obra + Peças + Serviços
Análises obrigatórias
MTBF · MTTR · Backlog · Custos por equipamento · Custos por área · Ranking de falhas
Critérios de aceite do mês (novo)
    • ≥10 queries documentadas cobrindo as 6 análises
    • Conferência manual: resultados de 5 OS escolhidas batem com cálculo feito à mão
    • Script Python executa do zero sem erro e gera relatório
    • README completo nos 8 tópicos do padrão de documentação
Entregável: manutencao-sql-analysis · Tecnologias: SQL, PostgreSQL, Python, GitHub

MÊS 2 — Dashboard Profissional
Objetivo: transformar dados em informação executiva.
Semanas 5 e 6
Power BI: importação, Power Query, modelagem, relacionamentos, Star Schema DAX: SUM, SUMX, CALCULATE, FILTER, DIVIDE, IF, SWITCH
Semanas 7 e 8 — Projeto: Dashboard Inteligente de Manutenção
Indicadores (usar as fórmulas oficiais do Mês 1):
    • Confiabilidade: MTBF, taxa de falhas, disponibilidade
    • Manutenção: MTTR, backlog, ordens abertas, ordens concluídas
    • Custos: totais, por área, por equipamento
    • Estratégia: preventiva × corretiva, tendência mensal, equipamentos críticos
Recursos visuais: KPI Cards, gráficos de tendência, Pareto de falhas, heatmap de criticidade, página executiva.
Critérios de aceite do mês (novo)
    • Números do dashboard = números das queries do Mês 1 (conferir amostra; tolerância zero)
    • Filtros funcionais por área, período e criticidade
    • Demonstração em GIF ou vídeo no README
    • README completo nos 8 tópicos
Entregável: dashboard-manutencao-powerbi · Tecnologias: Power BI, SQL, DAX

MÊS 3 — IA Aplicada à Manutenção
Objetivo: usar modelos de linguagem para resolver problemas industriais.
Semanas 9 e 10
Fundamentos de IA Generativa: APIs, JSON, REST, Prompt Engineering, OpenAI API Python para IA: requests, pandas, json, pathlib, openai (Novo: aprender python-dotenv e gestão de chaves em .env antes da primeira chamada de API.)
Exercícios: resumir textos, classificar falhas, gerar relatórios, consultar documentos.
Semanas 11 e 12 — Projeto: Assistente de Procedimentos de Manutenção
Objetivo: consultar procedimentos técnicos em linguagem natural.
text
Pergunta: "Qual o procedimento de troca de rolamento da bomba P-101?"
Resposta: "Segundo o procedimento XYZ, revisão 03, a troca deve seguir os passos..."
Conceitos: RAG, embeddings, banco vetorial (ChromaDB)
Arquitetura:
text
Documentos PDF → Embeddings → ChromaDB → LLM → Resposta (com citação da fonte)
Critérios de aceite do mês (novo)
    • Bateria de 10 perguntas de teste: ≥8 respostas corretas com documento e revisão citados
    • 2 perguntas fora do escopo dos documentos → assistente recusa responder em vez de inventar
    • Custo total de API registrado no README
    • README completo nos 8 tópicos
Entregável: assistente-procedimentos-rag · Tecnologias: Python, OpenAI API, ChromaDB

MÊS 4 — Agentes de IA e Automação
Objetivo: construir solução autônoma para o processo de manutenção.
Semanas 13 e 14
Automação: Function Calling, n8n, workflows, integração de APIs Conceitos: agentes, ferramentas (tools), orquestração, automação de decisões
Semanas 15 e 16 — Projeto Final: Agente Classificador Inteligente de Falhas
Entrada:
text
Vazamento no selo mecânico da bomba P-101
Saída esperada:
json
{
  "categoria": "Mecânica",
  "criticidade": "Alta",
  "prioridade": 1,
  "justificativa": "Risco de parada operacional",
  "recomendacao": "..."
}
Funcionalidades: categoria, criticidade, priorização automática, justificativa técnica, geração de recomendação.
Dataset de avaliação (novo)
    • 30 descrições de falhas rotuladas por você (especialista) com categoria, criticidade e prioridade — gabarito versionado no repositório (avaliacao/gabarito.csv).
Critérios de aceite do mês (novo — quantitativos)
    • ≥80% de concordância com o especialista em categoria (≥24/30 casos)
    • ≥80% de concordância em criticidade
    • 100% das saídas em JSON válido (validação por schema)
    • Divergências documentadas e analisadas no README (isso é o diferencial do projeto)
    • README completo nos 8 tópicos
Entregável: agente-classificador-falhas · Tecnologias: Python, OpenAI API, n8n, JSON, Prompt Engineering

Estrutura Final do GitHub
text
github.com/seu-usuario
├── manutencao-dados-estudos      (exercícios + log-progresso.md)
├── manutencao-sql-analysis
├── dashboard-manutencao-powerbi
├── assistente-procedimentos-rag
└── agente-classificador-falhas

Padrão de Documentação dos Projetos
Todos os projetos deverão possuir README com:
    1. Problema — desafio de negócio
    2. Contexto — situação industrial simulada ou real
    3. Solução — abordagem adotada
    4. Arquitetura — fluxograma ou diagrama
    5. Tecnologias — ferramentas utilizadas
    6. Demonstração — imagens, GIFs ou vídeos
    7. Resultados — indicadores e benefícios quantificados
    8. Melhorias Futuras — evoluções possíveis

Segurança e Custos de API (seção nova)
    • Chaves de API somente em variáveis de ambiente (.env + python-dotenv); .env no .gitignore desde o primeiro commit.
    • Se uma chave vazar em commit: revogar imediatamente no painel do provedor.
    • Definir limite de gastos no painel do provedor (sugestão: US$ 10–20 no total para os meses 3–4).
    • Usar modelos de menor custo durante o desenvolvimento; reservar modelos maiores para a demonstração final.
    • Cachear embeddings (não reprocessar PDFs a cada execução).
    • Registrar custo por execução nos READMEs dos projetos 3 e 4.
    • Testar lógica com mocks/respostas simuladas antes de gastar tokens reais.

Estratégia para LinkedIn
Título inicial — aplicar na Semana 1 (timing explicitado):
text
Planejador de Manutenção | SQL | Power BI | Python | IA Aplicada à Manutenção Industrial
Título após Projeto 3 — aplicar na Semana 12:
text
Especialista em Manutenção Industrial | Dados e IA Aplicada | SQL | Power BI | Python

Estratégia de Empregabilidade
Semana
Ação
8
Iniciar aplicações: BI Jr, Analista de Dados Jr
12
Expandir: BI Jr, Dados Jr, Automação Jr
16
Expandir: IA Aplicada Jr, Desenvolvedor de Automação, Assistente de IA, Soluções com IA

Meta de Networking
    • GitHub: 1 atualização por semana (desde a Semana 1)
    • LinkedIn: 3 publicações técnicas por mês
    • Mercado: 10 candidaturas por semana — a partir da Semana 8 (alinhado com a Estratégia de Empregabilidade; a v1 não deixava claro o início)

Gestão de Progresso e Riscos (seção nova)
Log de progresso
Manter log-progresso.md no repositório de estudos, atualizado todo domingo:
text
Semana: X/16 | Fase: Mês N | Projeto ativo: ...
Horas estudadas: __/23
Entregas concluídas: ...
Commits da semana: ...
Pendências: ...
Próximo passo: ...
Colar esse log no início de cada sessão com o agente mentor (o agente não tem memória entre conversas — o log é o estado dele).
Regra de priorização em caso de atraso
    • Se atrasar uma semana: concluir o projeto do mês em escopo mínimo antes de avançar — cortar enfeites, nunca cortar o projeto inteiro.
    • Um projeto só é considerado "pronto" quando: README nos 8 tópicos + critérios de aceite do mês aprovados + código publicado.

Resultado Esperado ao Final dos 4 Meses
O profissional deverá ser capaz de: desenvolver consultas SQL para manutenção industrial; automatizar tarefas com Python; construir dashboards executivos em Power BI; criar aplicações com IA Generativa; implementar sistemas RAG; construir agentes de IA orientados ao domínio de manutenção; demonstrar projetos reais no GitHub; posicionar-se como profissional híbrido entre manutenção industrial, dados e IA.
Diferencial Competitivo
A maior vantagem não é o conhecimento técnico isolado, mas a combinação entre: (1) experiência prática em manutenção industrial, (2) conhecimento de indicadores de confiabilidade, (3) SQL aplicado ao contexto industrial, (4) Power BI aplicado à gestão de ativos, (5) Python para automação, (6) IA Generativa aplicada à manutenção, (7) agentes inteligentes focados em operações industriais.
Essa combinação cria um perfil significativamente mais competitivo do que um júnior genérico de dados ou IA, pois está fundamentada em experiência operacional real e conhecimento de domínio.

Anexo — Changelog v1 → v2
#
Correção
1
"3 projetos" → 4 projetos (contradição com o roadmap)
2
Tabela Falhas ganhou FK para OS + Data_Falha (sem isso, falha não se relacionava a equipamento)
3
Nova tabela Registro de Operação + premissas explícitas (MTBF era incalculável com o schema original)
4
Fórmulas oficiais de MTBF, MTTR, Disponibilidade, Backlog, Taxa de falhas
5
Critérios de aceite mensuráveis por projeto (incl. ≥80% de concordância em 30 casos no Projeto 4)
6
Nova seção Segurança e Custos de API
7
Títulos do LinkedIn com timing explícito (Semana 1 / Semana 12)
8
Meta de candidaturas alinhada: início na Semana 8
9
Nova seção Gestão de Progresso e Riscos + log-progresso.md

