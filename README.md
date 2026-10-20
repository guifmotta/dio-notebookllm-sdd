# OpenSpec: O Framework de Especificações para Engenharia de Software

Desafio NotebookLLM - OpenSpec: O Framework de Especificações para Engenharia de Software

## Interação inicial

Quero aprender mais sobre Spec-Driven Development especialmente utilizando a ferramenta OpenSpec

## Fontes utilizadas

[OpenSpec | A lightweight and configurable spec framework](https://openspec.dev/)  
[O que é desenvolvimento orientado por especificações? | IBM](https://www.ibm.com/br-pt/think/topics/spec-driven-development)  
[Spec-Driven Development: o que é e como usar com IA](https://www.softdesign.com.br/blog/spec-driven-development/)  
[Beginner's Guide to Spec-Driven Development (SDD) With OpenSpec](https://www.youtube.com/watch?v=9MImID9o8MQ)  
[Do zero ao código com IA: por que você precisa de especificações](https://www.youtube.com/watch?v=dQ481H54nrM)  
[Full Course: Spec-Driven Development with Coding Agents](https://www.youtube.com/watch?v=hy8UstR2NEg)  
[Spec-Driven Development na prática com OpenSpec e Claude Code](https://www.youtube.com/watch?v=uCr_vqW8LpQ)  
[Spec-Driven Development: A Habilidade #1 para Devs de 2026 (Guia Completo)](https://www.youtube.com/watch?v=YFDp-smGYqQ)

## Perguntas realizadas
1. O que é o conceito de Delta Specs no OpenSpec?
  > O conceito de **Delta Specs** no OpenSpec é o mecanismo utilizado para documentar e gerenciar **apenas as diferenças e alterações** (*deltas*) entre o estado atual das especificações do sistema e as novas modificações solicitadas[1][2].
  > 
  >### Como funciona na prática?
  >
  >1. **Rastreamento Enxuto de Mudanças**: Em vez de reescrever toda a documentação do projeto a cada alteração, o OpenSpec cria uma pasta de mudança ativa (`changes/`) que registra estritamente o que está sendo adicionado ou modificado[1][2].
  >2. **Separação por Capacidades (** **Capabilities** **)**: As funcionalidades do sistema são divididas em "capacidades"[2][3]. Quando um requisito existente precisa evoluir (por exemplo, alterar o fluxo de autenticação ou incluir um novo botão), a Delta Spec lista a capacidade afetada como **modificada** e detalha apenas a diferença em relação ao estado anterior[1][2].
  >3. **Consolidação na Fonte da Verdade**: Assim que a nova funcionalidade é implementada e testada, o comando `/opsx archive` promove as Delta Specs e mescla as alterações de volta às especificações globais do sistema, mantendo a documentação sempre atualizada e sincronizada com o código[2][4].
  >
  >### Principais Vantagens
  >
  >* **Essencial para Projetos Existentes (** **Brownfield** **)**: Facilita a evolução de bases de código legadas sem a necessidade de reespecificar o sistema inteiro do zero[1].
  >* **Economia de Tokens e Contexto**: Ao limitar a leitura do agente de IA apenas às mudanças ativas e relevantes daquela tarefa, evita-se desperdício de tokens e problemas de degradação de contexto[1][2].
  >* **Rastreabilidade e Histórico**: Mantém um histórico claro e versionado de como cada requisito foi transformado ao longo do tempo[2][4].

  *Fontes utilizadas:*  
  Beginner's Guide to Spec-Driven Development (SDD) With OpenSpec  
  Spec-Driven Development na prática com OpenSpec e Claude Code

2. Como o OpenSpec lida com projetos legados?
>O **OpenSpec** foi projetado para ser extremamente eficiente no trabalho com **projetos existentes e sistemas legados** (projetos *brownfield*), eliminando a necessidade de reescrever o código do zero ou documentar todo o sistema de uma só vez[1].
>
>A abordagem do OpenSpec para bases de código legadas baseia-se em três pilares principais:
>
>---
>
>### 1\. Mapeamento de Contexto e Constituição da Base Legada
>
>Ao introduzir a metodologia em um projeto existente, o agente de IA faz uma varredura no repositório, analisando a estrutura do código-fonte, histórico e arquivos de apoio existentes (como `README.md` ou listas de tarefas)[2][3].
>
>* A partir dessa análise, é criada a **Constituição do Projeto** (armazenada em documentos de contexto e configurada em `openspec/config.yaml`)[3][4].
>* Esse arquivo mapeia a *stack* tecnológica, convenções de código, padrões de arquitetura e decisões passadas, garantindo que qualquer nova alteração feita pela IA respeite e se alinhe ao código já escrito no projeto[3]>[4].
>
>---
>
>### 2\. Uso de Delta Specs (Foco Apenas na Mudança Ativa)
>
>Tentar carregar ou especificar toda a base de código legada de uma só vez consumiria a janela de contexto da IA e geraria documentações extensas e difíceis de manter[1][5].
>
>* Com o conceito de **Delta Specs**, o OpenSpec isola a modificação na pasta de alterações ativas (`changes/`) e documenta **apenas as diferenças** entre a especificação anterior e o novo requisito desejado[1][6].
>* Na proposta da alteração (`proposal.md`), o OpenSpec diferencia claramente o que são **novas capacidades** (*new capabilities*) do que são **capacidades modificadas** (*modified capabilities*) do sistema legado[6].
>
>---
>
>### 3\. Documentação e Reestruturação Incremental
>
>* A documentação da aplicação legada não precisa nascer perfeita nem completa; ela é construída e enriquecida **gradualmente, demanda por demanda**[1].
>* Sempre que uma tarefa é implementada (`opsx apply`) e validada, o comando `opsx archive` promove a Delta Spec e mescla as alterações com a fonte da verdade do sistema[1][6].
>* Isso permite que, a cada nova funcionalidade ou refatoração, o projeto legado ganhe mais cobertura de especificações vivas sem sobrecarregar a memória do agente nem consumir tokens desnecessariamente[1][7].

*Fontes utilizadas:*  
  Beginner's Guide to Spec-Driven Development (SDD) With OpenSpec  
  Full Course: Spec-Driven Development with Coding Agents

3. Qual o procedimento correto ao alterar uma especificação já consolidada?
>Ao alterar uma especificação que já foi consolidada e arquivada como fonte da verdade do sistema (`openspec/specs/`), o procedimento correto no **OpenSpec** não é reescrever a documentação antiga manualmente ou alterar diretamente o código existente[1].
>
>O framework utiliza o conceito de **Delta Specs** dentro de um ciclo de mudança controlado para evoluir a especificação com rastreabilidade[1][2][4]. O passo a passo correto é:
>
>---
>
>### 1\. Iniciar uma Nova Proposta de Mudança (`opsx explore` e `opsx propose`)
>
>* Começa-se uma nova sessão de exploração para alinhar o novo requisito ou a modificação com o agente de IA[5][6].
>* Ao executar o comando `opsx propose`, o OpenSpec cria um novo diretório de alteração ativa dentro de `openspec/changes/`[5][7][8].
>
>### 2\. Registrar a Alteração como uma *Modified Capability* (Delta Spec)
>
>* No arquivo `proposal.md` gerado para essa mudança, a especificação afetada é categorizada na seção de **modified capabilities** (capacidades modificadas), e não como uma capacidade totalmente nova[2][8].
>* É criada uma **Delta Spec**: em vez de duplicar ou refazer todo o documento da funcionalidade, registra-se **apenas o delta (a diferença)** entre o comportamento consolidado anterior e o novo comportamento desejado[1][2].
>* **Vantagem**: Isso evita a degradação de contexto e reduz drasticamente o consumo de tokens na IA, mantendo o foco estritamente no que muda[1][9].
>
>### 3\. Implementar as Tarefas de Alteração (`opsx apply`)
>
>* O agente de IA lê a Delta Spec e o plano de tarefas atualizado (`tasks.md`) para realizar as modificações necessárias no código-fonte[5].
>* Como o escopo da Delta Spec é delimitado às diferenças, a alteração no código ocorre de forma isolada e sem quebrar o restante da aplicação[1][2].
>
>### 4\. Arquivar e Mesclar com a Fonte da Verdade (`opsx archive`)
>
>* Após testar e validar o novo comportamento, executa-se o comando `opsx archive`[5][12].
>* O OpenSpec promove a Delta Spec e **mescla (** **merge** **)** as alterações diretamente no arquivo de especificação global em `openspec/specs/`[2][4].
>* A pasta temporária de mudança em `changes/` é encerrada e a especificação global passa a refletir o novo estado consolidado do sistema[4][12].

*Fontes utilizadas:*  
  Beginner's Guide to Spec-Driven Development (SDD) With OpenSpec  
  Full Course: Spec-Driven Development with Coding Agents  
  Spec-Driven Development na prática com OpenSpec e Claude Code
  O que é desenvolvimento orientado por especificações? | IBM

## Link NotebookLLM
(https://notebook.google.com/notebook/15ad8eda-ac56-4125-a4be-53adda569bb1)
