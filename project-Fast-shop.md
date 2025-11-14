# Projeto Fast Shop - Assessment de Migração AWS para Azure

## Contexto do Projeto

O projeto consistiu na avaliação técnica de 38 repositórios da Fast Shop, visando mapear a migração de workloads da AWS para o Azure. Cada repositório foi analisado individualmente e organizado por stacks tecnológicas.

## Entregáveis

Para a conclusão de cada tarefa de assessment, foram produzidos os seguintes artefatos:

1. **Assessment completo do repositório** (formato Markdown)
2. **HTML de detalhes** - versão navegável do assessment com melhor visibilidade
3. **Resumo executivo** (formato Markdown)
4. **Resumo executivo em HTML**

---

## Metodologia - Fases do Processo

### Fase 0: Configuração do Agente

Foi utilizado o **agente Master** do GitHub Copilot, que fornece acesso às funcionalidades gerais dos agentes. O agente foi configurado para atuar como um **arquiteto de soluções**, garantindo análises técnicas de alto nível.

---

### Fase 1: Análise do Repositório

Nesta fase inicial, cada repositório passou por uma análise minuciosa para identificação das stacks tecnológicas utilizadas.

**Atividades realizadas:**
- Busca manual de arquivos de dependências
- Identificação de gerenciadores de pacotes
- Verificação das versões de cada tecnologia empregada
- Confirmação das stacks em uso

**Objetivo:** Garantir total compreendimento do ambiente tecnológico antes de prosseguir com o assessment.

---

### Fase 2: Geração do Assessment em Markdown

Esta fase focou na criação do documento base de assessment em formato Markdown para cada repositório.

**Prompt utilizado:**

```
Solicita-se que este trabalho seja conduzido por um especialista em arquitetura de soluções, responsável por realizar uma avaliação técnica detalhada de um parque de aplicações construídas em diversas tecnologias, com o objetivo de viabilizar a migração da infraestrutura atual da AWS para a Azure. Essa análise deve contemplar o levantamento completo de dependências e integrações entre os sistemas, identificando vínculos com serviços proprietários da AWS que possam representar lock-in tecnológico e impactar a portabilidade para a nova plataforma. Também é necessário identificar o uso de recursos depreciados que, atualmente, inviabilizam a adoção de soluções PaaS na Azure, resultando na hospedagem de aplicações legadas em máquinas virtuais, com base no template anexo, contendo o conjunto mínimo de informações essenciais para registrar, de forma padronizada, os aspectos técnicos de cada aplicação, suas dependências, integrações, restrições e recomendações para migração, conforme os requisitos descritos neste prompt.
Desconsiderar na avaliação quaisquer informações sobre custos, estimativas e alocações de profissionais, não está no escopo pretendido
Também é requerido a criação de uma pasta onde ficarão os outputs com o nome 'assessment', o material de anexo inclue o template do documento, na existência de diagrama utilize da linguagem mermaid, para uma boa apresentação para o stakeholders e o que for preciso com base nas boas práticas.
Esta anexado a unica pasta que deve ser feita as avaliação, não considerar as demais pastas do workspace
```

**Contexto fornecido:**
- Pasta do projeto a ser avaliado
- Template do assessment com os tópicos necessários

**Revisão:**
Após a geração do documento, era realizada uma revisão para garantir a conformidade do conteúdo. Quaisquer menções a tempo e custos (que eventualmente apareciam) eram removidas.

---

### Fase 3: Conversão dos Diagramas Mermaid para SVG

Os diagramas criados em formato Mermaid foram convertidos para SVG para melhor integração com o HTML.

**Processo:**
- Utilização da biblioteca **mermaid-cli** para conversão
- Padronização da estrutura de armazenamento para facilitar a localização de cada diagrama
- Upload das imagens SVG para um **container no Azure Blob Storage**

**Objetivo:** Garantir que os diagramas fossem exibidos de forma otimizada no documento HTML final.

---

### Fase 4: Criação do HTML de Assessment

Nesta fase, o assessment em Markdown foi transposto para um documento HTML completo, utilizando o template visual da Avanade.

**Prompt utilizado:**

```
Preciso que utilize com template o arquivo HTML, para transpor as informações do arquivo md pra html.
Ou seja, desejo que o contéudo do arquivo md seja transformado html utilizando como template o html anexado, se comportamento, cores e estilos devem ser mantidos.
Preciso que a localização deste arquivo seja feito em assessment -> HTML -> *nome do repositório. Neste primeiro momento para os diagramas, utilize o mermaid cli para converter em svg, as imagens dos diagramas salve no mesmo path do html, porém dentro de uma pasta img.
Para evitar problemas faça de forma incremental o código do html.
Não utiliza de biblioteca js para demonstrar os diagramas mermaid.
```

**Processo de revisão:**
1. Revisão minuciosa manual e com auxílio da IA
2. Identificação de erros de conteúdo e problemas de estilização
3. Correção dos problemas de acordo com a complexidade (manual ou com auxílio da IA)

---

### Fase 5: Criação do Resumo Executivo em Markdown

Com base no assessment completo, foi gerada uma versão resumida focada nos pontos críticos para a migração.

**Prompt utilizado:**

```
Solicita-se que este trabalho seja conduzido por um especialista em arquitetura de soluções, responsável por realizar entregar uma apresentação de assessment com base no documentação em anexo, gerar uma resumo executivo trazendo de forma objetiva e transparente os pontos de necessidade de refatoração de código, lembrado que tem que deixar explicito caso haja necessidade de refatoração e o nivel de complexidade
```

**Revisão:**
Verificação da conformidade do conteúdo do resumo executivo com o assessment detalhado.

---

### Fase 6: Criação do HTML do Resumo Executivo

A última fase consistiu na criação de uma página HTML única (single page) com os principais pontos de atenção para a migração.

**Prompt utilizado:**

```
Preciso transformar esse arquivo resumo executivo de um assessment em .md em um documento HTML único seguindo padrões de acessibilidade e design, siga exatamente o template em HTML em anexo.
gostaria que o nome do arquivo HTML, tivesse um prefixo de resumo-*nome do md
```

**Contexto fornecido:**
- Template HTML específico para resumos executivos

**Finalização:**
- Revisão final do conteúdo
- Verificação de conformidade com o assessment
- Marcação da task como **Done**

---

## Estrutura de Organização

```
assessment/
├── [nome-do-repositorio].md
├── HTML/
│   └── [nome-do-repositorio]/
│       ├── index.html
│       └── img/
│           └── *.svg
├── resumo-executivo/
│   └── [nome-do-repositorio].md
└── resumo-executivo-html/
    └── resumo-[nome-do-repositorio].html
```

---

## Considerações Finais

Este processo estruturado em seis fases garantiu:
- **Padronização** na documentação de todos os 38 repositórios
- **Qualidade** técnica nas avaliações realizadas
- **Visibilidade** para stakeholders através de múltiplos formatos de apresentação
- **Rastreabilidade** das decisões técnicas relacionadas à migração AWS → Azure

O uso estratégico do GitHub Copilot como agente arquiteto de soluções permitiu acelerar o processo mantendo a qualidade técnica esperada para assessments de migração cloud.
