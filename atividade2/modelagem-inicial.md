# Modelo de Otimização de Transporte e Armazenamento de Milho

---

## 1. Estrutura do Sistema e Índices

* **Camada 1 (Origem):** Fazendas de milho
  * $i \in \{1, 2, 3\}$
* **Camada 2 (Intermediária):** Silos de armazenamento de milho
  * $j \in \{1, 2, 3, 4, 5\}$
* **Camada 3 (Destino):** Consumidores
  * $k \in \{1, 2, 3, 4, 5, 6, 7, 8, 9, 10\}$

---

## 2. Variáveis de Decisão

* $x_{ij}$: Quantidade de milho transportada da fazenda $i$ para o silo $j$ (em toneladas), $\forall i \in \{1, 2, 3\}, j \in \{1, 2, 3, 4, 5\}$.
* $y_{jk}$: Quantidade de milho transportada do silo $j$ para o consumidor $k$ (em toneladas), $\forall j \in \{1, 2, 3, 4, 5\}, k \in \{1, 2, \dots, 10\}$.

---

## 3. Função Objetivo

Minimizar os custos totais de transporte entre as camadas:

* **Minimizar custos de transporte entre Camada 1 e Camada 2:**
  $$\min Z_1 = \sum_{i=1}^{3} \sum_{j=1}^{5} c_{ij} \cdot x_{ij}$$

* **Minimizar custos de transporte entre Camada 2 e Camada 3:**
  $$\min Z_2 = \sum_{j=1}^{5} \sum_{k=1}^{10} d_{jk} \cdot y_{jk}$$

### Função Objetivo Geral:
$$\min Z = \min Z_1 + \min Z_2$$

$$\min Z = \sum_{i=1}^{3} \sum_{j=1}^{5} c_{ij} \cdot x_{ij} + \sum_{j=1}^{5} \sum_{k=1}^{10} d_{jk} \cdot y_{jk}$$

---

## 4. Restrições

### 4.1. Camada 1 — Limite de fornecimento de milho (toneladas)
* **Fazenda 1:**
  $$\sum_{j=1}^{5} x_{1j} = 1$$
* **Fazenda 2:**
  $$\sum_{j=1}^{5} x_{2j} = 2$$
* **Fazenda 3:**
  $$\sum_{j=1}^{5} x_{3j} = 2$$

---

### 4.2. Camada 2 — Silos

* **Conservação de Fluxo (capacidade total que entra é igual à que sai):**
  $$\sum_{i=1}^{3} x_{ij} - \sum_{k=1}^{10} y_{jk} = 0, \quad \forall j \in \{1, 2, 3, 4, 5\}$$

* **Capacidade Máxima de Cada Silo (1 tonelada):**
  $$\sum_{i=1}^{3} x_{ij} \le 1, \quad \forall j \in \{1, 2, 3, 4, 5\}$$

---

### 4.3. Camada 3 — Demanda dos Consumidores
Cada consumidor recebe $0{,}5\text{ t}$ ($500\text{ kg}$):

$$\sum_{j=1}^{5} y_{jk} = 0{,}5, \quad \forall k \in \{1, 2, \dots, 10\}$$

---

### 4.4. Limite por Rota ($u_{jk}$)
$$y_{jk} \le u_{jk}, \quad \forall j \in \{1, 2, 3, 4, 5\}, \; \forall k \in \{1, 2, \dots, 10\}$$

---

### 4.5. Não Negatividade
$$x_{ij} \ge 0, \quad \forall i \in \{1, 2, 3\}, \; \forall j \in \{1, 2, 3, 4, 5\}$$

$$y_{jk} \ge 0, \quad \forall j \in \{1, 2, 3, 4, 5\}, \; \forall k \in \{1, 2, \dots, 10\}$$
