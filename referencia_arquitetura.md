# Referência de Arquitetura — Portal Cooperposse

Este documento serve como referência técnica para agentes de IA e desenvolvedores que atuarão no projeto Portal Cooperposse.

## 1. Visão Geral do Projeto
O Portal Cooperposse é uma aplicação web single-page (SPA) estática (HTML/CSS/JS) para auxiliar na prestação de contas mensal da OSC Cooperposse. 
A aplicação não utiliza frameworks (React, Vue, etc.), sendo construída com Vanilla JavaScript para máxima portabilidade e simplicidade. Todo o estado é gerenciado em memória (sem `localStorage` ou banco de dados).

## 2. Tecnologias Utilizadas
- **HTML5**: Estrutura semântica do portal.
- **CSS3 (Vanilla)**: Design system customizado usando CSS Variables (Custom Properties) para temas Light/Dark. O CSS foi extraído para o arquivo `styles.css`.
- **JavaScript (Vanilla)**: Lógica de negócio, roteamento e manipulação do DOM encapsulados no objeto global `App`.
- **Lucide Icons**: Biblioteca de ícones carregada via CDN.
- **Google Fonts**: Fontes 'DM Sans' (corpo) e 'Fraunces' (títulos).

## 3. Estrutura de Arquivos
- `portal-cooperposse.html`: Arquivo principal contendo a estrutura DOM e a lógica JavaScript (tag `<script>`).
- `styles.css`: Arquivo de estilos com todo o design system.
- `Coperposse (2).png`: Logo da instituição.

## 4. Arquitetura JavaScript (Objeto `App`)
A lógica da aplicação está centralizada no objeto `App`, dividido nos seguintes módulos:

### 4.1. `App.state`
Armazena o estado volátil da aplicação:
- `currentSection`: Seção atualmente visível.
- `sectionStatuses`: Status de cada seção (pendente, andamento, concluido).
- `checklistItems`: Estado (booleano) de cada item do checklist.
- `calculatorValues`: Valores numéricos em tempo real da calculadora RP-10.
- `rhExpanded`: Estado do painel expansível de Recursos Humanos.

### 4.2. `App.router`
Gerencia a navegação via âncoras na URL (`hash-based routing`). Exibe apenas a seção (`<section>`) correspondente ao hash atual, ocultando as demais via CSS.

### 4.3. `App.theme`
Controla a alternância entre os temas claro (`data-theme="light"`) e escuro (`data-theme="dark"`).

### 4.4. `App.calculator`
Contém a lógica de negócios da prestação de contas (RP-10 e Conciliação Bancária).
- Função principal: `compute()`. Lê todos os inputs monetários, aplica `parseCurrency()`, realiza os cálculos (A+B+C+D, H+I, etc.) e atualiza a interface.
- Gera o resumo formatado para cópia.

### 4.5. `App.checklist`
Gerencia a lógica do checklist geral e calcula a porcentagem de conclusão, atualizando o indicador circular SVG. Integra-se ao `App.ui` para atualizar automaticamente os status das seções de navegação conforme o progresso.

### 4.6. `App.ui`
Responsável pela renderização dinâmica de elementos:
- `renderSidebar()`: Constrói o menu lateral.
- `renderCertidoes()`: Renderiza a central de links de certidões.
- Controle de toasts, sidebar mobile e scroll-to-top.

## 5. Padrões Importantes Implementados nas Atualizações Recentes
- **Formatação Monetária**: Campos com a classe `.money-input` formatam valores em tempo real para o padrão BRL (R$ 0,00) via delegação de eventos no `document`.
- **Integração de Seções**: A seção de Conciliação Bancária foi integrada fisicamente à seção RP-10 para manter todo o fluxo de cálculo em um único contexto.
- **Central de Links**: A área de certidões atua estritamente como um repositório de acessos rápidos, sem armazenamento de datas.
- **Lançamento Rápido de RH**: O painel de Recursos Humanos foca em agilidade, permitindo adicionar novos valores pressionando a tecla `Enter`.
- **Orquestração de Progresso**: O progresso do checklist influencia o status visual das abas na barra lateral de navegação.

## 6. CSS e Design System
O `styles.css` utiliza variáveis de raiz (`:root`) para definir tokens de design (cores, espaçamentos, sombras).
- O tema base (`[data-theme="light"]`) e o tema noturno (`[data-theme="dark"]`) redefinem variáveis semânticas como `--color-bg`, `--color-text`, `--color-primary`.
- O contraste da sidebar foi ajustado para garantir legibilidade da logo original, utilizando um fundo contrastante com as cores institucionais (fundo branco ou container adaptado).
