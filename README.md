# Pesquisa Operacional - Otimização Operacional do Agendamento de Bombas e Distribuição de Água Tratada via Programação Linear Inteira Mista (MILP)

Repositório do projeto **Otimização Operacional do Agendamento de Bombas e Distribuição de Água Tratada via Programação Linear Inteira Mista (MILP)** apresentado na disciplina **MAI5032 - Tópicos em Pesquisa Operacional**, do **MECAI 2026**, com modelos de Pesquisa Operacional implementados em notebooks Jupyter.

## Projeto principal

O projeto principal modela o agendamento operacional de bombas de uma estação de tratamento de água (ETA) e a distribuição da água tratada para reservatórios e setores consumidores. O objetivo é minimizar o custo diário de energia elétrica sem deixar de atender a demanda e os limites operacionais do sistema.

A demanda representa uma distribuição para uma cidade plana, com comportamento próximo ao de Santos. O cenário considera:

- 6 bombas;
- 5 reservatórios;
- 12 setores consumidores;
- demanda-base total de 5.195 m³/h;
- demanda média de 8.312 m³/h;
- demanda máxima horária de 17.663 m³/h às 18h;
- tarifa fora de ponta de R$ 0,4525/kWh;
- tarifa de ponta de R$ 1,4048/kWh entre 18h00 e 20h59;
- horizonte diário de 1440 minutos (24 horas).

## Formulação

Os notebooks utilizam um modelo de programação linear inteira mista (MILP) que determina:

- quais bombas permanecem ligadas em cada período;
- a vazão bombeada por cada bomba;
- os fluxos entre bombas, reservatórios e setores;
- o volume armazenado em cada reservatório.

As principais restrições são:

- limites mínimo e máximo de vazão das bombas;
- capacidade máxima agregada da ETA;
- atendimento integral da demanda por setor;
- balanço volumétrico dos reservatórios;
- limites mínimo e máximo de volume de cada reservatório;
- recuperação do volume inicial ao final do horizonte.

O objetivo minimiza o consumo de potência das bombas multiplicado pela tarifa horária. Os notebooks também incluem um cenário-base opcional com tarifa uniforme para comparação com a solução tarifária otimizada.

## Notebooks

| Notebook | Biblioteca | Resolução | Horizonte |
|---|---|---|---|
| [PO_Otimização_ETA_HORA_Pyomo.ipynb](PO_Otimização_ETA_HORA_Pyomo.ipynb) | Pyomo | HiGHS, CBC ou Gurobi | 24 intervalos de 1 hora |
| [PO_Otimização_ETA_MIN_Pyomo.ipynb](PO_Otimização_ETA_MIN_Pyomo.ipynb) | Pyomo | HiGHS, CBC ou Gurobi | 1.440 intervalos de 1 minuto |
| [PO_Otimização_ETA_HORA_mip.ipynb](PO_Otimização_ETA_HORA_mip.ipynb) | python-mip | HiGHS, CBC ou Gurobi | 24 intervalos de 1 hora |
| [PO_Otimização_ETA_MIN_mip.ipynb](PO_Otimização_ETA_MIN_mip.ipynb) | python-mip | HiGHS, CBC ou Gurobi | 1.440 intervalos de 1 minuto |

As quatro versões possuem os mesmos dados físicos e econômicos. Os notebooks por hora permitem uma análise mais rápida, enquanto os notebooks por minuto representam cada hora com maior detalhamento temporal.

Os notebooks geram:

- status e métricas da solução;
- consumo de energia;
- custo da programação;
- comparação entre cenário-base e solução otimizada;
- perfil de bombeamento e tarifa;
- dinâmica de volume dos reservatórios;
- nível percentual dos reservatórios.

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
5. Selecione o solver pela variável `SOLVER`.
6. Execute as células na ordem apresentada.

O padrão dos notebooks é utilizar o CBC. HiGHS pode ser selecionado pela mesma configuração. Para usar Gurobi:

- no Pyomo, configure o pacote `gurobipy`;
- no python-mip, configure uma instalação nativa do Gurobi (com uma licença válida) por meio de `GUROBI_HOME` e reinicie o kernel.

Exemplo de instalação básica:

```bash
python -m pip install jupyter "pyomo>=6.8" "mip==2.0.0" "highspy>=1.8" cbcbox gurobipy pandas numpy matplotlib
```

## Observações

- Os notebooks minuto a minuto possuem mais variáveis e podem demandar significativamente mais tempo de execução que as versões horárias.
- Modelagem e dados baseados no [SINISA 2024](https://www.aguaesaneamento.org.br/municipios-e-saneamento/sp/santos) e [PMSB de Santos](https://www.santos.sp.gov.br/?q=servico/plano-municipal-de-saneamento-basico)
- As potências das bombas são hipóteses médias para simulação, calculadas com 30 m de altura manométrica e eficiência global de 80%.
