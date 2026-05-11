# Exemplo de saída — Bug

**Entrada do usuário:**
> "O botão de salvar na tela de cadastro não está respondendo quando o usuário clica"

---

## 📋 ATIVIDADE AZURE DEVOPS

**Tipo:** Bug

**Título:** Corrigir botão "Salvar" sem resposta na tela de cadastro

**Contexto / Solicitação original:**
> O botão de salvar na tela de cadastro não está respondendo quando o usuário clica

**Descrição do problema ou necessidade:**
Na tela de cadastro, o botão "Salvar" não executa nenhuma ação ao ser clicado pelo
usuário. O comportamento esperado é que, ao acionar o botão, o formulário seja
validado e os dados sejam persistidos. A ausência de resposta impede a conclusão do
cadastro, bloqueando o fluxo do usuário.

**Objetivo / Resultado esperado:**
Ao clicar no botão "Salvar", o sistema deve validar os campos do formulário de
cadastro e, se válidos, persistir as informações e exibir confirmação de sucesso.
Em caso de erro de validação, deve exibir mensagem de orientação ao usuário.

**Comportamento atual:**
O botão "Salvar" não responde ao clique — nenhuma ação é disparada, nenhuma
mensagem é exibida e os dados não são gravados.

**Comportamento esperado:**
Ao clicar em "Salvar", o formulário é validado e:
- Se válido → dados são gravados e o usuário recebe confirmação.
- Se inválido → campos com erro são destacados com mensagem explicativa.

**Passos para reproduzir:**
1. Acessar a tela de cadastro.
2. Preencher os campos do formulário.
3. Clicar no botão "Salvar".
4. Observar que nenhuma ação é executada.

**Impacto:** Alto — o fluxo de cadastro está completamente bloqueado para todos
os usuários que tentam concluir o processo.

**Evidências / Logs:** Não informado — solicitar ao reporter logs de console e
captura de tela do comportamento.

**Critérios de aceite:**
- [ ] Ao clicar em "Salvar" com dados válidos, o cadastro é gravado com sucesso.
- [ ] Mensagem de confirmação é exibida após gravação bem-sucedida.
- [ ] Campos inválidos são destacados com mensagens de erro claras.
- [ ] O comportamento é consistente nos navegadores Chrome, Edge e Firefox
      (adicionar/remover conforme escopo do produto).
- [ ] Nenhuma regressão é introduzida em outras ações da mesma tela.

**Definition of Done (DoD):**
- [ ] Causa raiz identificada e documentada
- [ ] Correção implementada e revisada por pares (code review)
- [ ] Testes de regressão executados e aprovados
- [ ] Comportamento corrigido validado em ambiente de homologação
- [ ] Nenhum novo Bug introduzido na correção
- [ ] Documentação/changelog atualizado (se aplicável)

**Impacto / Prioridade:** Alta
> Justificativa: o fluxo de cadastro está completamente bloqueado, impedindo
> todos os usuários de concluir a operação.

**Premissas / Dúvidas em aberto:**
- Premissa: o botão existe na tela mas o evento de clique não está sendo tratado
  corretamente (ou está sendo suprimido por erro de JavaScript/validação).
- ❓ O problema ocorre em todos os ambientes (produção, homologação) ou apenas em um?
- ❓ Quando o comportamento foi introduzido? Houve deploy recente?
- ❓ Há logs de erro no console do navegador ou no servidor?
- ❓ O problema ocorre em todos os perfis de usuário ou apenas em alguns?
