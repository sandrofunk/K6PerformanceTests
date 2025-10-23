# 🧩 Tipos de Testes de Performance

Os testes de performance englobam diferentes abordagens, cada uma voltada para avaliar aspectos específicos do comportamento de um sistema sob carga.  
A escolha do tipo de teste depende dos **objetivos do projeto**, **requisitos de negócio** e **níveis de serviço esperados (SLAs e SLOs)**.

---

## 1. Teste de Carga (Load Test)

**🎯 Objetivo:**  
Verificar como o sistema se comporta sob uma carga esperada de usuários, requisições ou transações durante um período de tempo.

**Características:**
- Simula o uso típico ou ligeiramente acima do esperado.  
- Mede **tempo de resposta**, **throughput**, **taxa de erro** e **uso de recursos**.  
- Ajuda a identificar gargalos de desempenho em condições normais de operação.

**Quando aplicar:**
- Antes de lançamentos em produção.  
- Após atualizações significativas no sistema.  
- Para validar a escalabilidade e eficiência sob demanda média.

---

## 2. Teste de Estresse (Stress Test)

**🎯 Objetivo:**  
Avaliar o comportamento do sistema sob **carga extrema**, além do limite esperado, até o ponto de falha.

**Características:**
- Identifica o **ponto de quebra** e como o sistema se recupera.  
- Mede **resiliência**, **tolerância a falhas** e **recuperação pós-estouro**.  
- Essencial para ambientes críticos que exigem alta disponibilidade.

**Quando aplicar:**
- Em sistemas que precisam manter disponibilidade mesmo sob picos (ex: Black Friday, campanhas de marketing).  
- Para validar mecanismos de fallback, cache e fila.

---

## 3. Teste de Picos (Spike Test)

**🎯 Objetivo:**  
Analisar o impacto de **aumentos repentinos e curtos de carga** (picos de usuários simultâneos).

**Características:**
- Carga sobe abruptamente e depois retorna ao normal.  
- Mede **elasticidade**, **tempo de estabilização** e **comportamento sob variações rápidas**.  

**Quando aplicar:**
- Para sistemas SaaS ou e-commerce com picos imprevisíveis de acesso.  
- Para avaliar a resposta da infraestrutura elástica (auto scaling, CDN, etc).

---

## 4. Teste de Volume (Volume Test)

**🎯 Objetivo:**  
Validar o comportamento do sistema ao lidar com **grandes volumes de dados**.

**Características:**
- Avalia **tempo de processamento**, **consumo de memória** e **capacidade de armazenamento**.  
- Testa limites de **bancos de dados**, **ETLs** e **relatórios**.

**Quando aplicar:**
- Em sistemas que processam grandes lotes de dados (financeiros, logs, analytics).  
- Antes de migrações ou operações em larga escala.

---

## 5. Teste de Endurance (Soak Test)

**🎯 Objetivo:**  
Medir o desempenho do sistema sob **carga contínua por longos períodos**.

**Características:**
- Executa com carga normal, mas durante várias horas ou dias.  
- Detecta **vazamentos de memória**, **degradação de performance** e **problemas de estabilidade**.  

**Quando aplicar:**
- Em sistemas 24/7 (bancos, ERPs, APIs corporativas).  
- Antes de liberar versões para produção contínua.

---

## 6. Teste de Escalabilidade (Scalability Test)

**🎯 Objetivo:**  
Verificar como o sistema **cresce em desempenho** à medida que se aumentam recursos (CPU, memória, instâncias, etc).

**Características:**
- Mede a **relação entre aumento de recursos e ganho de performance**.  
- Pode ser vertical (mais poder por máquina) ou horizontal (mais máquinas).  

**Quando aplicar:**
- Em arquiteturas de microserviços e cloud.  
- Durante decisões de investimento em infraestrutura.

---

## 7. Teste de Capacidade (Capacity Test)

**🎯 Objetivo:**  
Determinar o **número máximo de usuários simultâneos** que o sistema pode suportar sem violar SLAs.

**Características:**
- Serve como base para **planejamento de capacidade** (capacity planning).  
- Identifica **limites sustentáveis de operação**.

**Quando aplicar:**
- Em ambientes que precisam de **garantias contratuais de desempenho**.  
- Antes de expansões de infraestrutura.

---

## 8. Teste de Comparação (Benchmark Test)

**🎯 Objetivo:**  
Comparar o desempenho de diferentes versões, configurações ou tecnologias.

**Características:**
- Utiliza **cenários controlados e métricas padronizadas**.  
- Mede **ganhos de performance** entre versões ou alternativas técnicas.  

**Quando aplicar:**
- Ao migrar para nova linguagem, framework ou provedor de nuvem.  
- Durante a escolha de ferramentas de banco de dados ou APIs.

---

## 9. Teste de Latência e Throughput

**🎯 Objetivo:**  
Medir a **rapidez** e a **capacidade de processamento simultâneo** do sistema.

**Características:**
- **Latência:** tempo entre requisição e resposta.  
- **Throughput:** número de transações por segundo (TPS/RPS).  
- São métricas fundamentais em todos os testes de performance.

**Quando aplicar:**
- Em APIs REST, microserviços e integrações com alto volume de requisições.

---

## 📈 Resumo Comparativo

| Tipo de Teste | Objetivo Principal | Duração | Carga | Cenário Comum |
|----------------|--------------------|----------|--------|----------------|
| **Carga** | Validar desempenho esperado | Média | Esperada | Lançamento de sistema |
| **Estresse** | Identificar ponto de falha | Curta | Extrema | Campanhas intensas |
| **Picos (Spike)** | Testar variação repentina | Curta | Irregular | Acesso simultâneo súbito |
| **Volume** | Processamento de dados grandes | Média | Constante | Relatórios massivos |
| **Endurance** | Verificar estabilidade contínua | Longa | Normal | Operação 24/7 |
| **Escalabilidade** | Validar crescimento com recursos | Variável | Escalada | Cloud e microserviços |
| **Capacidade** | Definir limite suportado | Média | Gradual | Planejamento de capacidade |
| **Benchmark** | Comparar versões/configurações | Curta | Controlada | Atualização de stack |
| **Latência/Throughput** | Medir velocidade e vazão | Curta | Variável | APIs de alto desempenho |

---

> 💡 **Dica:** Combine diferentes tipos de testes para obter uma visão completa da performance do sistema.  
> Por exemplo: primeiro realize um **teste de carga** para avaliar o desempenho médio, seguido de um **teste de estresse** para encontrar os limites e, por fim, um **teste de endurance** para garantir estabilidade ao longo do tempo.

---
📘 **Autor:** Sandro Gonçales Funk  
🎯 *QA Engineer | Performance & Automation Enthusiast*  
📅 *Atualizado em 2025*