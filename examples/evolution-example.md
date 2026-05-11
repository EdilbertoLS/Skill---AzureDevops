# Exemplo de saída — Evolução

**Entrada do usuário:**
> "Quero adicionar um filtro por data na listagem de pedidos"

---

## 📋 ATIVIDADE AZURE DEVOPS

**Tipo:** Evolução

**Título:** Adicionar filtro por intervalo de datas na listagem de pedidos

**Contexto / Solicitação original:**
> Quero adicionar um filtro por data na listagem de pedidos

**Descrição do problema ou necessidade:**
A tela de listagem de pedidos não possui opção de filtro por data, o que obriga o
usuário a percorrer toda a lista para localizar pedidos de um período específico.
A melhoria consiste em adicionar um componente de filtro por intervalo de datas
(data inicial e data final) que refine os resultados exibidos na listagem.

**Objetivo / Resultado esperado:**
O usuário deve conseguir filtrar a listagem de pedidos por um intervalo de datas
(data inicial e data final), reduzindo os resultados exibidos ao período informado
e facilitando a localização de pedidos específicos.

**Valor esperado:**
Redução do tempo gasto pelo usuário para localizar pedidos em períodos específicos,
aumentando a produtividade e melhorando a experiência de uso da listagem.

**Escopo:**
- **Dentro do escopo:** componente de filtro por data inicial e data final na tela
  de listagem de pedidos; aplicação do filtro à consulta de dados; exibição dos
  resultados filtrados.
- **Fora do escopo (inferido — confirmar):** exportação dos resultados filtrados;
  filtros adicionais (status, cliente, valor); salvar filtros como favoritos.

**Usuários / Perfis impactados:**
Todos os usuários com acesso à tela de listagem de pedidos.
*(Confirmar se há perfis com restrições de visualização que devam ser respeitadas.)*

**Critérios de aceite:**
- [ ] A tela de listagem de pedidos exibe campos de "Data inicial" e "Data final".
- [ ] Ao aplicar o filtro, apenas pedidos dentro do intervalo informado são exibidos.
- [ ] O campo de data aceita seleção por calendário e entrada manual no formato
      DD/MM/AAAA (ou conforme padrão já adotado no produto).
- [ ] Se apenas "Data inicial" for informada, são exibidos pedidos a partir dessa data.
- [ ] Se apenas "Data final" for informada, são exibidos pedidos até essa data.
- [ ] Se nenhum filtro for informado, todos os pedidos são exibidos (comportamento atual).
- [ ] Datas inválidas ou intervalo incoerente (inicial > final) exibem mensagem de
      erro clara ao usuário.
- [ ] O filtro é aplicado sem necessidade de recarregar a página (se o produto já
      adota interatividade client-side) — *confirmar expectativa técnica*.

**Definition of Done (DoD):**
- [ ] Requisitos e critérios de aceite cobertos pela implementação
- [ ] Código implementado e revisado por pares (code review)
- [ ] Testes unitários e/ou de integração escritos e aprovados
- [ ] Funcionalidade validada em ambiente de homologação
- [ ] Documentação atualizada (se aplicável)
- [ ] Aprovação do responsável de produto/negócio

**Impacto / Prioridade:** Não definida — requer alinhamento com o time.
> Não há evidência de urgência ou criticidade na solicitação original.
> Sugestão: alinhar prioridade com o Product Owner considerando o volume de
> reclamações/solicitações similares.

**Premissas / Dúvidas em aberto:**
- Premissa: o filtro deve ser aplicado sobre a data de criação do pedido.
  Confirmar se deve ser data de criação, data de entrega, data de faturamento
  ou outra data relevante do domínio.
- Premissa: a listagem já possui paginação ou scroll — o filtro deve manter
  o comportamento de paginação existente.
- ❓ O filtro deve ser aplicado do lado do servidor (query no banco) ou do lado
  do cliente (filtro no array em memória)?
- ❓ Há limite de intervalo de datas? (ex: máximo de 90 dias por consulta)
- ❓ O filtro deve persistir ao navegar entre telas ou é sempre resetado?
- ❓ Há necessidade de exportar os resultados filtrados agora ou é escopo futuro?
