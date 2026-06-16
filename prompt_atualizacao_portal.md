## PROMPT DE ATUALIZAÇÃO E CORREÇÃO — PORTAL COOPERPOSSE

O portal já foi construído. Agora implemente as seguintes correções e adições no arquivo `portal-cooperposse.html` existente:

---

## 1. FORMATAÇÃO MONETÁRIA AUTOMÁTICA (PRIORITY FIX)

Todos os campos de input de valor monetário do portal (calculadora RP-10 e qualquer campo de R$) devem ter **formatação automática de moeda brasileira** enquanto o usuário digita.

**Comportamento esperado:**
- O usuário digita apenas os dígitos (sem pontos, vírgulas ou R$)
- O campo formata automaticamente em tempo real: `12012,55` → `R$ 12.012,55`
- Separador de milhar: ponto (.)
- Separador decimal: vírgula (,)
- Sempre 2 casas decimais
- O campo exibe o prefixo `R$` visualmente mas o valor interno para cálculo é sempre um float

**Implementação sugerida:**
```javascript
function formatCurrency(input) {
  // Remove tudo que não é dígito
  let val = input.value.replace(/\D/g, '');
  // Converte para centavos e depois para reais
  let num = (parseInt(val || '0') / 100).toFixed(2);
  // Formata com separadores BR
  input.value = new Intl.NumberFormat('pt-BR', {
    minimumFractionDigits: 2,
    maximumFractionDigits: 2
  }).format(num);
}

// Para extrair o valor numérico de um campo formatado:
function parseCurrency(input) {
  return parseFloat(
    input.value.replace(/\./g, '').replace(',', '.') || '0'
  );
}
```

Aplique esse listener `oninput` em TODOS os campos de valor monetário do portal. O cálculo automático dos totais deve usar `parseCurrency()` internamente.

---

## 2. SEÇÃO DE CERTIDÕES — NOVA SEÇÃO NO SIDEBAR

Adicione uma nova seção no sidebar chamada **"📜 Certidões"** entre "Preparação da Pasta" e "Ofício de Encaminhamento".

### Conteúdo da seção:

**Título:** Certidões e Documentos Cadastrais  
**Subtítulo:** CNPJ: 08706538000128

**Intro text:** "Estas certidões devem ser renovadas periodicamente e mantidas atualizadas no sistema. Verifique a validade antes de cada prestação de contas."

**Tabela interativa de certidões** com as seguintes colunas:
- Nº | Certidão | Link de emissão | Data de emissão | Data de validade | Status

**Linhas da tabela (pré-preenchidas):**

| Nº | Certidão | Link |
|---|---|---|
| 1 | Prova de inscrição no CNPJ — Cadastro Nacional da Pessoa Jurídica | https://solucoes.receita.fazenda.gov.br/Servicos/cnpjreva/ |
| 2 | Cadastro de Contribuintes Municipal | http://servicos.pmsaposse.sp.gov.br:8080/servicosweb/home.jsf — (acesso: mobiliário 4049 / senha: 3gjwisqxg2xcxxu) |
| 3 | Certidão Negativa de Débitos Federais e Dívida Ativa da União (CND Federal) — SRF | https://servicos.receitafederal.gov.br/servico/certidoes/#/home |
| 4 | Certidão Negativa de Débitos Estaduais — SP | https://www10.fazenda.sp.gov.br/CertidaoNegativaDeb/Pages/EmissaoCertidaoNegativa.aspx |
| 5 | Certidão Negativa de Débitos Tributários Municipais e Dívida Ativa Municipal | http://servicos.pmsaposse.sp.gov.br:8080/servicosweb/home.jsf |
| 6 | Certificado de Regularidade FGTS (CRF) — Caixa Econômica Federal | https://consulta-crf.caixa.gov.br/consultacrf/pages/consultaEmpregador.jsf |
| 7 | Certidão Negativa de Débitos Trabalhistas (CNDT) — TST | https://cndt-certidao.tst.jus.br/inicio.faces |
| 8 | Atualização Cadastral CADTCESP | https://www.tce.sp.gov.br/cadtcesp/#!/pessoa/cadastro |

**Funcionalidades da tabela:**
- Botão de link "🔗 Acessar" ao lado de cada certidão — abre em nova aba (`target="_blank"`)
- Campos editáveis inline para **Data de emissão** e **Data de validade** (input type="date")
- **Status visual automático** baseado na data de validade:
  - 🟢 Verde: válida (mais de 30 dias para vencer)
  - 🟡 Amarelo: vencendo em breve (menos de 30 dias)
  - 🔴 Vermelho: vencida ou sem data informada
- Observação especial para item 2 (Cadastro Municipal): exibir nota discreta com as credenciais de acesso
- Nota de rodapé: "Modelos de declarações para prestação de contas disponíveis em: https://www.tce.sp.gov.br/legislacao/instrucao/instrucoes-012020 (verificar se há versão 2024)"

---

## 3. CALCULADORA RP-10 — CAMPO RECURSOS HUMANOS DETALHADO

Na seção RP-10, na área **"DESPESAS — Tabela de Origem Municipal"**, substitua o campo único de "Recursos humanos (folha de pagamento — salário bruto total)" por um **sistema de lançamento de pagamentos individuais**.

**Comportamento:**
- Um painel expansível chamado "Recursos Humanos — Detalhamento da Folha"
- Ao expandir, mostra uma lista de linhas de pagamento individual
- Cada linha tem:
  - Campo: Nome/Descrição do colaborador (ex: "Maria - Coletora", "João - Motorista")
  - Campo: Valor bruto (R$) — com formatação automática
  - Botão: ❌ remover linha
- Botão: "+ Adicionar colaborador" — adiciona nova linha
- **Total calculado automaticamente** à medida que os valores são adicionados/alterados
- O total alimenta o campo "Recursos humanos" na calculadora principal
- O painel pode ser minimizado/expandido (toggle com seta)
- Estilo visual: fundo levemente diferenciado, bordas sutis, compacto

**Exemplo visual do painel expandido:**
```
▼ Recursos Humanos — Detalhamento da Folha

  Nome / Descrição          Valor Bruto
  [Maria - Coletora    ]    R$ [________]  [❌]
  [João - Motorista    ]    R$ [________]  [❌]
  [Carlos - Triagem    ]    R$ [________]  [❌]
  
  [+ Adicionar colaborador]
  
  ══════════════════════════════════════
  TOTAL RECURSOS HUMANOS:     R$ 12.012,55
```

---

## 4. INDICADOR DE PROGRESSO GLOBAL — BARRA ANIMADA

Adicione um **indicador de progresso circular** fixo no canto inferior direito da tela (acima do botão de scroll).

**Especificações visuais:**
- Círculo SVG animado (stroke-dasharray/dashoffset) com porcentagem no centro
- Diâmetro: 56px, stroke-width: 5px
- Cor da trilha: superfície neutra
- Cor de preenchimento: teal primário (#0a6b72 light / #4f9ea8 dark)
- Número no centro: porcentagem inteira (ex: "47%")
- Tooltip ao hover: "X de Y itens do checklist concluídos"
- Ao atingir 100%: anel fica verde + pequena animação de pulso
- Calcula baseado nos itens do Checklist Geral

**Posição:** `position: fixed; bottom: 80px; right: 20px; z-index: 900`

---

## 5. BOTÃO DE SCROLL TO TOP — ANIMADO E BONITO

Adicione um botão flutuante de "voltar ao topo" no canto inferior direito.

**Especificações:**
- Aparece apenas quando o usuário rola mais de 300px para baixo (dentro do conteúdo principal)
- Animação de entrada: fade + slide-up suave (200ms)
- Ícone: seta para cima (Lucide `chevrons-up`)
- Formato: círculo 44px, cor primária teal com hover mais escuro
- Ao clicar: scroll suave até o topo do conteúdo principal (não da página toda — do `<main>`)
- Tooltip: "Voltar ao topo"
- `position: fixed; bottom: 24px; right: 20px; z-index: 900`

O indicador circular de progresso fica em `bottom: 80px` e o botão scroll fica em `bottom: 24px`, ambos alinhados à direita.

---

## 6. TABELA GRÁFICA EXPLICATIVA DO RP-10

Na seção RP-10, antes da calculadora, adicione uma **visualização gráfica/didática** da estrutura do formulário RP-10 real, usando HTML/CSS — não uma imagem estática, mas uma representação visual dos campos.

Deve ser uma tabela estilizada que representa **visualmente** o formulário, com:
- Cores de fundo diferentes para cada bloco (recursos x despesas x saldo)
- Setas ou indicadores visuais mostrando de onde vem cada valor (ex: "← do extrato Rende Fácil", "← do extrato bancário")
- Campos destacados que precisam de atenção especial (ex: campo (K) em verde, campo data em azul)
- Legenda colorida abaixo da tabela
- Pode usar `position: relative` + pseudo-elementos ou badges de tooltip para as dicas

**Tabela 1 — Demonstrativo dos Recursos Disponíveis:**

Mostrar visualmente as linhas A, B, C, D, E, F, G com anotações:
- (A): badge "Rende Fácil — saldo bruto anterior"
- (B): badge "Extrato bancário — crédito do repasse"  
- (C): badge "Rende Fácil — rendimento - IOF - IR"
- (E): badge "Calculado: A+B+C+D" em verde
- (G): badge "Calculado: E+F" em verde

**Tabela 2 — Demonstrativo das Despesas:**

Mostrar visualmente as categorias com badges de fonte:
- Recursos humanos: badge "Folha de pagamento — salário bruto"
- Locação: badge "R$ 2.500,00 fixo"
- Combustível: badge "Comprovantes/extrato"
- Desp. bancárias: badge "Extrato — tarifas PIX/TED"

**Tabela 3 — Demonstrativo do Saldo Financeiro:**

Mostrar G, J, K, L, M com destaque especial em (K):
- (K): Fundo verde claro + ícone de verificação + texto "Deve coincidir com o saldo bruto Rende Fácil"

---

## 7. CORREÇÕES GERAIS DE BUGS

- Revisar todos os cálculos automáticos da calculadora RP-10 e garantir que todos os campos interdependentes atualizam em cascata ao alterar qualquer input
- Garantir que o botão "Copiar resumo para colar no Word" gera texto formatado correto com todos os valores
- Confirmar que a validação visual do campo (K) vs. saldo Rende Fácil funciona corretamente (verde/vermelho)
- Testar todos os campos de receita de aplicação financeira: Rendimento - IOF - IR = campo (C)
- Garantir que adicionar/remover repasses na tabela superior recalcula (B) e todos os campos dependentes

---

## OBSERVAÇÕES FINAIS

- Manter toda a estrutura modular existente do App object
- Não remover nenhuma seção existente — apenas adicionar e corrigir
- Manter compatibilidade com light/dark mode em todos os novos elementos
- Todos os novos componentes devem ser responsivos (375px+)
- Manter o padrão visual e tipográfico do portal existente

