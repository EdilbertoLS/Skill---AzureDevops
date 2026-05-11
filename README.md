# Skill — Criação de Atividades Azure DevOps

> **⚠️ Esta skill NÃO integra com a API do Azure DevOps.**  
> Ela estrutura o conteúdo de uma atividade no padrão do Azure DevOps Boards
> a partir de uma frase ou solicitação em linguagem natural. O registro do item
> no board deve ser feito manualmente ou por um processo separado.

---

## O que é esta skill?

Uma skill reutilizável que orienta um agente de IA a transformar uma solicitação
curta e informal em uma atividade bem estruturada para o **Azure DevOps Boards**,
distinguindo os tipos **Bug** e **Evolução** e aplicando **Definition of Done (DoD)**
adequado a cada caso.

## Como funciona?

1. O usuário fornece uma frase ou parágrafo descrevendo o problema ou a necessidade.
2. O agente utiliza as instruções desta skill (`skill.yaml`) para:
   - Classificar a atividade como **Bug** ou **Evolução**.
   - Estruturar todos os campos relevantes da atividade.
   - Gerar o **DoD** adequado ao tipo.
   - Sinalizar premissas adotadas e dúvidas em aberto.
3. A saída é um documento Markdown pronto para ser copiado ao Azure DevOps.

---

## Como usar

### 1. Referencie a skill no contexto do agente

Inclua o conteúdo de `skill.yaml` como instrução do sistema (system prompt) ou
como contexto da skill do seu agente. O campo `instructions` contém as regras
completas de comportamento.

### 2. Envie uma solicitação em linguagem natural

Exemplos de entrada válida:

```
O botão de salvar na tela de cadastro não está respondendo quando o usuário clica.
```

```
Quero adicionar um filtro por data na listagem de pedidos.
```

```
Criar relatório exportável em Excel com os dados de vendas do mês.
```

```
Erro 500 ao tentar acessar o perfil de um usuário inativo.
```

```
Melhorar a performance da tela de consulta de estoque que demora mais de 10 segundos.
```

```
Ajustar o cálculo de desconto que está retornando valor negativo.
```

### 3. Receba a atividade estruturada

O agente retorna um documento com os seguintes campos:

| Campo | Obrigatoriedade |
|---|---|
| Tipo (Bug ou Evolução) | Obrigatório |
| Título | Obrigatório |
| Contexto / Solicitação original | Obrigatório |
| Descrição do problema ou necessidade | Obrigatório |
| Objetivo / Resultado esperado | Obrigatório |
| Campos específicos por tipo (comportamento atual/esperado ou valor/escopo) | Obrigatório |
| Critérios de aceite | Obrigatório |
| Definition of Done (DoD) | Obrigatório |
| Impacto / Prioridade | Inferido com cautela |
| Premissas / Dúvidas em aberto | Quando houver ambiguidade |

---

## Regras de classificação

### 🐛 Bug
Classifique como Bug quando houver indícios de:
- Erro, falha, comportamento incorreto, regressão ou exceção.
- Funcionalidade já existente que não funciona como deveria.
- Divergência entre comportamento atual e esperado.
- Palavras-chave: *erro, falha, quebrado, não funciona, exceção, crash, travando,
  divergência, regressão, problema, tela branca, dado errado, cálculo errado.*

### 🚀 Evolução
Classifique como Evolução quando houver indícios de:
- Nova funcionalidade, melhoria de UX, automação ou otimização solicitada.
- Alteração de regra de negócio ou extensão de funcionalidade existente.
- Ausência de relato de falha — há desejo de algo novo ou diferente.
- Palavras-chave: *novo, adicionar, criar, implementar, melhorar, ajustar, automatizar,
  refatorar, otimizar, habilitar, permitir, regra nova, melhoria.*

### Caso ambíguo
Se a classificação não for clara:
1. O agente faz a melhor classificação inicial.
2. Declara a premissa adotada.
3. Lista as dúvidas em aberto — **sem bloquear** a criação do rascunho.

---

## Definition of Done (DoD)

### DoD — Bug
- [ ] Causa raiz identificada e documentada
- [ ] Correção implementada e revisada por pares (code review)
- [ ] Testes de regressão executados e aprovados
- [ ] Comportamento corrigido validado em ambiente de homologação
- [ ] Nenhum novo Bug introduzido na correção
- [ ] Documentação/changelog atualizado (se aplicável)

### DoD — Evolução
- [ ] Requisitos e critérios de aceite cobertos pela implementação
- [ ] Código implementado e revisado por pares (code review)
- [ ] Testes unitários e/ou de integração escritos e aprovados
- [ ] Funcionalidade validada em ambiente de homologação
- [ ] Documentação atualizada (se aplicável)
- [ ] Aprovação do responsável de produto/negócio (se aplicável)

> O agente adapta o DoD ao contexto — remove itens que não se aplicam e adiciona
> itens específicos quando a solicitação fornece informação suficiente.

---

## Exemplos completos de entrada e saída

| Tipo | Arquivo |
|---|---|
| Bug | [`examples/bug-example.md`](examples/bug-example.md) |
| Evolução | [`examples/evolution-example.md`](examples/evolution-example.md) |

---

## Estrutura do repositório

```
Skill---AzureDevops/
├── skill.yaml                   # Definição completa da skill (instruções do agente)
├── README.md                    # Esta documentação
└── examples/
    ├── bug-example.md           # Exemplo de saída para um Bug
    └── evolution-example.md     # Exemplo de saída para uma Evolução
```

---

## Limitações e avisos

- Esta skill **não cria itens no Azure DevOps**. Ela apenas estrutura o conteúdo
  da atividade em formato padronizado.
- Campos marcados como "Inferir com cautela" são preenchidos apenas quando há
  evidência suficiente na solicitação. Quando não há, o agente indica
  "Não informado" ou "Requer alinhamento".
- O agente não inventa detalhes técnicos (nomes de tabelas, endpoints, serviços)
  sem base na solicitação original.

---

## Licença

Este projeto está licenciado sob a [Apache License 2.0](LICENSE).
