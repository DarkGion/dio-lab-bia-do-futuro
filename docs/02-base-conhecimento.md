# 🧠 Base de Conhecimento: FinAI

## 📊 Dados Utilizados

O FinAI utiliza uma estrutura de dados focada no histórico financeiro real do usuário e nas projeções das metas desejadas. Os dados de entrada são estruturados da seguinte forma:

| Arquivo / Tabela | Formato | Utilização no Agente |
| :--- | :--- | :--- |
| `usuarios.json` | JSON / Banco | Armazena o perfil básico e a renda fixa mensal líquida do usuário. |
| `historico_transacoes.csv` | CSV / Banco | Registra o fluxo de caixa (entradas e saídas) para cálculo de médias de gastos e identificação de gargalos. |
| `custos_ocultos_veiculos.json`| JSON | Base de conhecimento estática com estimativas de custos invisíveis (IPVA, seguro, manutenção média, combustível) por categoria de veículo. |
| `metas_planejamento.json` | JSON / Banco | Armazena os objetivos ativos do usuário (ex: financiamento do carro) e os prazos estipulados. |

---

## 🔧 Adaptações nos Dados

> **Nota de Desenvolvimento:** Os dados iniciais de transações foram expandidos para cobrir um histórico mínimo de 3 a 6 meses. Essa adaptação é obrigatória para que a LLM consiga calcular médias de consumo realistas e identificar de forma consistente se o usuário possui margem financeira confortável ou se opera no limite antes de assumir uma nova dívida.

---

## ⚙️ Estratégia de Integração

### Como os dados são carregados?
Os dados de perfil do usuário, médias de gastos extraídas do CSV e os parâmetros de custos ocultos do veículo simulado são carregados dinamicamente via API no início de cada sessão de simulação e injetados diretamente no contexto da conversa.

### Como os dados são usados no prompt?
Os dados históricos e as regras de comportamento não vão inteiramente no *System Prompt* para evitar desperdício de tokens. A integração funciona de forma híbrida:
1. O *System Prompt* dita a persona (realista, empática e encorajadora) e as limitações do FinAI.
2. Os dados de média de gastos e renda do usuário são inseridos como **Contexto Dinâmico** na mensagem de sistema toda vez que uma simulação é disparada.
3. Os cálculos matemáticos pesados passam por uma camada de validação em código antes de a resposta de texto ser gerada pela LLM.

---

## 📝 Exemplo de Contexto Montado

Abaixo está o exemplo de como a camada de backend estrutura os dados consolidados do usuário para enviar à LLM realizar o diagnóstico:

```yaml
[CONTEXTO ENVIADO À IA]
DADOS DO USUÁRIO:
- Nome: Giovanni
- Renda Mensal Líquida: R$ 6.500,00

MÉDIAS DE GASTOS ATUAIS (ÚLTIMOS 3 MESES):
- Gastos Essenciais (Moradia, Contas): R$ 3.100,00
- Gastos Supérfluos/Lazer (Delivery, Assinaturas): R$ 1.400,00
- Reserva/Investimentos atuais: R$ 500,00
- Margem Livre Atual: R$ 1.500,00

META SOLICITADA PARA SIMULAÇÃO:
- Objetivo: Financiamento de Carro UP (Seminovo)
- Valor da Parcela Informada: R$ 1.200,00 / mês
- Prazo: 48 meses

PARÂMETROS DE CUSTOS OCULTOS AGREGADOS (BASE FINAI):
- Estimativa Seguro + IPVA proporcional: R$ 250,00 / mês
- Estimativa Combustível + Manutenção básica: R$ 400,00 / mês
- Custo Total Real do Objetivo: R$ 1.850,00 / mês

DIRETRIZ DE DIAGNÓSTICO DA IA:
O custo total real (R$ 1.850) excede a margem livre atual (R$ 1.500). 
O agente deve alertar que o plano gerará um sufoco financeiro de R$ 350 negativos, 
sendo necessário cortar lazer ou aumentar o prazo/entrada. Seja realista, mas encorajador.
