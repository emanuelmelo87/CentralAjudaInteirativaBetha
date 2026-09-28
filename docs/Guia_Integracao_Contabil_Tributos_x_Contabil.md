# Guia Operacional: Integração Contábil (Tributos x Contábil)

**Preparação para a Prestação de Contas 2027 (e-Sfinge / TCE-SC)**

Base: comunicado Betha de 21/09/2026, "Prestação de contas 2027: Evolução na rotina de Integração Contábil".

> **Obrigatório para municípios de Santa Catarina (e-Sfinge) e Paraná (SIM-AM).** As regras entram em vigor em **janeiro de 2027**, mas as rotinas descritas aqui já estão disponíveis e devem ser adotadas desde já. Quanto antes as movimentações forem integradas de forma completa e no período correto, menor será o volume de ajustes em 2027.

---

## 1. Por que este guia é importante

A partir de 2027, o e-Sfinge passa a contar com duas consistências **impeditivas**:

| Consistência | O que valida | Efeito |
|---|---|---|
| **CON 811** | Saldos a receber provenientes de **lançamentos** | Bloqueia o envio |
| **CON 812** | Saldos a receber provenientes de **dívidas** | Bloqueia o envio |

Por serem impeditivas, **não geram apenas alerta: barram a remessa**. Para atendê-las, duas condições precisam ser cumpridas ao mesmo tempo:

1. **Toda** movimentação deve ser integrada, sem exceções.
2. As integrações devem seguir **rigorosamente a ordem** estabelecida (seção 4).

> **Atenção:** integrar tudo não basta se a ordem não for respeitada. Uma base com 100% das movimentações integradas, porém fora de ordem, pode apresentar saldo incorreto exatamente como uma base incompleta.

---

## 2. Rotinas de integração disponíveis hoje

Estas 11 rotinas já estão disponíveis no Tributos e devem ser utilizadas desde já:

- [ ] 1. Lançamentos
- [ ] 2. Cancelamentos de lançamentos
- [ ] 3. Inscrição de dívidas
- [ ] 4. Cancelamentos de dívidas
- [ ] 5. Prescrição de dívidas
- [ ] 6. Imunidade
- [ ] 7. Incentivos
- [ ] 8. Remissão
- [ ] 9. Isenção
- [ ] 10. Pagamentos
- [ ] 11. Estornos de pagamentos

---

## 3. Movimentações ainda sem integração (em desenvolvimento)

As movimentações abaixo ainda não possuem integração ou precisam ser aprimoradas. Enquanto não estiverem disponíveis, **podem gerar divergência de saldo** e exigir ajuste manual:

1. Integração de restituições
2. Estorno de cancelamento de lançamento
3. Estorno de dívida ativa
4. Estorno de prescrição
5. Estorno de isenção
6. Estorno de imunidade
7. Estorno de remissão
8. Estorno de benefício fiscal
9. Revogação de benefícios fiscais (isenção, imunidade e demais benefícios)
10. Integração das taxas vinculadas
11. Integração das taxas de parcelamento
12. Integração dos pagamentos dessas taxas dentro do parcelamento
13. Integração dos acréscimos

A maior parte são **estornos**: hoje a entrada de um evento chega à Contabilidade, mas o seu desfazimento não, o que por si só produz divergência.

> **Regra de ouro:** toda movimentação lançada manualmente no sistema **Contábil** deve ser replicada no sistema **Tributos**. Caso contrário, voltarão a ocorrer divergências entre os dois sistemas.

---

## 4. Ordem obrigatória das integrações (ação imediata)

**Hoje não existe trava no sistema que impeça a integração fora de ordem.** O sistema aceita e conclui a integração normalmente, mas o saldo resultante fica incorreto. Até que a "amarração de integridade e ordem" (em desenvolvimento) esteja disponível, **garantir a sequência correta é responsabilidade de quem opera a rotina.**

### Lógica das dependências

- **Primeiro o lançamento**; depois as movimentações relacionadas a ele (cancelamentos, pagamentos, estornos, benefícios).
- **Primeiro a inscrição em dívida ativa**; depois as movimentações vinculadas a ela (acréscimos, pagamentos, estornos, prescrições).

### Checklist mensal de integração

Execute nesta ordem, a cada período:

- [ ] **Passo 1.** Integrar **todos** os lançamentos do período.
- [ ] **Passo 2.** Integrar as inscrições em dívida ativa.
- [ ] **Passo 3.** Integrar as movimentações dependentes: cancelamentos, prescrições, benefícios (isenção, imunidade, incentivos, remissão) e estornos.
- [ ] **Passo 4.** Integrar os pagamentos **somente** quando o lançamento ou a dívida correspondente já estiver integrado.
- [ ] **Passo 5.** Conferir se não há nenhuma movimentação pendente de integração.
- [ ] **Passo 6.** Somente então encerrar o período.

> **Não encerre o período com movimentação pendente de integração.** O que ficar para trás só será corrigível reabrindo o mês.

### O que acontece se a ordem não for respeitada

Exemplo: um pagamento integrado **antes** do lançamento correspondente.

1. A Contabilidade recebe o pagamento sem o crédito registrado: ele entra como "não lançado" e não baixa saldo nenhum.
2. Quando o lançamento é integrado depois, chega como um crédito novo, em aberto.
3. Resultado: **o saldo permanece aberto mesmo com o pagamento já efetuado e integrado.**

Essa divergência **não se resolve integrando de novo**. Corrigir exige intervenção manual e, se o mês já foi encerrado, exige reabri-lo.

---

## 5. Carga inicial: conferência e ajuste de saldos

Como os valores atualmente registrados podem não estar compatíveis entre Contábil e Tributos, pode ser necessário um **ajuste manual único** para equalizar os saldos. Alinha-se o ponto de partida uma vez e, dali em diante, a rotina de integração mantém os dois sistemas juntos, salvo movimentações da seção 3 ou lançamentos manuais na Contabilidade.

### 5.1 Definir a data de corte

- [ ] Definir o mês que será o ponto de partida da integração (**data de corte**).
- [ ] No **Tributos**, acessar **Central de configurações > Integrações contábeis** e preencher o campo **Mês/Ano do Ajuste (Principal) - Lançamentos**. Salvar.

**Premissas da data de corte:**

- Nenhuma movimentação pode ter sido integrada com data **posterior** à data de corte. *Exemplo: se a data de corte for setembro, nenhuma movimentação de outubro pode ter sido contabilizada.*
- Todas as integrações e movimentações **anteriores** à data de corte serão consideradas já contabilizadas, pois é a partir desse saldo que será feito o ajuste manual.
- Após o ajuste, as novas movimentações seguem o fluxo normal de integração, respeitando obrigatoriamente a ordem da seção 4.

### 5.2 Emitir os relatórios de conferência

**No sistema Tributos:**

- [ ] **[Tributos] Demonstrativo de Saldo de Dívida Ativa**: saldo acumulado das dívidas até a competência, agrupado por receita ou rubrica.
- [ ] **[Tributos] Demonstrativo de Saldo de Lançamento**: saldo acumulado dos lançamentos até a competência, agrupado por receita ou rubrica.

Parâmetros: **Ano**, **Competência** (mês da data de corte), **Agrupamento** (ex.: Por crédito/receita) e, se desejado, **Crédito Tributário** (ex.: IPTU).

**No sistema Contábil:**

- [ ] **Comparativo da Receita Lançada com Arrecadada**: verificar, na coluna **Saldo**, o valor de cada natureza de receita correspondente ao tributo.
  Parâmetros: **Exercício**, **Consolidado**, **Entidade**, **Detalhar Naturezas Sintéticas?** e **Mês**.
- [ ] **Balancete Dinâmico**: verificar a coluna **Saldo Final** de cada conta contábil correspondente ao tributo.

### 5.3 Regras de ajuste

| Situação encontrada | Ação | Onde fazer (Contábil) |
|---|---|---|
| Balancete dinâmico **e** receita lançada **iguais** ao Tributos | Nenhum ajuste necessário | - |
| Saldo do **balancete dinâmico divergente** | Lançamento contábil manual em cada conta divergente, igualando ao saldo tributário | **Escriturando > Escriturações de documentos > + Lançamento contábil** |
| Saldo da **receita lançada divergente** | Cadastrar lançamento de receita em cada conta divergente, igualando ao saldo tributário | **Executando > Receita > Lançamentos > + Lançamentos** |
| **Dívida ativa** | Considerar apenas a comparação pelo balancete dinâmico, com ajuste por lançamento contábil manual | **Escriturando > Escriturações de documentos > + Lançamento contábil** |

- [ ] Em todos os ajustes, usar a **mesma data do relatório de Tributos**.

### 5.4 Validação final do ajuste

- [ ] Reemitir os relatórios do Contábil e confirmar que os saldos estão **iguais** aos do relatório de Tributos.

> **Importante:** se os saldos não estiverem iguais, o ajuste não está concluído e toda integração posterior partirá de uma base divergente.

Para detalhes do processo no sistema Contábil (Cloud), consulte o comunicado completo na **Central de Ajuda** do produto.

---

## 6. Acréscimos (controle manual pelo cliente)

> **Acréscimos não possuem integração automática. O controle também é do cliente.**

Os ajustes contábeis devem contemplar os acréscimos. Nos relatórios de Tributos é possível visualizar:

- o valor acumulado dos acréscimos até a data da carga inicial;
- os valores de acréscimos gerados mensalmente ao longo do período.

**Na carga inicial:**

- [ ] Conferir e ajustar considerando **o valor original do tributo e o valor acumulado de acréscimos**.

**Todo mês, enquanto não houver integração automática:**

- [ ] Emitir o relatório e identificar os acréscimos gerados no período.
- [ ] Realizar o ajuste manual correspondente na Contabilidade.

Deixar de fazer esse acompanhamento não bloqueia as demais integrações, mas faz o saldo contábil se distanciar do tributário mês a mês, **exatamente o que as consistências CON 811 e CON 812 vão medir a partir de 2027**. A integração automática de acréscimos está em desenvolvimento e será entregue nos próximos meses.

---

## 7. Resumo: checklist de fechamento mensal

- [ ] Todos os lançamentos do período integrados
- [ ] Todas as inscrições em dívida ativa integradas
- [ ] Cancelamentos, prescrições, benefícios e estornos integrados (após os itens acima)
- [ ] Pagamentos integrados somente após o lançamento ou a dívida correspondente
- [ ] Nenhuma movimentação pendente de integração
- [ ] Movimentações manuais feitas no Contábil replicadas no Tributos
- [ ] Movimentações da seção 3 (sem integração) identificadas e ajustadas manualmente
- [ ] Acréscimos do mês ajustados manualmente na Contabilidade
- [ ] Saldos conferidos entre Tributos e Contábil
- [ ] Período encerrado

---

*Em caso de dúvidas, entre em contato com a equipe de atendimento Betha.*

Emanuel de Melo Alexandre
Coordenador de Serviços
Betha Sistemas Ltda
