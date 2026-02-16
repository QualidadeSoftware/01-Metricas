# 🔬 Atividade Prática: Análise de Métricas de Software com SonarQube Cloud

---

## 📋 Objetivo da Atividade

Utilizar a plataforma **SonarQube Cloud** (antigo SonarCloud) para realizar a **análise estática** de dois projetos open-source que implementam o **Jogo da Velha (Tic-Tac-Toe)** em JavaScript, comparando suas métricas de qualidade e identificando diferenças em termos de manutenibilidade, confiabilidade, segurança e duplicação de código.

---

## 📚 Fundamentação Teórica

### O que é Análise Estática de Código?

A análise estática examina o código-fonte **sem executá-lo**, identificando problemas potenciais como bugs, vulnerabilidades de segurança, *code smells* (indicadores de práticas de programação ruins) e violações de padrões de codificação. Diferente dos testes automatizados, ela avalia a **estrutura** e a **qualidade interna** do código.

### Métricas Principais do SonarQube Cloud

| Métrica | Descrição |
|---|---|
| **Bugs** | Problemas que representam erros reais ou potenciais no código |
| **Vulnerabilidades** | Falhas de segurança que podem ser exploradas |
| **Code Smells** | Trechos de código que dificultam a manutenção |
| **Cobertura** | Percentual de código coberto por testes automatizados |
| **Duplicações** | Percentual de linhas de código duplicadas |
| **Dívida Técnica** | Tempo estimado para corrigir todos os *code smells* |
| **Complexidade Ciclomática** | Quantidade de caminhos independentes no código |

### Classificações (Ratings)

O SonarQube Cloud atribui notas de **A** (melhor) a **E** (pior) para três dimensões:

- **Confiabilidade (Reliability):** baseada na quantidade e severidade dos bugs
- **Segurança (Security):** baseada nas vulnerabilidades encontradas
- **Manutenibilidade (Maintainability):** baseada na dívida técnica em relação ao tamanho do código

---

## 🎯 Repositórios Utilizados

Nesta atividade, vamos analisar dois repositórios públicos que implementam o Jogo da Velha em JavaScript, com abordagens e níveis de complexidade diferentes:

| | Projeto A | Projeto B |
|---|---|---|
| **Repositório** | [WebDevSimplified/JavaScript-Tic-Tac-Toe](https://github.com/WebDevSimplified/JavaScript-Tic-Tac-Toe) | [CodeExplainedRepo/Tic-Tac-Toe-JavaScript](https://github.com/CodeExplainedRepo/Tic-Tac-Toe-JavaScript) |
| **Abordagem** | DOM com CSS Grid e classes | Canvas API com IA (Minimax) |
| **Arquivos principais** | `script.js`, `styles.css`, `index.html` | `app.js`, `style.css`, `index.html` |
| **Complexidade** | Mais simples, interação via DOM | Mais complexo, lógica de IA e renderização via Canvas |

---

## 🛠️ Parte 1 — Criação da Conta no SonarQube Cloud (15 min)

### Passo 1.1 — Acessar o SonarQube Cloud

1. Abra o navegador e acesse: **[https://sonarcloud.io](https://sonarcloud.io)**
2. Clique em **"Log in"** (canto superior direito)
3. Selecione **"Log in with GitHub"**
4. Caso solicitado, autorize o SonarQube Cloud a acessar sua conta GitHub
   - Ele solicitará permissões de leitura sobre seus repositórios
   - Isso é necessário para que a ferramenta possa analisar o código

> 💡 **Dica:** Se preferir maior privacidade, você pode autorizar o acesso apenas a repositórios específicos na tela de permissões do GitHub App.

### Passo 1.2 — Fazer Fork dos Repositórios

Antes de importar os projetos no SonarQube Cloud, é necessário fazer o **fork** (cópia) de cada repositório para sua conta pessoal do GitHub.

**Para cada um dos dois repositórios:**

1. Acesse o link do repositório no GitHub
2. Clique no botão **"Fork"** (canto superior direito)
3. Na tela de criação do fork, mantenha as configurações padrão
4. Clique em **"Create fork"**
5. Aguarde a cópia ser concluída

Ao final, você terá em sua conta:
- `seu-usuario/JavaScript-Tic-Tac-Toe`
- `seu-usuario/Tic-Tac-Toe-JavaScript`

### Passo 1.3 — Criar a Organização no SonarQube Cloud

1. Após o login, clique no **"+"** (canto superior direito) e selecione **"Analyze new project"**
2. Se for seu primeiro acesso, será solicitado importar uma organização do GitHub:
   - Clique em **"Import an organization from GitHub"**
   - Selecione sua conta pessoal do GitHub
   - Escolha conceder acesso aos repositórios que você acabou de criar via fork (ou a todos os repositórios)
   - Clique em **"Install"** / **"Save"**
3. Na tela **"Create an organization"**:
   - Defina um **nome** e uma **chave** para sua organização (pode usar seu nome de usuário)
   - Selecione o plano **Free** (gratuito — para repositórios públicos)
   - Clique em **"Create Organization"**

### Passo 1.4 — Importar os Projetos

1. Na tela **"Analyze projects"**, você verá a lista dos seus repositórios
2. Selecione os dois repositórios do Jogo da Velha que você criou via fork:
   - ☑️ `JavaScript-Tic-Tac-Toe`
   - ☑️ `Tic-Tac-Toe-JavaScript`
3. Clique em **"Set Up"**
4. Na tela **"Set up project for Clean as You Code"**, selecione **"Previous version"** como definição de código novo
5. Clique em **"Create Project"**

> ⏳ **Aguarde:** O SonarQube Cloud iniciará automaticamente a análise dos projetos. Para repositórios JavaScript hospedados no GitHub, a **Análise Automática** (Automatic Analysis) é utilizada — não é necessário configurar CI/CD.

---

## 🔍 Parte 2 — Análise das Medidas (Measures) (25 min)

Após a conclusão da análise, concentre a coleta e interpretação de dados na aba **Measures** de cada projeto. A atividade desta parte é tratar as *medidas* como evidências quantitativas para discutir qualidade (confiabilidade, segurança, manutenibilidade, duplicação e complexidade).

### Passo 2.1 — Aba Measures (Medidas) — Foco em Conceitos de Métricas de Software

1. Para **cada projeto (A e B)**, acesse o projeto no SonarQube Cloud e clique na aba **"Measures"**.
2. (Contexto rápido) Registre o status do **Quality Gate** exibido no topo do projeto (se disponível na sua visualização).
3. Selecione **pelo menos 6 medidas** distribuídas entre as categorias abaixo (mínimo de 1 por categoria, se disponível):
   - **Confiabilidade (Reliability)**: Bugs, Reliability Rating, esforço de remediação
   - **Segurança (Security)**: Vulnerabilities, Security Hotspots, Security Rating
   - **Manutenibilidade (Maintainability)**: Code Smells, Dívida Técnica, Maintainability Rating
   - **Duplicações (Duplications)**: Duplicated Lines (%), blocos/arquivos com duplicação
   - **Tamanho e Complexidade**: Lines of Code, Complexidade ciclomática, Complexidade cognitiva

4. Para **cada medida selecionada**, preencha o registro abaixo (no seu documento de entrega):

**Registro de Medida (modelo obrigatório):**
- **Nome no SonarQube Cloud:** (ex.: “Code Smells”, “Cognitive Complexity”, “Duplicated Lines (%)”)
- **O que é medido (definição operacional):** descreva *o que exatamente* o número representa
- **Unidade / escala:** (contagem, porcentagem, tempo estimado, rating A–E etc.)
- **Tipo (medida × métrica):**
  - Indique se é uma **medida direta** (ex.: contagem de bugs) ou uma **métrica derivada/composta** (ex.: rating A–E, dívida técnica agregada)
- **Interpretação:** o que significa **aumentar/diminuir** esse valor? Isso é sempre “melhor/pior”?
- **Atributo de qualidade relacionado:** associe a medida a pelo menos **um atributo** (ex.: manutenibilidade, confiabilidade, segurança)
- **Limitações:** cite **1 limitação** (ex.: falso positivo, depende de regras, não mede comportamento em execução)

5. **Comparação orientada por métricas (obrigatório):**
   - Escolha **3 medidas** (ex.: Duplications %, Complexidade Cognitiva, Bugs).
   - Compare A vs. B e explique: **o que a diferença sugere** sobre o produto e **qual decisão** você tomaria (ex.: “qual projeto está mais arriscado para manutenção?”) com base **nos números**.


> ✅ **Dica didática:** trate “Measures” como o conjunto de **dados quantitativos** usados para justificar conclusões sobre qualidade. Evite afirmações vagas (“é melhor”) sem conectar a uma medida específica.

---

## 📊 Parte 3 — Comparação e Análise Crítica (20 min)

### Passo 3.1 — Preencher a Tabela Comparativa

Com base nas métricas coletadas em **Measures**, preencha a tabela abaixo:

| Métrica | Projeto A | Projeto B |
|---|---|---|
| Linhas de Código | | |
| Bugs (quantidade) | | |
| Rating de Confiabilidade (A-E) | | |
| Vulnerabilidades | | |
| Rating de Segurança (A-E) | | |
| Code Smells (quantidade) | | |
| Rating de Manutenibilidade (A-E) | | |
| Dívida Técnica (tempo estimado) | | |
| Duplicações (%) | | |
| Complexidade Ciclomática | | |
| Complexidade Cognitiva | | |

### Passo 3.2 — Responder às Questões de Análise

Responda às seguintes questões **exclusivamente com base nas informações disponíveis na aba _Measures_** . Entregue suas respostas em um documento de texto na atribuicão da tarefa no _TEAMS_.

**Questão 1 — Comparação Quantitativa (baseada em Measures)**
> Considerando pelo menos **3 medidas** (ex.: *Bugs*, *Technical Debt*, *Duplicated Lines (%)*, *Cognitive Complexity*, *Security Hotspots*), qual projeto apresenta melhor qualidade **para manutenção futura**? Justifique conectando **valores → interpretação → decisão**.

**Questão 2 — Medida vs. Métrica Derivada**
> Escolha **2 itens** do _Measures_: um que você considere **medida direta** (contagem/percentual/linhas/tempo) e outro que seja **métrica derivada/composta** (ex.: *ratings A–E*). Explique:
> (a) por que cada um se encaixa nessa categoria e  
> (b) que cuidado você teria ao comparar projetos usando esse item.

**Questão 3 — Complexidade e Risco**
> Compare **Complexidade Ciclomática** e **Complexidade Cognitiva** entre os projetos. O que cada uma sugere sobre:
> (a) esforço de entendimento do código e  
> (b) probabilidade de defeitos ao modificar funcionalidades?

**Questão 4 — Duplicação e Impacto na Manutenibilidade**
> Analise *Duplicated Lines (%)* e ao menos uma medida de tamanho (ex.: *Lines of Code*). A duplicação observada é “alta” ou “baixa” **no contexto do tamanho do projeto**? Que impacto isso pode gerar em correções e evolução?

**Questão 5 — Quality Gate e Limiar (Threshold)**
> Verifique se cada projeto **Passou/Falhou** no **Quality Gate**. Proponha um **mini–Quality Gate** (3 condições) para estes projetos (ex.: limite de bugs, limite de duplicação, limite de complexidade/ dívida técnica) e justifique por que esses **limiares** são úteis para padronizar qualidade e evitar regressões.

**Questão 6 — Limitações das Medidas**
> Aponte **2 limitações** de avaliar qualidade apenas por _Measures_ (ex.: dependência de regras, falsos positivos/negativos, ausência de comportamento em execução). Em seguida, cite **2 práticas complementares** (ex.: testes, revisão de código, análise dinâmica) que ajudariam a reduzir o risco de conclusões equivocadas.

---

## 📦 Entregáveis

Ao final da atividade, cada aluno (ou dupla) deve entregar:

1. **Tabela comparativa** preenchida (Passo 3.1)
2. **Respostas** às 6 questões de análise (Passo 3.2)
3. **Registros de Medidas (Passo 2.1)** preenchidos (modelo obrigatório) para **cada projeto**
4. **Capturas de tela** (screenshots) evidenciando as informações usadas na análise, contendo:
   - A aba **Measures** de cada projeto (com as medidas selecionadas visíveis)
   
---

## ⚠️ Solução de Problemas Comuns

| Problema | Solução |
|---|---|
| A análise não iniciou automaticamente | Acesse *Administration > Analysis Method* no projeto e verifique se "Automatic Analysis" está habilitada |
| Não consigo ver meus repositórios | Verifique se o fork está como **público** no GitHub e se o SonarQube Cloud tem permissão de acesso |
| A análise mostra 0 linhas de código | Aguarde alguns minutos; a primeira análise pode demorar. Tente recarregar a página |
| Erro ao criar organização | Certifique-se de que a chave da organização é única e contém apenas letras minúsculas, números e hifens |
| Métricas de cobertura em 0% | Isso é esperado — a cobertura requer configuração de testes com CI/CD, o que está fora do escopo desta atividade |

---

## 📖 Referências e Leitura Complementar

- **Documentação oficial do SonarQube Cloud:** [https://docs.sonarcloud.io](https://docs.sonarcloud.io)
- **Guia de primeiros passos (GitHub):** [https://docs.sonarcloud.io/getting-started/github](https://docs.sonarcloud.io/getting-started/github)
- **Definições de métricas:** [https://docs.sonarcloud.io/digging-deeper/metric-definitions](https://docs.sonarcloud.io/digging-deeper/metric-definitions)
- **Análise Automática:** [https://docs.sonarcloud.io/advanced-setup/automatic-analysis](https://docs.sonarcloud.io/advanced-setup/automatic-analysis)
- **ISO/IEC 25010** — Modelo de qualidade de produto de software
- PRESSMAN, R. S. *Engenharia de Software: Uma Abordagem Profissional*. 9ª ed. McGraw-Hill, 2021.

---

