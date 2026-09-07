# Atividade 2

Considere o **Problema do Transbordo** e o código disponibilizado na **Aula 2** (`2026_Transbordo.ipynb`).

Imagine agora a situação hipotética em que existem **3 camadas na rede de transporte**, com diversas fazendas oferecendo toneladas de um tipo de produto, como, por exemplo, milho.

Esse milho deve ser transportado até depósitos localizados na segunda camada.

Devemos considerar que existem pelo menos 3 fazendas, 5 depósitos e que o milho chega a esses depósitos, devendo ser totalmente transportado utilizando outro meio de transporte.

Após esses depósitos, há uma terceira camada com vários consumidores que devem receber os pedidos de milho em toneladas (considere pelo menos 10 consumidores com suas respectivas demandas).

Considere também que existem custos de transporte por tonelada para deslocar do nó *i* para o nó *j* em cada camada.

Crie um exemplo, modele e codifique utilizando o **Gurobi** (`gurobi.py`) e analise a solução obtida.

Fazer o exercício em grupo com, no máximo, 2 alunos.

Escrever o papel de cada um no desenvolvimento da atividade.

Apresentar o notebook com o relatório.

> **Atenção**, tem que tratar com os nós de cada uma das camadas.