# finAI 🚀 | Agente Financeiro Inteligente & Proativo

> Desafio de Projeto realizado para o Lab **"BIA do Futuro"** da **DigitalInnovationOne (DIO)** em parceria com o **Bradesco**.

O **finAI** é um assistente virtual e agente financeiro inteligente que utiliza Inteligência Artificial Generativa para transformar a relação dos clientes com suas finanças pessoais. Diferente dos chatbots tradicionais e reativos, o finAI atua de forma **proativa, consultiva e hiper-personalizada**, antecipando necessidades, mitigando riscos de endividamento e sugerindo as melhores alocações de investimentos com base no perfil individual.

---

## 📋 Índice

- [Visão Geral e Caso de Uso](#-visão-geral-e-caso-de-uso)
- [Funcionalidades Principais](#-funcionalidades-principais)
- [Persona e Tom de Voz](#-persona-e-tom-de-voz)
- [Arquitetura e Fluxo de Dados](#-arquitetura-e-fluxo-de-dados)
- [Segurança e Diretrizes Anti-Alucinação](#-segurança-e-diretrizes-anti-alucinação)
- [Estrutura da Base de Conhecimento](#-estrutura-da-base-de-conhecimento)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Como Executar o Projeto](#-como-executar-o-projeto)
- [Estrutura do Repositório](#-estrutura-do-repositório)

---

## 💡 Visão Geral e Caso de Uso

O principal problema resolvido pelo **finAI** é a falta de planejamento financeiro e a dificuldade na tomada de decisões de investimento por parte de clientes de varejo e alta renda. O agente cruza dados históricos de consumo com o perfil de investidor para:

1. **Prevenir o superendividamento:** Identificando padrões atípicos de gastos e emitindo alertas preditivos.
2. **Potencializar a capacidade de poupança:** Recomendando aportes automáticos sempre que houver sobra de caixa estimada para o mês.
3. ** Democratizar a consultoria de investimentos:** Traduzindo termos técnicos e recomendando portfólios adequados sem jargões complexos.

---

## ✨ Funcionalidades Principais

* **Análise Preditiva de Saldo:** Avalia a recorrência de despesas e avisa o cliente se o saldo projetado para o fim do mês for insuficiente.
* **Recomendação de Portfólio sob Medida:** Cruza o perfil de investidor do cliente com o catálogo de produtos disponíveis na instituição financeira.
* **Alocação Inteligente de Sobras:** Identifica quando o cliente gasta menos que a média e sugere a transferência do saldo remanescente para um produto de liquidez diária.
* **Conciliação e Explicação de Gastos:** Permite ao usuário perguntar coisas como: *"Por que minha fatura este mês veio R$ 300 mais alta que o normal?"* e obter um sumário analítico imediato.

---

## 🎭 Persona e Tom de Voz

O finAI adota a persona de um **Especialista em Finanças Pessoais de Confiança**.

* **Tom de Voz:** * **Empático e Proativo:** Sempre oferece uma solução ou um próximo passo prático, em vez de apenas apontar um problema.
  * **Claro e Didático:** Evita o "financês" corporativo, explicando conceitos como CDI, IPCA e Liquidez de forma simples e acessível.
  * **Seguro e Confiável:** Não faz promessas de ganhos irreais (ex: "rendimento garantido acima do mercado") e mantém foco rigoroso no gerenciamento de riscos.

---

## 🏗️ Arquitetura e Fluxo de Dados

O agente funciona utilizando a abordagem de **RAG (Retrieval-Augmented Generation)** combinada com um **System Prompt estruturado** (guardrails de comportamento).
