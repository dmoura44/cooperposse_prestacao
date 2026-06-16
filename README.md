# Portal de Prestação de Contas - Cooperposse

Este projeto consiste em uma aplicação web interativa desenvolvida para otimizar, padronizar e controlar o processo mensal de prestação de contas da Cooperposse (Cooperativa dos Coletores de Material Reciclável de Santo Antônio de Posse) junto à administração pública.

A ferramenta foi idealizada para substituir processos manuais suscetíveis a erros, oferecendo um guia visual, calculadoras automatizadas e checklists de conferência integrados em uma única interface.

## Funcionalidades Principais

* **Calculadora RP-10 Integrada:** O sistema possui uma calculadora financeira desenvolvida sob medida para a estrutura do documento RP-10. Ela consolida automaticamente saldos anteriores, repasses, rendimentos de aplicações financeiras (já abatendo deduções de IR e IOF) e despesas categorizadas (como recursos humanos, locação, combustível e despesas bancárias).
* **Validação de Conciliação Bancária:** Para evitar falhas humanas no preenchimento, a aplicação cruza os resultados das operações financeiras e valida se o saldo não aplicado informado (Campo K) bate exatamente com o extrato bruto bancário, alertando o usuário em tempo real sobre qualquer divergência de valores.
* **Acompanhamento de Progresso (Status Tracking):** O processo de prestação de contas foi dividido em etapas de ciclo de vida (Pendente, Em andamento, Concluído). O sistema acompanha o andamento de cada seção por meio de um indicador de progresso visual (Progress Ring), oferecendo uma métrica clara de completude do trabalho.
* **Gestão de Documentos e Certidões:** Centraliza os links para emissão e verificação das certidões obrigatórias de regularidade fiscal e trabalhista da cooperativa.
* **Interface Dinâmica:** A aplicação é construída com design responsivo (mobile-friendly), controle de tema (Claro/Escuro) e painéis expansíveis, permitindo que a visualização foque apenas na tarefa que está sendo executada no momento.

## Tecnologias Utilizadas

O projeto foi construído priorizando a estabilidade e a facilidade de manutenção a longo prazo, sem depender de pesados frameworks externos:

* **HTML5 e CSS3 Vanilla:** Estruturação semântica e estilização completa utilizando CSS puro com variáveis globais.
* **JavaScript (ES6+):** Toda a lógica de negócios, cálculos financeiros com formatação de moeda local (BRL), manipulação do DOM e controle de estado gerenciados por scripts nativos.
* **Lucide Icons:** Utilização de biblioteca leve para os vetores da interface.

## Motivação e Impacto

O principal objetivo deste sistema é mitigar a devolução de documentações por erros burocráticos ou de cálculo, que frequentemente atrasam o repasse de recursos essenciais para o funcionamento da cooperativa. A ferramenta atua tanto como um checklist rigoroso das exigências normativas quanto como um ambiente de trabalho que calcula, formata e organiza os dados necessários antes de serem transcritos para os ofícios oficiais.