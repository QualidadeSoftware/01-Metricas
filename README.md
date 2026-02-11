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

> ⏳ **Aguarde:** O SonarQube Cloud iniciará automaticamente a análise dos projetos. Para repositórios JavaScript hospedados no GitHub, a **Análise Automática** (Automatic Analysis) é utilizada — não é necessário configurar CI/CD. A primeira análise pode levar de 1 a 3 minutos por projeto.

---

## 🔍 Parte 2 — Explorando as Métricas (20 min)

Após a conclusão da análise, explore as métricas de cada projeto seguindo o roteiro abaixo.

### Passo 2.1 — Visão Geral do Projeto (Overview)

1. No menu lateral, clique em **"My Projects"**
2. Selecione o primeiro projeto (Projeto A: `JavaScript-Tic-Tac-Toe`)
3. Na página de **Overview**, observe e anote:

| Item | O que observar |
|---|---|
| **Quality Gate** | O projeto passou (Passed) ou falhou (Failed)? |
| **Bugs** | Quantos bugs foram encontrados? Qual a classificação (A-E)? |
| **Vulnerabilidades** | Existem vulnerabilidades de segurança? |
| **Code Smells** | Quantos *code smells* foram identificados? |
| **Duplicações** | Qual o percentual de código duplicado? |
| **Dívida Técnica** | Quanto tempo seria necessário para resolver os *code smells*? |

4. Repita o processo para o segundo projeto (Projeto B: `Tic-Tac-Toe-JavaScript`)

### Passo 2.2 — Análise Detalhada de Issues

1. Dentro de cada projeto, clique na aba **"Issues"**
2. Explore os filtros disponíveis no painel lateral esquerdo:
   - **Type:** Bug, Vulnerability, Code Smell
   - **Severity:** Blocker, Critical, Major, Minor, Info
   - **Status:** Open, Confirmed, Resolved, Closed
3. Clique em pelo menos **2 issues** de cada projeto e observe:
   - A **descrição** do problema
   - A **explicação** de por que aquilo é considerado um problema
   - A **sugestão de correção** oferecida pelo SonarQube
   - O **trecho de código** onde o problema foi detectado

> 📝 **Anote:** Para cada issue analisada, registre o tipo, a severidade e se você concorda com a recomendação da ferramenta.

### Passo 2.3 — Aba Measures (Medidas)

1. Clique na aba **"Measures"** no menu do projeto
2. Explore as seguintes categorias:

**Confiabilidade (Reliability):**
- Quantidade de bugs
- Rating de confiabilidade
- Esforço de remediação

**Manutenibilidade (Maintainability):**
- Quantidade de *code smells*
- Dívida técnica (em minutos/horas)
- Rating de manutenibilidade

**Segurança (Security):**
- Vulnerabilidades
- Security Hotspots (pontos que exigem revisão manual)

**Duplicações:**
- Percentual de linhas duplicadas
- Blocos duplicados
- Arquivos com duplicação

**Tamanho e Complexidade:**
- Linhas de código (Lines of Code)
- Complexidade ciclomática
- Complexidade cognitiva

### Passo 2.4 — Explorar o Código (Code Tab)

1. Clique na aba **"Code"**
2. Navegue pela estrutura de arquivos do projeto
3. Observe as métricas exibidas ao lado de cada arquivo:
   - Quantidade de issues
   - Linhas de código
   - Percentual de duplicação
4. Clique em um arquivo `.js` para ver os problemas marcados diretamente no código-fonte

---

## 📊 Parte 3 — Comparação e Análise Crítica (20 min)

### Passo 3.1 — Preencher a Tabela Comparativa

Com base nas métricas coletadas, preencha a tabela abaixo:

| Métrica | Projeto A | Projeto B |
|---|---|---|
| Quality Gate (Passed/Failed) | | |
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

Responda às seguintes questões com base nos dados coletados. Entregue suas respostas em um documento de texto ou diretamente no ambiente de aprendizagem da disciplina.

**Questão 1 — Comparação Quantitativa**
> Qual dos dois projetos apresentou melhores métricas gerais de qualidade? Justifique sua resposta comparando pelo menos três métricas diferentes.

**Questão 2 — Code Smells**
> Selecione um *code smell* encontrado em um dos projetos. Descreva: (a) qual é o problema apontado, (b) por que ele é considerado um *code smell*, e (c) como você corrigiria o código.

**Questão 3 — Complexidade**
> Compare a complexidade ciclomática dos dois projetos. É esperado que um deles seja mais complexo que o outro? Por quê? A complexidade adicional é justificável?

**Questão 4 — Duplicação de Código**
> Algum dos projetos apresentou duplicação de código? Se sim, qual seria o impacto dessa duplicação na manutenibilidade a longo prazo?

**Questão 5 — Limitações da Análise Estática**
> A análise estática é suficiente para avaliar completamente a qualidade de um software? Quais aspectos da qualidade **não** são cobertos por ferramentas como o SonarQube? Cite pelo menos dois exemplos.

**Questão 6 — Quality Gate**
> Explique o conceito de Quality Gate. Ambos os projetos passaram? Se algum falhou, quais condições não foram atendidas?

### Passo 3.3 — Reflexão Final

Escreva um parágrafo (5 a 10 linhas) refletindo sobre:
- A importância da análise estática no ciclo de desenvolvimento de software
- Como ferramentas como o SonarQube Cloud podem ser integradas a um fluxo de trabalho com CI/CD
- Em que momento do desenvolvimento a análise estática deveria ser aplicada e por quê

---

## 📦 Entregáveis

Ao final da atividade, cada aluno (ou dupla) deve entregar:

1. **Tabela comparativa** preenchida (Passo 3.1)
2. **Respostas** às 6 questões de análise (Passo 3.2)
3. **Reflexão final** (Passo 3.3)
4. **Capturas de tela** (screenshots) do dashboard de cada projeto no SonarQube Cloud, mostrando:
   - A visão geral (Overview)
   - A aba de Issues com pelo menos um issue expandido
   - A aba de Measures

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

## ✅ Critérios de Avaliação

| Critério | Peso |
|---|---|
| Tabela comparativa corretamente preenchida | 20% |
| Qualidade e profundidade das respostas às questões | 40% |
| Reflexão final demonstrando compreensão do tema | 20% |
| Capturas de tela adequadas | 10% |
| Organização e clareza do documento entregue | 10% |

---

> **Bom trabalho!** 🚀 Ao concluir esta atividade, você terá experiência prática com uma das ferramentas de análise estática mais utilizadas no mercado e compreenderá como métricas de qualidade podem guiar decisões de engenharia de software.
