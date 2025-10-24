<h1 align="center">🧪 Testes de Performance — Conceitos Fundamentais</h1>

<p align="center">
  <a href="#"><img src="https://img.shields.io/badge/Status-Em%20Desenvolvimento-blue?style=flat-square"></a>
  <a href="#"><img src="https://img.shields.io/badge/QA-Performance%20Testing-brightgreen?style=flat-square"></a>
  <a href="#"><img src="https://img.shields.io/badge/Tool-JMeter-orange?style=flat-square"></a>
  <a href="#"><img src="https://img.shields.io/badge/Tool-k6-purple?style=flat-square"></a>
  <a href="#"><img src="https://img.shields.io/badge/Author-Sandro%20Gonçales%20Funk-blueviolet?style=flat-square"></a>
</p>

---

## 📘 Sumário
1. [O que são Testes de Performance](#-1-o-que-são-testes-de-performance)
2. [Objetivos Principais](#-2-objetivos-principais)
3. [Tipos de Testes](#-3-tipos-de-testes-de-performance)
4. [Principais Métricas](#-4-principais-métricas)
5. [Conceitos Essenciais](#-5-conceitos-essenciais)
6. [Processo Básico de Execução](#-6-processo-básico-de-um-teste-de-performance)
7. [Estrutura do Repositório](#-estrutura-sugerida-para-o-repositório)
8. [Próximos Passos](#-próximos-passos)
9. [Autor](#-autor)

---

## 🧩 1. O que são Testes de Performance

Os **testes de performance** têm como objetivo avaliar **como um sistema se comporta sob diferentes condições de carga**, medindo:

- 🚀 **Velocidade**  
- 💪 **Estabilidade**  
- 📈 **Escalabilidade**  
- ⚙️ **Uso de recursos**

> 💬 “O sistema aguenta quantos usuários simultâneos sem degradar a experiência?”

---

## 🚀 2. Objetivos Principais

- 🔹 **Garantir estabilidade:** validar se o sistema permanece funcional sob alta carga.  
- 🔹 **Detectar gargalos:** identificar pontos lentos (banco de dados, rede, API, etc.).  
- 🔹 **Verificar escalabilidade:** entender o comportamento quando há aumento de usuários.  
- 🔹 **Comprovar SLAs:** validar metas como “responder em até 2 segundos”.

---

## ⚙️ 3. Tipos de Testes de Performance

| Tipo | Objetivo | Exemplo |
|------|-----------|----------|
| **Load Test (Carga)** | Avaliar o comportamento sob carga esperada | 500 usuários simultâneos |
| **Stress Test (Estresse)** | Testar o limite máximo antes da falha | Aumentar até o sistema quebrar |
| **Spike Test (Pico)** | Observar reação a picos súbitos | Subir de 100 → 1000 usuários em 5 segundos |
| **Endurance / Soak Test (Resistência)** | Avaliar estabilidade ao longo do tempo | Rodar 8h com carga constante |
| **Scalability Test (Escalabilidade)** | Medir comportamento ao adicionar recursos | Subir número de instâncias e medir ganho |

---

## 📊 4. Principais Métricas

| Categoria | Métrica | O que indica |
|------------|----------|--------------|
| **Tempo de resposta** | `avg`, `median`, `p95`, `p99` | Rapidez das respostas |
| **Taxa de transferência** | `requests/sec`, `throughput` | Quantidade de requisições processadas |
| **Erros** | `% de falhas` | Estabilidade e limites atingidos |
| **Recursos** | `CPU`, `RAM`, `I/O`, `latência de rede` | Capacidade de infraestrutura |

> ⚠️ *Dica:* Sempre colete métricas em conjunto com logs e monitoramento de infraestrutura.

---

## 🧠 5. Conceitos Essenciais

| Conceito | Explicação |
|-----------|------------|
| **Throughput** | Volume de requisições processadas por segundo |
| **Latency** | Tempo entre o envio da requisição e o início da resposta |
| **Response Time** | Tempo total até a resposta completa |
| **Bottleneck** | Gargalo que limita o desempenho |
| **Ramp-up** | Tempo para aumentar gradualmente o número de usuários |
| **SLA / SLO / SLI** | Acordos e indicadores de desempenho de serviço |

---

## 🧩 6. Processo Básico de um Teste de Performance

1. **Definir o objetivo**  
   > Exemplo: “O sistema deve suportar 1000 usuários simultâneos com tempo de resposta < 2s”.

2. **Identificar cenários críticos**  
   Login, busca, checkout e outras funcionalidades de alto impacto.

3. **Configurar ferramenta**  
   Configurar e parametrizar scripts no JMeter, k6, Gatling ou Locust.

4. **Executar testes**  
   Simular diferentes níveis de carga e ramp-ups.

5. **Analisar resultados**  
   Avaliar métricas e gargalos de desempenho.

6. **Reexecutar após ajustes**  
   Validar se as otimizações surtiram efeito.

---

## 📁 Estrutura do repositório

```bash
📦 testes-performance/
 ┣ 📂 docs/
 ┃ ┣ 📜 conceitos.md
 ┃ ┣ 📜 metricas.md
 ┃ ┣ 📜 tipos-de-testes.md
 ┃ ┗ 📜 processo.md
 ┣ 📂 exemplos/
 ┃ ┣ 📜 jmeter-exemplo.jmx
 ┃ ┣ 📜 k6-script.js
 ┃ ┗ 📜 locustfile.py
 ┣ 📜 README.md
 ┗ 📜 LICENSE
