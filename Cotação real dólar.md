Importei as bibliotecas apropriadas:

- Pandas, para dataframes;
- Matplotlib, para gráficos simples;
- Seaborn, para gráficos mais elaborados;
- Prophet, para previsões;
- Numpy, para operações matemáticas.

Li o arquivo CSV e fiz as conversões de formatos necessários: [real_dolar.csv](https://github.com/mths-andrade/dolar/blob/a2019e917a632db7db6493fcf1774ee7f070a8a6/real_dolar.csv)

Além disso, fiz o tratamento de dados nulos por interpolação.

Abaixo, temos alguns resultados:

|  | reais |
| --- | --- |
| contagem | 7695.000000 |
| média | 2.719741 |
| mínimo | 0.832000 |
| 25% | 1.787000 |
| 50% | 2.312000 |
| 75% | 3.495550 |
| máximo | 5.920400 |
| desvio padrão | 1.309956 |

Temos 7695 dados, cuja média é 2.72 reais. A cotação mínima foi de 83 centavos em 13/02/1995 e a máxima, de 5.92 reais em 13/05/2022. O desvio padrão é de 1.31 reais, consideravelmente alto.  A mediana é de R$2.31. 

Podemos dizer que apenas 25% dos dados estão acima do terceiro quartil, que é R$3.50, e 25% abaixo de 1.79 reais, o primeiro quartil. Ou seja, a distância interquartil é 3.50-1.79, que é de R$1.71.

Lembrando de que grande parte dos valores é aproximada, como pode ser visto na tabela ao lado.

Abaixo, a frequência das cotações.

![frequência dólar](https://github.com/mths-andrade/dolar/assets/159069202/f0651a6c-0a5b-480c-8eac-1ed0e0b02f3f)

Mesmo com os crescentes aumentos a partir da pandemia, temos, em maioria, cotações abaixo de 3 reais. Já vimos algo parecido na tabela de estatística, mas agora temos tal fato visualmente.

Temos a série temporal diária das cotações:

![cotação](https://github.com/mths-andrade/dolar/assets/159069202/4b179c1c-d029-43dc-a90b-573ffc95a107)

Temos também a série temporal mensal média. Vemos que são bem parecidas, mas a segunda é mais suave, pois considera menos dados. Vou trabalhar com esses dados de agora em diante.

![cotação média](https://github.com/mths-andrade/dolar/assets/159069202/ffc6743b-7e52-47bd-82d4-a4d898db0702)

Transformando as datas em números, podemos fazer uma regressão. Espera-se algum ajuste, mas não muito. Temos alguma relação linear. Ajustando pelos mínimos quadrados, temos um coeficiente de correlação de 0.671, bastante razoável.

Temos p-valores nulos, tornando o modelo estatístico relevante.

![modelo](https://github.com/mths-andrade/dolar/assets/159069202/c59d4896-63c7-4779-ba23-047d39f9f7b1)

![regressão](https://github.com/mths-andrade/dolar/assets/159069202/3a0ed085-a6be-431f-9a3a-8860b1069767)

Agora, usei o Prophet para fazer a previsão das cotações até o fim do ano. Usei os valores médios de cada mês.

![previsão](https://github.com/mths-andrade/dolar/assets/159069202/226d8f65-1676-48a9-a9e3-c1f013c64b4c)

Entre 2003 e 2010, vemos uma diminuição na cotação e aumento no resto do tempo. A presença de outliers não é tão alta, apenas em 2003, 2016 e a partir da pandemia, acima ou abaixo do intervalo de confiança.

Nessa página HTML, temos um gráfico interativo da previsão criado usando a biblioteca Plotly. Ele funciona melhor em computadores: [real_dolar.html](https://github.com/mths-andrade/dolar/blob/a2019e917a632db7db6493fcf1774ee7f070a8a6/real_dolar.html)

Dando um zoom no futuro, não se espera um grande salto nas cotações, assim como na taxa de inflação.

![plotly](https://github.com/mths-andrade/dolar/assets/159069202/5fc6e63d-7423-4352-a5df-707cbc612bbe)

Temos também gráficos de tendências:

![tendência](https://github.com/mths-andrade/dolar/assets/159069202/8270ae14-9339-4f57-807a-ea7fe7de8015)

O único período com tendência de queda foi entre final de 2003 e 2010 mais ou menos, atualmente continuamos na tendência de aumento. Depois, temos uma visualização anual. Nota-se que a cotação tende a diminuir entre janeiro e março e a subir até julho, enquanto diminui de novo até setembro, quando passa a aumentar até o fim do ano.

Obrigado pela leitura!

Notebook: [real_dolar.ipynb](https://github.com/mths-andrade/dolar/blob/a2019e917a632db7db6493fcf1774ee7f070a8a6/real_dolar.ipynb)
