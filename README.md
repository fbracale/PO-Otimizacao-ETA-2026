# MAI5032 - Tópicos em Pesquisa Operacional

Repositório de atividades, modelos e notebooks desenvolvidos para a disciplina **MAI5032 - Tópicos em Pesquisa Operacional**, do **MECAI 2026**.

## Objetivo

Organizar os materiais produzidos ao longo da disciplina, com foco na modelagem e na resolução computacional de problemas de Pesquisa Operacional.

## Estrutura do repositório

```text
.
├── README.md
└── atividade2/
	├── 2026_Transbordo.ipynb
	├── 2026_Transbordo_3_camadas_Milho.ipynb
	├── atividade2.md
	└── modelagem-inicial.md
```

### Atividade 2

A atividade aborda o **Problema do Transbordo** em uma rede de transporte com três camadas:

- fazendas, como nós de oferta;
- depósitos, como nós intermediários;
- consumidores, como nós de demanda.

O exercício propõe criar um exemplo, formular o modelo, implementá-lo utilizando o Gurobi e analisar a solução obtida.

- [Enunciado da atividade](atividade2/atividade2.md)
- [Modelagem inicial](atividade2/modelagem-inicial.md)
- [Notebook base sobre transbordo](atividade2/2026_Transbordo.ipynb)
- [Notebook do problema com três camadas e milho](atividade2/2026_Transbordo_3_camadas_Milho.ipynb)

## Requisitos

- Python 3;
- Jupyter Notebook ou JupyterLab;
- Gurobi e o pacote `gurobipy`;
- licença do Gurobi válida para execução dos modelos.

## Como executar

1. Clone este repositório.
2. Instale o Python e o Jupyter Notebook ou JupyterLab.
3. Instale e configure o Gurobi e o pacote `gurobipy`.
4. Abra o notebook desejado na pasta correspondente.
5. Execute as células na ordem apresentada e analise os resultados gerados.

Exemplo de instalação do pacote Python:

```bash
python -m pip install gurobipy jupyter
```

## Autoria

Este repositório reúne o trabalho desenvolvido para a disciplina MAI5032 - Tópicos em Pesquisa Operacional (MECAI 2026).
