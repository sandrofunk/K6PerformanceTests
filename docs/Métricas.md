# 📊 Métricas em Testes de Performance

As métricas são os **indicadores objetivos** usados para medir o desempenho de um sistema sob diferentes condições de carga.  
Interpretar corretamente essas métricas é essencial para **identificar gargalos**, **avaliar melhorias** e **garantir o cumprimento de SLAs (Service Level Agreements)**.

---

## 🕓 1. Tempo de Resposta (Response Time)

**Definição:**  
Tempo total entre o envio de uma requisição e o recebimento completo da resposta.

**Tipos de medição:**
- **Average (média):** média de todos os tempos de resposta.  
- **Median (mediana):** valor central; menos afetado por outliers.  
- **Percentis (p90, p95, p99):** indicam a performance para a maioria dos usuários.  
  - Exemplo: p95 = 1,2s → 95% das requisições responderam em até 1,2 segundos.

**Boas práticas:**
- Use **percentis** em relatórios (média pode mascarar problemas).  
- Monitore também o **tempo de resposta máximo** (worst-case).

---

## 🚀 2. Throughput (Taxa de Transações)

**Definição:**  
Número de transações processadas por unidade de tempo.

**Unidades comuns:**
- **TPS (Transactions per Second)**  
- **RPS (Requests per Second)**

**Exemplo de interpretação:**
> O sistema processa 450 RPS estáveis com tempo médio de resposta de 800 ms.

**Importância:**
- Indica a **capacidade de processamento simultâneo**.  
- Ajuda a avaliar a **eficiência sob carga crescente**.

---

## 📦 3. Concurrency e Users (Usuários Simultâneos)

**Definição:**  
Número de usuários virtuais ou requisições simultâneas sendo executadas.

**Tipos:**
- **Usuários concorrentes:** número de sessões ativas.  
- **Usuários simultâneos:** número de requisições ativas no mesmo instante.

**Dica:**  
Planeje a carga com base em **dados reais de uso** (ex: Google Analytics, logs de acesso).

---

## ⚡ 4. Latência

**Definição:**  
Tempo que leva para a requisição começar a ser atendida (antes de a resposta começar a ser transferida).

**Importância:**
- Indicador de **tempo de espera na rede** e **resposta do servidor**.  
- Alta latência pode indicar **problemas de rede, DNS ou sobrecarga inicial**.

**Exemplo:**
> Requisição HTTP:  
> - Latência: 200 ms  
> - Tempo total: 1,2 s  
> → O tempo de processamento do backend é dominante.

---

## 💾 5. Utilização de Recursos

**Definição:**  
Mede o uso de **CPU, memória, disco e rede** durante o teste de performance.

**Monitoramentos típicos:**
| Recurso | Indicador | Alerta |
|----------|------------|--------|
| CPU | % de uso total e por processo | > 80% contínuo |
| Memória | Consumo e swap | Vazamentos ou picos |
| Disco | IOPS, latência, espaço livre | I/O saturado |
| Rede | Mbps, pacotes perdidos | Congestionamento |

**Ferramentas úteis:** Grafana, Prometheus, New Relic, Datadog, CloudWatch.

---

## ❌ 6. Taxa de Erro (Error Rate)

**Definição:**  
Percentual de requisições com falha em relação ao total de requisições enviadas.

**Cálculo:**
Error Rate (%) = (Número de requisições com erro / Total de requisições enviadas) × 100

**Exemplos numéricos:**
- Se você enviou **10.000** requisições e **50** retornaram erro:

Error Rate = (50 / 10.000) * 100 = 0,5%

- Se em um cenário de pico houve **2.000** requisições e **200** erros:

Error Rate = (200 / 2.000) * 100 = 10%


**Faixas de gravidade (guideline):**
- ✅ **< 1%** — aceitável para a maioria dos sistemas (bom sinal)  
- ⚠️ **1% – 5%** — alerta; investigar causas e comportamento sob carga  
- ❌ **> 5%** — crítico; sistema instável ou saturado, ação imediata necessária

> Observação: metas reais dependem de SLA/SLO do serviço — para sistemas críticos (pagamentos, autenticação) a tolerância pode ser muito menor (ex.: < 0.1%).

---

### Tipos comuns de erros a monitorar
- **HTTP 4xx** (erros do cliente) — requisições malformadas, autenticação, validação.  
- **HTTP 5xx** (erros do servidor) — exceções no backend, timeouts, erro de infraestrutura.  
- **Timeouts** — requisições que não receberam resposta no tempo definido.  
- **Conexões recusadas / reset** — limite de conexões atingido ou serviços abaixo.  
- **Erros de payload / parsing** — falhas ao processar dados (ex.: JSON inválido).  
- **Erros de dependência** — falhas em serviços externos (DB, API de terceiros).

---

### Como coletar a Taxa de Erro
- **Ferramentas de carga:** JMeter, k6, Locust e Gatling já reportam números de sucesso/falha.  
- **Logs e APM:** correlacione com logs de aplicação, traces e métricas de APM (New Relic, Datadog, Prometheus).  
- **Monitoramento infra:** verifique CPU, memória, filas, conexões de banco e limites (file descriptors, threads).  
- **Estratégia:** sempre capture **status code**, **mensagem de erro**, **endpoint**, **latência** e **timestamp**.

---

### Interpretação e investigação (passo a passo)
1. **Confirmar baseline:** comparar com testes anteriores para detectar regressão.  
2. **Segmentar por endpoint:** identifique quais endpoints concentram os erros.  
3. **Verificar tipo de erro:** 4xx vs 5xx vs timeouts.  
4. **Correlacionar com recursos:** CPU/RAM/IO e métricas de DB no momento do erro.  
5. **Analisar logs e traces:** stack traces, exceptions e mensagens detalhadas.  
6. **Testar com menor carga:** reproduzir o erro com carga reduzida para checar sensibilidade.  
7. **Implementar mitigação:** retries exponenciais, circuit breaker, aumentar pool/threads, otimização de query ou cache.  
8. **Re-testar e validar:** executar testes após alterações e comparar métricas.

---

### Ações recomendadas conforme a causa
- **Alta latência → timeouts:** aumentar timeout upstream temporariamente; otimizar queries/handlers.  
- **5xx em massa:** investigar exceção no backend; analisar logs e rollback de deploy (se tiver correlação).  
- **Erros de autenticação (4xx):** revisar tokens/session handling e dados de teste.  
- **Saturação de DB:** aumentar conexões, usar caching, otimizar índices, shard/replicar.  
- **Problema de infra (network/IO):** checar limites da cloud, rede, disco IOPS; considerar escala horizontal.

---

### Exemplos práticos

**JavaScript (exemplo simples para calcular error rate no Postman / node):**
```javascript
const total = 10000;
const errors = 50;
const errorRate = (errors / total) * 100;
console.log(`Error Rate: ${errorRate.toFixed(2)}%`); // 0.50%

---

📘 **Autor:** Sandro Gonçales Funk  
🎯 *QA Engineer | Performance & Automation Enthusiast*  
📅 *Atualizado em 2025*