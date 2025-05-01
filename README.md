# Evolução de Pagamentos PIX – Telefonia
![Painel fundo Dashboard Pix](https://github.com/user-attachments/assets/ee201a7c-40f4-4794-b557-49f358524ac7)


---
[![Dados Fictícios](https://img.shields.io/badge/Dados-Fict%C3%ADcios-red)](#)

> ⚠️ **Disclaimer**  
> Os **dados apresentados são fictícios** e foram alterados para preservar confidencialidade.  
> A **estrutura**, **fluxo de ETL**, **scraping** e **dashboard**, porém, refletem fielmente o processo real.


## 🎯 Situação  
A TIM Brasil precisava de um painel analítico capaz de monitorar e comparar, em tempo real e de forma histórica, a evolução dos recebimentos via PIX. Os dados estavam fragmentados no SAP, em portais internos e planilhas, sem uma visão única e padronizada para suportar decisões de pricing, operações e relacionamento com bancos e segmentos de clientes.

---

## 🚩 Tarefa  
- **Objetivo principal**  
  - Demonstrar a evolução diária dos pagamentos via PIX ao longo de um mês e comparar indicadores-chave entre meses consecutivos.

- **Subtarefas**  
  1. Identificar os principais bancos arrecadadores e a penetração por segmento (Controle, Corporativo, Pós-Pago, Ultra Fibra).  
  2. Construir métricas de performance mensal (variação absoluta e percentual).  
  3. Avaliar eficiência de desbloqueio e tempo de liquidação/baixa de pagamentos.  
  4. Entregar um dashboard interativo para os tomadores de decisão, no qual é atualizado diariamente com novas informações.

---

## 🔧 Ações Executadas  

1. **Extração & ETL**  
   - Conexão ao SAP para extração bruta das transações PIX.  
   - Carregamento e transformação no SAS Enterprise via SQL(Dados atualizados até 29 de Abr/25). Nessa etapa os dados são salvos em tabelas que todas a empresa pode utilizar.  
   - Exportação dos dados tratados para o Excel. É feita essa exportação, pois reduz o tempo de processamento para salvamento posterior no Access.

2. **Web Scraping (Python + Selenium)**  
   - Coleta de métricas de Desbloqueio e Tempos de Baixa de Pagamento em portais internos(Splunk).  
   > ⚠️ *Observação:* O uso de Web Scraping foi necessário pois o sistema consultado **não disponibiliza API** para extração automatizada dos dados.
  
   - Exportação intermediária para CSV (`Nomenclatura`, `Valor`, `Fluxo`, `Período`, `Segmento`).

3. **Persistência**  
   - Consolidação de todas as tabelas em um banco de dados Access (`.accdb`) para versionamento e consulta unificada.

4. **Desenvolvimento do Dashboard**  
   - **Página 1:** Evolução diária (timeline) + principais arrecadadores × segmentos.  
   - **Página 2:** Evolução mensal com variações (p.p. e %) e penetração por segmento.  
   - **Página 3:** Comparativo mês atual vs. anterior; performance por banco; % PIX diário.  
   - **Página 4:** KPIs de desbloqueio (eficiência de fluxo, % sucesso/erro/tramitação).  
   - **Página 5:** Distribuição de tempo de baixa de pagamento (de até 10 s a >1 h).

5. **Validação & Entrega**  
   - Revisão de consistência e usabilidade de filtros(Lembrando que o projeto é atualizado diariamente).  
   - Publicação no serviço Interno do Cliente, apresentação em reunião e envio por e-mail aos envolvidos.
## 🧭 Arquitetura do Projeto – Pipeline de Dados do Dashboard PIX
![Arquitetura Dashboard Pix](https://github.com/user-attachments/assets/697a0139-e119-4ab6-bf48-adf606bdef18)

> ⚠️ **Importante:**  
> Esta imagem representa a **arquitetura real do pipeline de dados** desenvolvido no projeto.  
> Apesar de os **dados utilizados serem fictícios** (anonimizados ou simulados para fins de apresentação), o fluxo de **extração, tratamento, armazenamento e visualização** reflete com fidelidade a solução aplicada em um ambiente corporativo real.
---

## 🚀 Resultados & Insights  

- **Estabilidade & Crescimento**  
  - Penetração média diária de PIX estabilizada em ~**61,8%** (abr/2025).  
  - Março/2025 teve **+15,1%** de faturas pagas a mais que Fevereiro/2025.

- **Principais Arrecadadores**  
  - **Nubank (23%)**, **CEF (13%)**, **Itaú (11%)** concentram quase metade do volume.  
  - “Outros” bancos/fintechs somam **8%**, indicando espaço para novas parcerias.

- **Adoção por Segmento**  
  - **Controle:** 70,3% de penetração (líder).  
  - **Corporativo:** 29,7% (crescimento de +4,6 p.p. de jul/2024 a mar/2025).  
  - **Ultra Fibra:** maior aumento relativo (+8,6 p.p. no período).

- **Eficiência de Desbloqueio**  
  - **99,5%** de sucesso no fluxo de desbloqueio, tempo médio de **0,1 min** (6 s).  
  - No segmento Controle (24 h), **74,3%** das requisições eram elegíveis sem precisar desbloquear.

- **Tempo de Baixa de Pagamento**  
  - **>284 mil** pagamentos reconhecidos em até **10 s**; < 0,5% > 1 min sem reprocessamento.  
  - Com reprocessamento, tempo médio sobe para **1 min 14 s** — impacto operacional gerenciável.

> **Conclusão:**  
> O dashboard tornou-se ferramenta estratégica para:  
> - Monitorar quedas de performance (ex.: –3,8% em fev/2025).  
> - Priorizar ajustes técnicos em fluxo de baixas.  
> - Negociar condições com bancos de menor participação.  
> - Avaliar a evolução dos pagamentos ao longo do mês.  
> - Acompanhar o crescimento da distribuição percentual do método Pix ao longo do tempo.

📊 **Acesse o dashboard completo clicando na imagem abaixo:**

[![Pagina01 Dashboard Pix](https://github.com/user-attachments/assets/80f805f6-19f9-4a0f-9dd0-e431f1e47bb7)](https://app.powerbi.com/view?r=eyJrIjoiNjM2MDQwMjAtYThlMi00YzI2LTgxNDctMmQwNGM2OGU1NzIyIiwidCI6IjQzZDMwZGIxLThkNGItNDA5Yi04ZWYzLWVlODRmZDRjZGIzOSJ9)


