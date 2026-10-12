# 📄 ATS Resume Optimizer & Matcher

> **Aplicação Web em SPA (Single Page Application)** desenvolvida para comparar currículos com descrições de vagas de emprego, avaliar o grau de compatibilidade e gerar uma versão reestruturada, limpa e otimizada para sistemas ATS (Applicant Tracking System) — sem nunca inventar experiências falsas.

---

## 🎯 Qual problema a aplicação resolve?

Grande parte das empresas utiliza sistemas **ATS (Applicant Tracking System)** para realizar a triagem inicial de candidaturas. Esses robôs analisam o texto dos currículos e os ranqueiam antes mesmo que um profissional de RH leia qualquer documento. 

Muitos candidatos qualificados são descartados nessa fase inicial por motivos simples:
- **Ausência de palavras-chave exatas** mencionadas na descrição da vaga;
- **Formatação incompatível** com leitores automáticos (tabelas, colunas duplas, gráficos, ícones ou PDFs mal estruturados);
- **Estruturação inadequada** de experiências e competências.

**A solução:** Esta aplicação analisa o cruzamento de dados entre o currículo do usuário e a vaga desejada, identifica lacunas de termos essenciais e reorganiza o currículo em um formato 100% compatível com ATS, garantindo que o candidato apresente seu histórico real da melhor forma possível.

---

## 🧠 O Mega Prompt e sua Evolução

### Mega Prompt Utilizado

```markdown
# ESPECIFICAÇÃO DE APLICAÇÃO: ATS RESUME OPTIMIZER & MATCHER

## 1. VISÃO GERAL DO PRODUTO
Crie uma aplicação web moderna de página única (SPA) responsiva para otimização de currículos com foco em sistemas ATS (Applicant Tracking System).
A aplicação permite ao usuário colar a descrição de uma vaga de emprego e o seu currículo atual, exibindo uma análise de compatibilidade (Match Rate), palavras-chave encontradas/faltantes e gerando uma versão do currículo reestruturada, formatada e pronta para exportação.

## 2. REGRA DE OURO (TRANSPARÊNCIA E ÉTICA)
- A aplicação MELHORA A APRESENTAÇÃO das experiências existentes, adaptando termos e organizando tópicos para alinhar com a descrição da vaga.
- É EXPRESSAMENTE PROIBIDO inventar, fabricar ou presumir experiências, cargos, conquistas, métricas, empresas, datas ou competências que o usuário não declarou no currículo original.
- Destaque em local visível na interface a mensagem permanente:
  > "Otimizamos a linguagem e a estrutura do seu currículo. Nenhuma experiência falsa ou não fornecida é criada."

## 3. DESIGN SYSTEM E ESTÉTICA DE INTERFACE
- Framework & Componentes: React + Tailwind CSS + componentes shadcn/ui (Card, Button, Badge, Progress, Textarea, Tabs, Alert, Tooltip, Dialog).
- Ícones: lucide-react.
- Paleta de Cores: Dark Mode padrão em zinc-950/zinc-900, com destaques em emerald-600 para sucessos/matches e amber-500/rose-500 para lacunas de palavras-chave.

## 4. ESTRUTURA DA TELA E FLUXO DO USUÁRIO
- Header: Título, subtítulo, banner explicativo da Regra de Ouro e botão "Preencher com Exemplo".
- Seção de Entrada: Grid de 2 colunas com Textareas para "Descrição da Vaga" e "Seu Currículo Atual", acompanhados de um botão central "Analisar e Otimizar para ATS".
- Dashboard de Resultado:
  1. Card de Match Score com porcentagem e barra de progresso.
  2. Card de Análise de Keywords (Badges verdes para encontradas, amarelas/vermelhas para ausentes).
  3. Card de Dicas e Boas Práticas ATS.
- Seção de Saída: Interface em abas (Tabs) alternando entre "Visualização Formatada (Layout ATS Limpo)" e "Texto Puro", com botões para Copiar Texto e Exportar PDF.
```

### O que mudou até a versão final?
Durante a construção no Lovable, o prompt original foi aprimorado para atender detalhes de usabilidade e funcionalidade técnica:
1. **Inclusão da simulação local (Mock Engine):** Adicionou-se uma lógica de análise via cliente para que a aplicação funcionasse instantaneamente sem depender obrigatoriamente de uma chave de API externa.
2. **Refinamento do visualizador ATS:** A aba de preview foi ajustada para exibir uma folha simulada estilo A4 (fundo claro com tipografia escura em coluna única), garantindo que o usuário visualize exatamente como o robô do ATS enxergará o documento.
3. **Mapeamento explícito de exportação:** Incluiu-se a especificação da biblioteca de geração de PDF no client-side para evitar perda de formatação durante a conversão.

---

## ⚙️ Como funciona a análise (Da vaga ao currículo ajustado)

```
[ Entrada: Vaga + Currículo ] 
          │
          ▼
[ Processamento de Linguagem ] ──► Extração de palavras-chave e requisitos
          │
          ▼
[ Cálculo de Match Rate ]    ──► Comparação direta e geração de pontuação (%)
          │
          ▼
[ Mapeamento de Keywords ]   ──► Classificação em Encontradas vs. Ausentes
          │
          ▼
[ Reestruturação ATS ]       ──► Organização do texto original em layout limpo
          │                      (Sem invenções • Foco em impacto e relevância)
          ▼
[ Painel de Resultados & PDF ]
```

1. **Entrada de Dados:** O usuário cola o texto da descrição da vaga e do seu currículo atual nos campos correspondentes (ou utiliza o botão *Preencher com Exemplo* para testes).
2. **Processamento e Extração de Termos:** O sistema lê os requisitos da vaga e extrai substantivos técnicos, competências, ferramentas e qualificações essenciais.
3. **Cruzamento de Dados & Match Score:** O currículo original é varrido em busca dos termos extraídos. A aplicação calcula o percentual de correspondência com base no volume de termos-chave encontrados.
4. **Mapeamento Visual de Lacunas:** A aplicação exibe badges interativas categorizando quais termos o candidato já possui e quais palavras-chave faltam no texto original.
5. **Reestruturação e Otimização ATS:** O texto do currículo original é reorganizado em uma estrutura de coluna única, padronizando cabeçalhos (*Resumo, Experiência, Competências, Formação*), aplicando verbos de ação e destacando os termos relevantes existentes.
6. **Exportação:** O usuário visualiza o resultado formatado em folha A4 e pode exportar o documento em PDF ou copiar o texto estruturado.

---

## 🛠️ Ajustes solicitados após a primeira geração (Refinamentos)

Após a geração inicial no Lovable, foram solicitadas as seguintes alterações direcionadas para aprimorar o produto:

1. **Geração de PDF integrada:**
   - **Por quê:** A primeira versão apenas exibia o texto na tela sem opção de download formatado. Foi solicitada a integração da exportação em PDF via código para permitir o download direto de um arquivo limpo e pronto para envio.
2. **Formatação visual do Preview ATS (Estilo Folha A4):**
   - **Por quê:** O preview inicial herdava o tema Dark Mode da aplicação. Pediu-se a alteração do container de preview para um visual de "Folha A4" (fundo branco, texto escuro, coluna única e sem elementos gráficos), pois essa é a representação fiel de um currículo ATS.
3. **Reforço proeminente do Banner Ético:**
   - **Por quê:** Para evitar qualquer ambiguidade sobre a integridade da aplicação, foi solicitado o destaque permanente do aviso informando que a ferramenta melhora a escrita, mas nunca cria experiências falsas.

---

## 🌐 Endereço da Aplicação Publicada

Acesse a aplicação rodando ao vivo:

(https://pixel-perfect-buddy-455.lovable.app)
