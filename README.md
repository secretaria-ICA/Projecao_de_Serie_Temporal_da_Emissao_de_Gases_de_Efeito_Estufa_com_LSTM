# Projeção de Série Temporal da Emissão de Gases de Efeito Estufa com LSTM

#### Aluno: [Rodrigo Chaves Cardoso de Oliveira](https://github.com/rodrigochaves73).
#### Orientadora: [Manoela Kohler](https://github.com/manoelakohler).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

---

### Resumo

O objetivo deste trabalho é rodar três alternativas de modelo de Deep Learning e sugerir o melhor entre eles para estimar o período seguinte de uma série temporal. A série em questão é o histórico de emissões de gases de efeito estufa (GEE) de uma atividade de exploração e produção (E&P), de uma empresa do setor de Óleo e Gás, de grande porte.

#### Base de Dados
Os dados compreendem o período de 2003 a 2019. Foram obtidos dois arquivos, um para treino (emissoes_treino.csv) e um para teste (emissoes_teste.csv).
A base de treino tem os registros mensais de janeiro de 2003 a dezembro de 2018. A base de testes compreende o período de janeiro a dezembro de 2019.

#### Preparação dos Dados
Os dados foram preparados utilizando o janelamento de 12 registros na base de treino, correspondendo ao histórico de um ano para cada valor registrado, a normalização da base de treino, *reshape* para tranformar em tensor e servir de entrada para as redes neurais, a normalização da base de testes e, após aplicação do modelo, a desnormalização para avaliação dos resultados utilizando as métricas de desempenho de modelos.

#### Arquitetura da Rede
Todos os modelos foram construídos considerando uma rede LSTM (Long-Short Term Memory), com 12 inputs para obter 1 output, ou seja, neste caso, com os valores dos últimos 12 meses, será possível prever o valor do próximo mês.

A rede é um modelo Sequencial, com 3 camadas LSTM e Dropout de 0,2 e uma camada final Dense. A primeira camada com 100 unidades, a segunda com 80 e a terceira com 50. As perdas foram definidas por *mse* (mean squared error).

#### Modelos de Redes Neurais
As alternativas se deram pela escolha de 3 otimizadores (ADAM, SGD e RMSProp), sem alterar os demais parâmetros da rede.

### Resultados

#### Alternativa 1 (ADAM)
Os resultados acompanharam bem as formas apresentadas pelos dados reais. Os valores parecem ser sempre superiores aos valores reais.

#### Alternativa 2 (SGD)
Os resultados atenuaram as grandes variações apresentadas pelos dados reais. Os valores parecem ser sempre situados na média em relação aos valores reais, o que pode significar uma ponderação interessante para as previsões.

#### Alternativa 3 (RMSProp)
Assim como a Alternativa 1, os resultados acompanharam bem as formas apresentadas pelos dados reais. Neste caso, os valores parecem ser sempre inferiores aos valores reais.

Os resultados numéricos serão avaliadas agora em termos de RMSE, MSE e MAPE.

#### Avaliação dos Resultados

Alternativa | RMSE | MSE | MAPE | Tempo 
--- | --- | --- | --- |--- 
alt1:lstm+adam | 114811.711606 | 1.318173e+10 | 4.690578 | 46.184942 
**alt2:lstm+sgd**	| 108714.159795 | 1.181877e+10	| 4.746776 | 47.527325
alt3:lstm+rmsprop	| 115261.134965	| 1.328513e+10	| 4.994035	| 48.326665

De acordo com os resultados acima, a combinação "modelo + otimizador" que apresentou melhores resultados foi a Alternativa 2 (LSTM + SGD).

Para futuros estudos, recomenda-se buscar obter mais valores de output para cada grupo de inputs, por exemplo, permitir a previsão de 3 meses a partir de um input de 6 meses. Também sugere-se rodar uma validação, reservando um trecho da série temporal para validar os resultados do modelo.

---

Matrícula: 192.190.069

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
