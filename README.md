# Previsão de Crescimento e Mensuração do Efeito de Substituição do Pix sobre os Meios de Pagamento Concorrentes no Brasil

> **Projeto Aplicado IV — Curso de Ciência de Dados**  
> **Universidade Presbiteriana Mackenzie** (São Paulo, 2026)

---

## 👥 Integrantes da Equipe

- **Cainã Fernandes Guimarães da Silva**
- **Gabriel de Oliveira Meloni**
- **Humberto Guttau Bravo**
- **Jimmy Paiva Gomes**

---

## 📌 Visão Geral do Projeto

Este projeto insere-se na área de **Ciência de Dados aplicada a séries temporais financeiras**, com foco na modelagem estatística da adoção tecnológica do **Pix** (sistema de pagamentos instantâneos do Banco Central do Brasil) e na quantificação de seus efeitos de substituição e complementaridade em relação a outros instrumentos de pagamento concorrentes (*boleto bancário, cheque, TED/DOC e cartões de crédito e débito*).

### 🎯 Problema de Pesquisa
> **Em que medida o Pix efetivamente substituiu cada um dos meios de pagamento concorrentes, e em que medida ele os complementou por meio da expansão da base de usuários bancarizados?**

---

## 💡 Motivação e Contexto

1. **Digitalização e Disputa Internacional:**
   - Em 2025/2026, o Escritório do Representante Comercial dos EUA (USTR) iniciou investigações (Seção 301 do *Trade Act*) questionando a atuação do Banco Central do Brasil como operador e regulador do Pix, alegando prejuízos à competitividade de empresas norte-americanas de cartões e pagamentos.
2. **Substituição vs. Bancarização (Complementaridade):**
   - Embora o Pix tenha substituído diretamente transferências tradicionais (TED/DOC, cheques e boletos), dados da Abecs apontam que o setor de cartões movimentou R$ 4,5 trilhões em 2025 (+10,1% em relação a 2024, com alta de 14,5% em cartões de crédito).
   - O Pix atuou como um vetor de inclusão financeira, ampliando o acesso a contas digitais e injetando novos usuários no ecossistema de pagamentos.
3. **Achados Preliminares (Ticket Médio):**
   - Análise da série temporal (nov/2020 a jul/2026) mostra a queda do ticket médio por transação Pix de **~R$ 880 (nov/2020)** para **~R$ 400 (2023)**, estabilizando-se em um platô de **R$ 380 a R$ 450**, evidenciando a incorporação de transações do dia a dia e novos casos de uso populares.

---

## 🎯 Objetivos

- [x] **a) Previsão do Pix:** Modelar a trajetória de adoção em volume e quantidade via ARIMA/SARIMA.
  - *Status:* Modelo base `SARIMA(0,1,0)(0,1,1,12)` ajustado e validado.
- [ ] **b) Cenários Contrafactuais:** Construir modelos `ARIMAX` com variável de intervenção para estimar a trajetória projetada dos concorrentes (sem Pix) vs. observada.
- [ ] **c) Validação Estatística:** Aplicar testes de **Causalidade de Granger** e detecção de **Pontos de Mudança Estrutural** (*change point detection*).

---

## 📊 Descrição das Bases de Dados

As fontes são primárias, públicas e consumidas via **API OData (Plataforma Olinda)** do Banco Central do Brasil:

| Endpoint / Fonte | Granularidade / Período | Observações | Status |
| :--- | :--- | :--- | :---: |
| **`EstatisticasTransacoesPix`** | Mensal (Nov/2020 – Jul/2026) | 69 obs. Microdados por 9 variáveis categóricas agregadas por mês. | 🟢 Coletado |
| **`MeiosdePagamentosMensalDA`** | Mensal (Nov/2020 – Jul/2026) | 69 obs. Volumes/valores de Pix, TED, Cheque, Boleto e DOC (DOC zerado após descontinuação). | 🟢 Coletado |
| **`Quantidadeetransacoesdecartoes`** | Trimestral (4Q20 – 1Q26) | 22 obs. Estoque e transações de cartões de crédito e débito. | 🟢 Coletado |
| **`MeiosdePagamentosTrimestralDA`** | Trimestral | Falha no servidor do BCB (Erro 500 para todos os 22 trimestres). | 🟡 Pendente (Fallback: Abecs) |
