# Pesquisa Operacional - Otimização Operacional do Agendamento de Bombas e Distribuição de Água Tratada via Programação Linear Inteira Mista (MILP)

Repositório do projeto **Otimização Operacional do Agendamento de Bombas e Distribuição de Água Tratada via Programação Linear Inteira Mista (MILP)** apresentado na disciplina **MAI5032 - Tópicos em Pesquisa Operacional**, do **MECAI 2026**, com modelos de Pesquisa Operacional implementados em notebooks Jupyter.

## Projeto principal

O projeto principal modela o agendamento operacional de bombas de uma estação de tratamento de água (ETA) e a distribuição da água tratada para reservatórios e setores consumidores. O objetivo é minimizar o custo diário de energia elétrica sem deixar de atender a demanda e os limites operacionais do sistema.

A demanda representa uma distribuição para uma cidade plana, com comportamento próximo ao de Santos. O cenário considera:

- 6 bombas;
- 5 reservatórios;
- 12 setores consumidores;
- demanda-base total de 5.195 m³/h;
- demanda média de 8.312 m³/h (199.488 m³/dia);
- demanda máxima horária de 17.663 m³/h às 18h;
- tarifa fora de ponta de R$ 0,4525/kWh;
- tarifa de ponta de R$ 1,4048/kWh entre 18h00 e 20h59;
- horizonte diário de 24 horas, configurável para passos de 1 hora (24 períodos) ou 1 minuto (1.440 períodos).

## Formulação

Os notebooks utilizam um modelo enxuto de programação linear inteira mista (MILP) que determina:

- quais bombas permanecem ligadas em cada período;
- a vazão bombeada por cada bomba (representada diretamente pela soma dos fluxos de recalque);
- os fluxos entre bombas, reservatórios e setores;
- o volume armazenado em cada reservatório.

As principais restrições são:

- limites mínimo e máximo de vazão das bombas;
- capacidade máxima agregada da ETA (9.400 m³/h);
- atendimento integral da demanda por setor;
- balanço volumétrico dos reservatórios;
- limites mínimo (15%) e máximo (100%) de volume de cada reservatório, aplicados diretamente nos *bounds* das variáveis;
- recuperação do volume inicial (30%) ao final do horizonte.

O objetivo minimiza o consumo de potência das bombas multiplicado pela tarifa horária. Os notebooks também incluem um cenário-base opcional com tarifa uniforme para comparação econômica e **warm start hierárquico** (solução horária projetada para o modelo minuto a minuto) para acelerar a convergência.

## Notebooks

| Notebook | Biblioteca | Solvers | Horizonte (`MODO_TEMPORAL`) |
|---|---|---|---|
| [PO_Otimização_ETA_MIN_Pyomo_otimizado.ipynb](PO_Otimização_ETA_MIN_Pyomo_otimizado.ipynb) | Pyomo | HiGHS, CBC ou Gurobi | `"hora"` (24 períodos) ou `"minuto"` (1.440 períodos) |
| [PO_Otimização_ETA_MIN_mip_otimizado.ipynb](PO_Otimização_ETA_MIN_mip_otimizado.ipynb) | python-mip | HiGHS, CBC ou Gurobi | `"hora"` (24 períodos) ou `"minuto"` (1.440 períodos) |

As duas versões compartilham os mesmos dados físicos e econômicos, formulação enxuta (−35% de restrições frente à formulação base), warm start hierárquico opcional e acompanhamento temporal da otimização.

Os notebooks geram:

- status e métricas da solução (incumbente, limite inferior, gap relativo e nós explorados);
- acompanhamento temporal da otimização para HiGHS e CBC (gráficos de incumbente vs. limite inferior e evolução do gap);
- consumo de energia e custo da programação;
- comparação entre cenário-base e solução otimizada;
- perfil de bombeamento e tarifa;
- dinâmica de volume e nível percentual dos reservatórios.

## Documentação e Resultados

- **Análise comparativa dos solvers:** [Benchmark/Comparativo-Analise-Solvers.md](Benchmark/Comparativo-Analise-Solvers.md) — artigo técnico comparando Pyomo e python-mip com HiGHS, CBC e Gurobi (horário vs. minuto a minuto, *cold start* vs. formulação enxuta + *warm start*).
- **Apresentação do projeto (PDF 16:9):** [Apresentação/Apresentacao_ETA_PO_2026_v2.pdf](Apresenta%C3%A7%C3%A3o/Apresentacao_ETA_PO_2026_v2.pdf)

## Requisitos

- Python 3.10 ou superior;
- Jupyter Notebook ou JupyterLab;
- Pyomo e/ou python-mip;
- NumPy;
- pandas;
- Matplotlib;
- um dos solvers HiGHS, CBC ou Gurobi.

Os notebooks por Pyomo e python-mip podem instalar automaticamente suas dependências em execução.

## Como executar

1. Clone este repositório.
2. Abra o notebook desejado no Jupyter Notebook, JupyterLab ou VS Code.
3. Execute a célula de instalação de dependências.
4. Reinicie o kernel, caso uma dependência tenha sido instalada durante a execução.
5. Na **Seção 2**, configure `MODO_TEMPORAL` (`"hora"` ou `"minuto"`), `USAR_WARM_START`, `ACOMPANHAR_PROGRESSO` e a execução do cenário-base.
6. Na **Seção 3**, selecione o solver pela variável `SOLVER` (`"highs"`, `"highs_base"`, `"cbc"` ou `"gurobi"`).
7. Execute as células na ordem apresentada.

O padrão do notebook Pyomo é o **HiGHS** (`SOLVER = "highs"`) e o do notebook python-mip é o **CBC** (`SOLVER = "cbc"`), sendo possível alternar facilmente entre ambos. Para usar Gurobi:

- no Pyomo, configure o pacote `gurobipy`;
- no python-mip, configure uma instalação nativa do Gurobi (com uma licença válida) por meio de `GUROBI_HOME` e reinicie o kernel.

Exemplo de instalação básica:

```bash
python -m pip install jupyter "pyomo>=6.8" "mip==2.0.0" "highspy>=1.8" cbcbox gurobipy pandas numpy matplotlib
```

## Observações

- O modo `"minuto"` (1.440 períodos, 8.640 variáveis binárias) demanda significativamente mais esforço computacional que o modo `"hora"`; recomenda-se manter `USAR_WARM_START = True` para atingir gaps abaixo de 0,5% em poucos minutos.
- Modelagem e dados baseados no [SINISA 2024](https://www.aguaesaneamento.org.br/municipios-e-saneamento/sp/santos) e [PMSB de Santos](https://www.santos.sp.gov.br/?q=servico/plano-municipal-de-saneamento-basico).
- As potências das bombas são hipóteses médias para simulação, calculadas com 30 m de altura manométrica e eficiência global de 80%.
