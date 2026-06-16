# PROMPT COMPLETO — PORTAL DE PRESTAÇÃO DE CONTAS (Claude Opus)

---

You are an expert full-stack web developer specializing in clean, production-grade single-file HTML applications. Your task is to build a complete instructional + interactive web portal for monthly accountability documentation (prestação de contas) for a Civil Society Organization (OSC) in Brazil — specifically the **Cooperposse (Cooperativa dos Coletores de Material Reciclável de Santo Antônio de Posse)**, operating under a **Termo de Colaboração** with the Prefeitura Municipal.

The portal must work as:
1. A **step-by-step tutorial** guiding staff through the monthly process
2. An **interactive calculator/assistant** that automates computations from the RP-10 form
3. A **checklist tracker** for all required documents
4. A **reference hub** for normative rules and common mistakes

---

## TECHNICAL REQUIREMENTS

- **Single HTML file**: `portal-cooperposse.html`
- Vanilla JS, no frameworks, no build tools
- All CSS in `<style>`, all JS in `<script>` at end of `<body>`
- CDN only for fonts and icons:
  - Google Fonts: `DM Sans` (body) + `Fraunces` (display headings)
  - Lucide Icons: `<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.min.js"></script>`
- **No localStorage/sessionStorage** — use JS in-memory state only
- Fully responsive: mobile-first, works at 375px and 1280px+
- Light + dark mode via `data-theme` on `<html>`, with toggle button
- Skip-to-content link for accessibility
- Hash-based routing (`#inicio`, `#rp10`, `#checklist`, etc.) for navigation

---

## DESIGN DIRECTION

- **Tone**: Institutional, civic, trustworthy, practical. This is used by cooperative staff — not developers.
- **Color palette** (CSS custom properties):
  - Primary accent: Deep teal-blue (`#0a6b72` light / `#4f9ea8` dark) — civic authority
  - Warning: Amber (`#b45309`) for normative alerts
  - Success: Green (`#3d7a2a`) for checklist completion
  - Surfaces: Warm off-white light mode, dark charcoal dark mode
- **Typography**: `Fraunces` for section titles (serif, authoritative), `DM Sans` for all body/UI text
- **Layout**: Fixed left sidebar (260px) + scrollable main content area
  - Sidebar collapses to top hamburger menu on mobile
  - Active section highlighted in sidebar
- **Components**: Cards with subtle shadows, step-numbered lists, highlighted alert boxes, interactive calculator panels, progress badges

---

## SIDEBAR NAVIGATION STRUCTURE

Each sidebar item has: Lucide icon + label + status badge (Pendente / Em andamento / Concluído)
Status is togglable by user click, stored in JS memory.

```
1. 🏠  Início                    — Visão geral e alertas normativos
2. 📁  Preparação da Pasta       — Montagem da subpasta do mês
3. 📄  Ofício de Encaminhamento  — Como atualizar e carimbar
4. 📊  RP-10 (Doc Principal)     — Tutorial completo + calculadora
5. 📋  Relatório de Execução     — Orientações de preenchimento
6. 🏦  Conciliação Bancária      — Rende Fácil + extrato
7. 💳  PC-02 (Contas Bancárias)  — Termo de consentimento
8. 🗂️  Folha de Pagamento        — Procedimento e carimbos
9. ✅  Checklist Geral           — Todos os documentos do mês
10. ⚠️  Erros Comuns             — Referência rápida
```

---

## SECTION CONTENT — DETAILED SPECIFICATIONS

---

### SEÇÃO 1: INÍCIO

Display at top:
- Logo/title: "Portal de Prestação de Contas — Cooperposse"
- Subtitle: "Guia mensal para OSCs parceiras da Prefeitura de Santo Antônio de Posse"

**Alert card (amber/warning, prominent):**
> ⚠️ ATENÇÃO NORMATIVA
> A instrução normativa vigente é a **Instrução Normativa TCESP nº 01/2024**.
> NÃO faça referência à IN nº 01/2020 em NENHUM documento, ofício ou formulário.
> Documentos com referência à norma antiga serão devolvidos para correção.

**Card: Sobre a prestação de contas**
- A prestação de contas é sempre **referente ao mês anterior** à data de entrega
- Exemplo: entrega em junho → prestação referente a maio
- Baseada no **Termo de Colaboração nº 12/2026** (Aditivo Contratual nº 12/2026)
  - Vigência: 01/01/2026 a 15/09/2026 | Valor: R$ 228.000,00
  - Fonte de recurso: **Municipal**

**Card: Destino dos documentos**
- Cópia do RP-10 assinada → **Amanda** (prestação de contas)
- Original da Folha de Pagamento → **Lumen**
- Cópia da Folha de Pagamento carimbada → pasta da prestação de contas
- Todos os documentos digitalizados → upload no Portal de Transparência da Cooperposse

---

### SEÇÃO 2: PREPARAÇÃO DA PASTA

Step-by-step numbered tutorial:

**Passo 1 — Crie a subpasta do mês**
- Dentro da pasta principal "Subvenção", faça uma cópia da pasta do mês anterior
- Renomeie para o mês atual (ex: `Prestacao_Maio_2026`)
- Essa cópia serve como modelo de trabalho para a nova prestação

**Passo 2 — Reúna os documentos necessários**
Lista com checkboxes interativos:
- [ ] Extrato bancário do mês da prestação (conta principal)
- [ ] Extrato Rende Fácil do mês da prestação
- [ ] Comprovantes de pagamento do mês
- [ ] Planilha de contabilidade do mês (fornecida pela contabilidade)
- [ ] Folha de pagamento do mês
- [ ] Documentos/certificados para atualização no portal (a listar futuramente)

**Passo 3 — Atualize os arquivos e certificados nos portais**
- Seção reservada para links — adicionar futuramente
- Placeholder com instrução: "Links e certificados a serem adicionados conforme orientação"

---

### SEÇÃO 3: OFÍCIO DE ENCAMINHAMENTO

**O que é**: Documento formal que encaminha a prestação de contas à Secretaria.

**Passo a passo:**
1. Abra o modelo do mês anterior
2. Altere o **número do ofício**: incrementar o número sequencial do mês
   - Exemplo: Ofício nº 04/2026 → Ofício nº 05/2026
3. Altere todas as **datas** para o mês atual
4. Verifique se a referência normativa menciona: **Instrução Normativa TCESP nº 01/2024**
   - Se mencionar 01/2020, CORRIJA antes de imprimir
5. Imprima, assine e inclua na pasta

**Alert box (info):** "Sempre confira se o ofício menciona a IN TCESP 01/2024 antes de finalizar."

---

### SEÇÃO 4: RP-10 — DOCUMENTO PRINCIPAL (com calculadora interativa)

Esta é a seção mais importante do portal. Dividida em sub-abas ou seções expansíveis:

#### 4.1 — Cabeçalho e identificação
- Altere o mês e o exercício (ano)
- Verifique: Termo de Colaboração nº 12 / Aditivo nº 12/2026
- Origem dos recursos: **Municipal**

#### 4.2 — Tabela superior: Demonstrativo dos Recursos Disponíveis no Exercício

Instrução visual com tabela explicativa de cada coluna:

| Campo | Instrução |
|---|---|
| Coluna 1 — Data prevista para o repasse | Manter sempre **dia 10** do mês (fixo) |
| Coluna 2 — Valores previstos | Manter informação do mês anterior (não altera) |
| Coluna 3 — Data do repasse | Localizar no **extrato bancário** a data real do crédito |
| Coluna 4 — Número do documento de crédito | Localizar no **extrato bancário** o número do documento |
| Valores repassados | Valor do repasse conforme extrato bancário |

**Linhas de totais:**

| Campo | Como preencher |
|---|---|
| (A) Saldo do exercício anterior | Saldo bruto final do mês anterior no comprovante **Rende Fácil** |
| (B) Repasses públicos no exercício | Valor do(s) repasse(s) conforme extrato bancário do mês |
| (C) Receitas com aplicações financeiras | Rendimento do Rende Fácil no mês, **menos IOF e IR** do resgate |
| (D) Outras receitas | Normalmente R$ 0,00 |
| (E) Total de recursos públicos | Soma automática: A + B + C + D |
| (F) Recursos próprios da entidade | Preencher se houve tarifa bancária de transferência para outra conta da Cooperposse (saldo remanescente) |
| (G) Total de recursos disponíveis | Soma automática: E + F |

#### 4.3 — Calculadora Interativa do RP-10

**Construa um painel de calculadora** com os seguintes campos de entrada:

```
CALCULADORA RP-10

[A] Saldo do exercício anterior (Rende Fácil — último saldo bruto):  R$ [________]
[B] Repasses públicos no exercício (do extrato bancário):            R$ [________]
    [+ Adicionar repasse] — permite múltiplos repasses

Receitas de aplicação financeira:
  Rendimento bruto Rende Fácil:   R$ [________]
  IOF retido:                     R$ [________]
  IR retido:                      R$ [________]
[C] Receita líquida = Rendimento - IOF - IR:                         R$ [resultado automático]

[D] Outras receitas:                                                 R$ [________] (padrão 0,00)

═══════════════════════════════════════════════
[E] TOTAL DE RECURSOS PÚBLICOS (A+B+C+D):                           R$ [calculado]

[F] Recursos próprios (tarifa inter-bancos, se houver):             R$ [________]

[G] TOTAL DISPONÍVEL NO EXERCÍCIO (E+F):                            R$ [calculado]
═══════════════════════════════════════════════

DESPESAS — Tabela de Origem Municipal:

  Recursos humanos (folha de pagamento — salário bruto total):      R$ [________]
  Locação de imóveis:                                               R$ [________] (padrão R$ 2.500,00)
  Combustível:                                                      R$ [________]
  Despesas financeiras/bancárias (tarifas PIX, TED, etc.):         R$ [________]
  Outras despesas:                                                  R$ [________]

[J] TOTAL DESPESAS PAGAS NO EXERCÍCIO (H+I):                        R$ [calculado]

═══════════════════════════════════════════════
DEMONSTRATIVO DO SALDO FINANCEIRO:

[G] Total de recursos disponíveis:                                  R$ [espelho automático]
[J] Despesas pagas no exercício:                                    R$ [espelho automático]
[K] Recurso público não aplicado [E-(J-F)]:                        R$ [calculado]
    ✅ Este valor DEVE coincidir com o saldo bruto do Rende Fácil
[L] Valor devolvido ao órgão público:                               R$ 0,00 (fixo)
[M] Valor autorizado para exercício seguinte (K-L):                 R$ [espelho de K]

═══════════════════════════════════════════════
[📋 COPIAR RESUMO PARA COLAR NO WORD]  ← botão que copia texto formatado
```

O botão "Copiar resumo" deve gerar e copiar para o clipboard um bloco de texto formatado com todos os valores preenchidos, pronto para colar no documento Word do RP-10.

**Validação visual**: O campo (K) deve ter um indicador verde se coincidir com o saldo Rende Fácil, ou vermelho se divergir — baseado em campo adicional onde o usuário informa o saldo bruto do Rende Fácil para conferência.

#### 4.4 — Tabela de Despesas por Categoria

Instrução detalhada por linha da tabela DEMONSTRATIVO DAS DESPESAS INCORRIDAS NO EXERCÍCIO:

| Categoria | Instrução |
|---|---|
| Recursos humanos (5) | Total da folha de pagamento — salário bruto de todos os colaboradores |
| Locação de imóveis | R$ 2.500,00 (valor fixo mensal — manter) |
| Combustível | Consultar extrato ou comprovantes — valor variável |
| Despesas financeiras e bancárias | Soma de todas as tarifas de PIX, TED, tarifas bancárias — extrair do extrato |
| Outros campos | Preencher somente se houver movimentação correspondente |

Colunas da tabela:
- **Coluna H**: Despesas contabilizadas E pagas neste exercício (o valor principal)
- **Coluna I**: Despesas contabilizadas neste exercício a pagar em exercício seguinte (normalmente vazio)
- **Total J = H + I**

#### 4.5 — Finalização do RP-10

1. Confirme que o valor total de despesas (J) bate com os comprovantes
2. Confirme que (K) = saldo bruto Rende Fácil
3. Imprima **duas vias**:
   - Via 1 → Presidente assina → envia para **Amanda** com a prestação de contas
   - Via 2 → Arquivar na pasta física
4. Digitalize e faça upload no Portal de Transparência da Cooperposse

---

### SEÇÃO 5: RELATÓRIO DE EXECUÇÃO DO OBJETO

**O que é**: Documento narrativo descrevendo o que foi executado com os recursos no mês.

Instruções:
1. Descreva as ações realizadas no mês (serviços de coleta, atividades da cooperativa)
2. Use linguagem objetiva e factual — evite textos genéricos
3. Referencie o Termo de Colaboração nº 12/2026
4. Mencione os principais gastos do mês (folha, aluguel, combustível)
5. Assinar e incluir na pasta da prestação de contas

---

### SEÇÃO 6: CONCILIAÇÃO BANCÁRIA / RENDE FÁCIL

**Passo a passo:**

1. Acesse o extrato Rende Fácil do mês
2. Localize:
   - **Último saldo bruto** → campo (A) do RP-10 para o mês seguinte / campo de verificação (K)
   - **Rendimento bruto do mês** → para cálculo do campo (C)
   - **IOF retido** → subtrair do rendimento
   - **IR retido** → subtrair do rendimento
3. Acesse o extrato bancário principal do mês
4. Localize:
   - Créditos de repasse (data + número do documento de crédito) → tabela superior do RP-10
   - Pagamentos realizados (salários, aluguel, combustível, tarifas) → tabela de despesas
5. Confirme que o saldo final do extrato bancário coincide com o campo (K) do RP-10

**Calculadora auxiliar de rendimento líquido:**
```
  Rendimento bruto:     R$ [________]
  (-) IOF:              R$ [________]
  (-) IR:               R$ [________]
  = Receita líquida (C): R$ [resultado] [📋 Copiar]
```

---

### SEÇÃO 7: PC-02 — TERMO DE CONSENTIMENTO DE CONTAS BANCÁRIAS

- Documento que autoriza a fiscalização das contas bancárias da OSC pelo órgão público
- Atualizar com dados do período vigente
- Assinar e incluir na pasta da prestação de contas
- Observar se há novas contas bancárias a incluir

---

### SEÇÃO 8: FOLHA DE PAGAMENTO — PROCEDIMENTO E CARIMBOS

**Passo a passo:**
1. Receba a folha de pagamento do mês da contabilidade
2. **Carimbe** com o número do Termo de Colaboração:
   - Recurso: **Municipal**
   - Número: **Termo de Colaboração nº 12 / Aditivo Contratual nº 12/2026**
3. Faça **duas cópias** da folha carimbada:
   - Original → enviar para **Lumen**
   - Cópia carimbada → incluir na pasta da prestação de contas (para Amanda)
4. O valor total da folha (salário bruto) deve ser lançado no RP-10 como "Recursos humanos"

**Alert box:**
> 💡 O valor de Recursos Humanos no RP-10 deve corresponder ao salário bruto total da folha de pagamento do mês.

---

### SEÇÃO 9: CHECKLIST GERAL

Checklist interativo completo com todos os itens necessários para fechar a prestação de contas.
Cada item tem checkbox clicável (estado em memória JS), indicador visual de status, e seção de referência.

```
DOCUMENTOS DA PASTA — [Mês de referência: _______]

PREPARAÇÃO
[ ] Pasta do mês criada (cópia do mês anterior)
[ ] Extrato bancário do mês reunido
[ ] Extrato Rende Fácil do mês reunido
[ ] Comprovantes de pagamento reunidos
[ ] Planilha de contabilidade recebida
[ ] Folha de pagamento recebida da contabilidade

DOCUMENTOS A PREENCHER
[ ] Ofício de encaminhamento — número e datas atualizados
[ ] Ofício menciona IN TCESP 01/2024 (não 01/2020)
[ ] RP-10 preenchido — tabela de recursos
[ ] RP-10 preenchido — tabela de despesas
[ ] RP-10 verificado — (K) coincide com saldo Rende Fácil
[ ] Relatório de Execução do Objeto preenchido
[ ] Conciliação bancária realizada
[ ] PC-02 atualizado e assinado

FOLHA DE PAGAMENTO
[ ] Folha carimbada com Termo de Colaboração nº 12 / Aditivo 12/2026
[ ] Original enviado para Lumen
[ ] Cópia incluída na pasta da prestação

IMPRESSÃO E ASSINATURA
[ ] RP-10 impresso em 2 vias
[ ] Presidente assinou as duas vias
[ ] Via 1 do RP-10 entregue para Amanda
[ ] Via 2 do RP-10 arquivada na pasta física

DIGITALIZAÇÃO E UPLOAD
[ ] Todos os documentos digitalizados
[ ] Upload realizado no Portal de Transparência da Cooperposse

ENTREGA
[ ] Pasta entregue para Amanda (prestação de contas completa)
```

Mostrar barra de progresso visual no topo: "X de Y itens concluídos" com percentual.
Botão "Resetar checklist" para novo mês.
Campo de texto editável para indicar o mês de referência.

---

### SEÇÃO 10: ERROS COMUNS — REFERÊNCIA RÁPIDA

Cards de alerta com erros frequentes identificados:

1. **❌ Referência à IN 01/2020**
   - Problema: Ofícios e documentos ainda citando a norma antiga
   - Correto: Instrução Normativa TCESP nº **01/2024**

2. **❌ Campo (K) não coincide com o Rende Fácil**
   - Problema: Erro de cálculo ou lançamento errado nas despesas
   - Solução: Usar a calculadora do RP-10 e conferir o saldo bruto do extrato Rende Fácil

3. **❌ Data prevista de repasse errada**
   - Problema: Coluna 1 da tabela superior sendo alterada incorretamente
   - Correto: Manter sempre **dia 10** do mês

4. **❌ Folha de pagamento sem carimbo**
   - Problema: Folha encaminhada sem identificação do Termo de Colaboração
   - Correto: Carimbar com "Termo de Colaboração nº 12 / Aditivo 12/2026 — Recurso Municipal"

5. **❌ Recursos humanos com valor errado no RP-10**
   - Problema: Lançar salário líquido em vez do salário bruto
   - Correto: Usar o **total bruto** da folha de pagamento

6. **❌ Receita de aplicação financeira calculada errada**
   - Problema: Usar rendimento bruto sem descontar IOF e IR
   - Correto: Rendimento - IOF - IR = valor a lançar no campo (C)

---

## MODULARIZATION INSTRUCTIONS FOR THE AGENT

Build the portal in clearly separated JS modules/objects:

```javascript
// Module structure:
const App = {
  state: { currentSection, checklistItems, calculatorValues },
  router: { navigate(hash), highlightActive() },
  calculator: { compute(), copyToClipboard(), validate() },
  checklist: { toggle(id), getProgress(), reset() },
  theme: { toggle(), apply() },
  ui: { renderSidebar(), renderBadges(), initLucide() }
}
```

This allows future sections and features to be added without rewriting existing code.

**Future-proofing placeholders** to include:
- Section for portal links/certificates (currently empty, labeled "A configurar")
- Ability to add more expense categories dynamically
- Space for future document upload instructions

---

## VISUAL COMPONENTS TO IMPLEMENT

1. **Step cards** — numbered, with icon, title, instruction body, and optional alert
2. **Alert boxes** — warning (amber), info (teal), success (green), error (red)
3. **Interactive calculator panel** — input fields, auto-calculated results, copy button
4. **Checklist with progress bar** — animated fill, item count, reset button
5. **Sidebar with status badges** — Pendente (gray), Em andamento (amber), Concluído (green)
6. **Data table explainer** — annotated table showing what goes in each field
7. **Validation indicator** — green ✅ / red ❌ for the (K) == Rende Fácil check

---

## IMPORTANT CONTEXT

- Organization: **Cooperposse — Cooperativa dos Coletores de Material Reciclável**
- Municipality: **Santo Antônio de Posse, SP**
- Instrument: **Termo de Colaboração / Aditivo Contratual nº 12/2026**
  - Start: 01/01/2026 | End: 15/09/2026 | Value: R$ 228.000,00
- Resource origin: **Municipal**
- Responsible: **Maria Luiza de Paula** — Presidente
- Accountability submissions go to: **Amanda** (Secretaria Municipal de Desenvolvimento Social)
- Original payroll goes to: **Lumen**
- Applicable norm: **Instrução Normativa TCESP nº 01/2024**
- Portal for transparency uploads: **Portal de Transparência da Cooperposse** (URL to be added)

---

## OUTPUT

Deliver a single file: `portal-cooperposse.html`
Complete, production-ready, no placeholders in functional areas, fully working calculator and checklist, light/dark mode, responsive.

