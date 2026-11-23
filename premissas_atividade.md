# Premissas Básicas e Guia da Atividade: Sistema de Apoio à Decisão (BI)

Este documento consolida todas as premissas, requisitos técnicos, entregáveis e critérios de avaliação da atividade prática de desenvolvimento de um painel de Business Intelligence (BI) integrado a uma planilha de dados.

---

## 1. Escolha do Problema

O projeto deve partir de uma **situação real** (do seu trabalho, estágio, negócio próprio ou de uma organização que você conheça), sendo específico e compatível com um sistema simples.

* **Exemplos de temas:** Divergências de estoque, desperdícios, retrabalho, reclamações de clientes, queda de vendas, falhas de equipamentos ou dificuldade de planejamento.

### Definições Obrigatórias:
* [ ] **Problema e Consequências:** Qual é exatamente o problema enfrentado e quais impactos negativos ele gera para a organização?
* [ ] **Pergunta Analítica:** Qual pergunta central o sistema deverá ajudar a responder?
* [ ] **Decisão e Tomador de Decisão:** Qual decisão prática será apoiada pelo painel e quem (cargo/papel) tomaria essa decisão?

---

## 2. Planejamento do Sistema

O planejamento estrutura a lógica de negócio e a arquitetura de dados antes da construção do protótipo.

### 2.1. Estrutura e Qualidade de Dados
* **Dados e Origem:** Quais dados serão necessários e de onde viriam na prática?
* **Granularidade:** O que cada linha (registro) da planilha representará?
* **Organização e Atualização:** Como os dados serão preparados e atualizados?
* **Regras de Qualidade (Mínimo 2):** Definir pelo menos duas regras práticas (ex.: evitar duplicidades por ID único, padronizar datas no formato `AAAA-MM-DD`, validação de categorias, tratamento de campos vazios).

### 2.2. Indicadores e KPI
Devem ser definidos **dois indicadores** contendo os seguintes atributos:

| Atributo | Indicador 1 | Indicador 2 |
| :--- | :--- | :--- |
| **Nome do Indicador** | *Definir* | *Definir* |
| **Fórmula de Cálculo** | *Definir* | *Definir* |
| **Unidade de Medida** | *Ex.: %, R$, horas, un.* | *Ex.: %, R$, horas, un.* |
| **Frequência de Atualização** | *Ex.: Diária, Semanal, Tempo real* | *Ex.: Diária, Semanal, Tempo real* |
| **Meta ou Parâmetro** | *Valor alvo de comparação* | *Valor alvo de comparação* |
| **É o KPI principal?** | *Justificar qual dos dois é o KPI estratégico do problema e por quê.* |

### 2.3. Análise, Decisão e Limitações
* **Tipo de Análise:** Especificar se a análise será **descritiva, diagnóstica, preditiva ou prescritiva** e explicar como ela ajudará a responder à pergunta analítica.
* **Tomada de Decisão:** Descrever um resultado possível no painel, a ação concreta que ele apoiaria e como acompanhar futuramente se houve melhoria após a ação.
* **Limitação Analítica:** Apontar um cuidado necessário na leitura dos dados para evitar interpretações equivocadas (ex.: sazonalidade, tamanho da amostra, variáveis externas não mapeadas).

### 2.4. Fluxo de Dados e Conceitos (BI, Big Data e Ciência de Dados)
* **Representação do Fluxo:** Descrever como ocorre cada etapa no seu projeto:
  $$\text{Fontes} \rightarrow \text{Extração} \rightarrow \text{Preparação} \rightarrow \text{Planilha} \rightarrow \text{Painel} \rightarrow \text{Decisão}$$
* **Enquadramento Conceitual:**
  * Explicar brevemente como a proposta utiliza **Business Intelligence (BI)**.
  * Avaliar e justificar se haveria necessidade (ou não) de aplicar **Big Data** ou **Ciência de Dados** neste cenário *(não é obrigatório utilizar os três conceitos)*.
  * **Fontes Externas (se aplicável):** Caso a decisão envolva mercado ou concorrência, indicar uma fonte externa de dados e como sua confiabilidade seria avaliada.

---

## 3. Desenvolvimento do Sistema (Requisitos Técnicos)

O protótipo funcional deve atender obrigatoriamente aos seguintes critérios técnicos:

* [ ] **Base de Dados (Planilha):** Mínimo de **50 registros** coerentes com o problema escolhido.
  * *Nota sobre privacidade e autenticidade:* Podem ser usados dados reais anonimizados ou simulados. É obrigatório identificar claramente o que é **fato real**, o que é **dado simulado** e o que é **suposição**. Não incluir dados pessoais (LGPD) ou confidenciais.
  * *Edição:* Os dados serão inseridos e editados diretamente na planilha (não é necessário criar formulário de cadastro no HTML).
* [ ] **Front-end Conectado:** Página em **HTML com JavaScript** conectada diretamente à planilha.
  * *Restrição crítica:* A planilha deve ser a fonte efetiva do painel. **Não são aceitos** indicadores fixos no código (*hardcoded*) nem soluções que exijam importar manualmente o arquivo a cada alteração.
* [ ] **Cálculo Dinâmico de Indicadores:** Pelo menos **2 indicadores** calculados via código diretamente a partir dos registros lidos da planilha.
* [ ] **Visualizações:** Pelo menos **1 gráfico** dinâmico e **1 visualização dos registros** (tabela de dados).
* [ ] **Interatividade (Filtro):** Pelo menos **1 filtro relevante** (ex.: período, produto, setor, categoria, status) que recalcule indicadores, gráfico e tabela ao ser acionado.
* [ ] **Sinalização de Desempenho:** Destaque visual (ex.: cores tipo semáforo, badges ou alertas) comparando o resultado atual com a **meta ou parâmetro** definido.
* [ ] **Atualização Automática (*Polling* / *Auto-refresh*):** O painel deve refletir alterações feitas na planilha automaticamente em **até 60 segundos**, sem necessidade de reimportar arquivos.
* [ ] **Timestamp de Sincronização:** Exibir na tela a **data e o horário da última leitura bem-sucedida** dos dados.

---

## 4. Testes, Validação e Uso de IA

Antes da entrega final, o sistema deve passar por uma bateria de validação e documentação:

### Checklist de Testes
* [ ] **Auditoria dos Indicadores:** Conferir os resultados exibidos no painel por meio de um cálculo independente (ex.: fórmula direta ou tabela dinâmica na própria planilha).
* [ ] **Teste de Filtro:** Verificar se a aplicação do filtro altera corretamente tanto os indicadores quanto o gráfico e a listagem de registros.
* [ ] **Teste de Tempo Real:** Alterar um valor na planilha e confirmar se a mudança aparece automaticamente no painel dentro de 60 segundos.
* [ ] **Verificação de Qualidade:** Confirmar se as duas regras de qualidade de dados definidas no planejamento foram devidamente aplicadas na base.

### Registro do Uso de IA e Depuração
* **Registro de Erro/Inadequação:** Documentar brevemente um erro técnico ou inadequação identificado durante o desenvolvimento e explicar como foi corrigido.
* **Rastreabilidade de IA:** Registrar qual ferramenta de IA foi utilizada, qual foi o **pedido inicial (*prompt*)** e detalhar **uma correção** feita sobre o código ou texto gerado pela IA.
* **Domínio da Solução:** O aluno deve compreender e saber explicar integralmente a organização dos dados, as fórmulas de cálculo e a utilidade prática do sistema para o negócio.

---

## 5. Checklist de Entregas

Todos os itens abaixo devem compor o pacote de entrega da atividade:

1. [ ] **Documento de Descrição do Problema e Planejamento do Sistema** (contemplando todos os itens das seções 1, 2 e 4).
2. [ ] **Planilha Base de Dados** (com no mínimo 50 registros e permissões de leitura configuradas caso utilize Google Sheets/OneDrive).
3. [ ] **Código-Fonte** (Arquivo `.html`, scripts `.js`, folhas de estilo `.css` e demais arquivos necessários).
4. [ ] **Instruções Breves de Acesso e Execução** (passo a passo rápido de como abrir e testar a integração).
5. [ ] **Registro do Uso de IA** (ferramenta utilizada, prompt inicial e registro de um erro/correção realizada).

> **Atenção para o dia da apresentação:** Confira previamente as permissões de acesso da planilha (ex.: link público de leitura/CSV publicado no Google Sheets) e o funcionamento da conexão de rede no computador que será utilizado em sala.

---

## 6. Roteiro para Apresentação Individual (Até 5 Minutos)

Sugestão de divisão de tempo para cobrir todos os pontos exigidos na apresentação em sala:

1. **Contextualização (1 min):** Explicar o problema real, suas consequências, a pergunta analítica e a decisão que será apoiada.
2. **Dados e Indicadores (1 min):** Apresentar a estrutura da planilha, as regras de qualidade aplicadas e os dois indicadores (destacando o KPI e a meta).
3. **Demonstração do Painel e Filtros (1 min):** Mostrar o painel funcionando, o gráfico, a tabela, a sinalização de meta e aplicar o filtro ao vivo.
4. **Teste de Atualização Automática (1 min):** Alterar um dado diretamente na planilha e demonstrar o painel atualizando automaticamente (com o horário da última leitura).
5. **Conclusão Analítica (1 min):** Interpretar um resultado exibido, propor uma ação prática baseada nele e apontar uma limitação da análise.

---

## 7. Matriz de Critérios de Avaliação (Total: 10,0 Pontos)

| Critério Avaliado | Pontuação | O que será observado na avaliação |
| :--- | :---: | :--- |
| **1. Autenticidade do caso analisado** | **1,0 pt** | Vínculo com situação real, conhecimento do contexto e distinção clara entre fatos, suposições e dados simulados. |
| **2. Definição do problema e coerência** | **1,0 pt** | Clareza na definição do problema, pergunta analítica bem formulada e aderência da proposta a um sistema simples. |
| **3. Organização, preparação e qualidade dos dados** | **1,5 pt** | Estrutura lógica da planilha (mín. 50 linhas), granularidade correta e aplicação prática das regras de qualidade. |
| **4. Indicadores, análise e interpretação** | **2,0 pts** | Fórmulas corretas, definição de meta/KPI, classificação adequada do tipo de análise e capacidade de interpretação. |
| **5. Capacidade de apoiar a tomada de decisão** | **1,5 pt** | Geração de informações úteis para orientar ações concretas, identificar prioridades, comparar resultados ou avaliar alternativas. |
| **6. Funcionamento do sistema e integração** | **1,0 pt** | Conexão real entre HTML/JS e planilha, funcionamento dos filtros, sinalização de meta e atualização automática em até 60s. |
| **7. Clareza da apresentação e domínio** | **2,0 pts** | Cumprimento do tempo (até 5 min), segurança ao explicar os cálculos, organização dos dados e resposta sobre o uso de IA. |
| **TOTAL** | **10,0 pts** | |
