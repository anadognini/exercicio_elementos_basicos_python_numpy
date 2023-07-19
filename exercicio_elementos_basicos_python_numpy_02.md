```python
import numpy as np
```

### 1) Alturas  
i. No trecho de código abaixo, crie um ndarray chamado ```altura_em_centimetros``` transformando a lista ```lista_de_alturas``` em um ndarray do numpy com a função ```np.array()```  
ii. Crie um outro objeto ```altura_em_metros```, com os valores de ```altura_em_centimetros``` convertidos para metros.


```python
lista_de_centimetros = list(range(170, 190, 5))
lista_de_centimetros
```




    [170, 175, 180, 185]




```python
altura_em_centimetros = np.array(lista_de_centimetros)

altura_em_metros = altura_em_centimetros / 100.0
```


```python
print(altura_em_metros) 
```

    [1.7  1.75 1.8  1.85]
    

### 2) IMC  
i. Considere que pesos em Kg dessas pessoas, na mesma ordem, estão na lista pesos ```lista_pesos = [70, 75, 80, 85]```. Crie um **ndarray** chamado ```pesos``` com a função ```np.array()``` que contenha esses valores.  
ii. Utilizando o objeto que contém as alturas em metros e esse objeto que contém os respectivos pesos em quilos, calcule o IMC desses indivíduos utilizando a aritmética de arrays e guarde os resultados em um objeto chamado ```imc```.


```python
lista_pesos = [70, 75, 80, 85]
lista_pesos
# seu código aqui

pesos = np.array(lista_pesos)
print(pesos)
```

    [70 75 80 85]
    


```python
# calcule o IMC dessas pessoas

def calcula_IMC(peso, altura):
    imc = peso / (altura * altura)
    return imc

print(calcula_IMC(pesos, altura_em_metros))
```

    [24.22145329 24.48979592 24.69135802 24.83564646]
    

### 3) Endividamento

Cálculos de novas variáveis como endividamento total e comprometimento de renda são essenciais para a construção de modelos financeiros em ciência de dados. Áreas não financeiras terão cálculos semelhantes também. Vamos praticar:

Considere que o seguinte ndarray contém os dados de 4 pessoas, total a ser pago a empréstimos mensalmente e renda familiar:

| custo fixo | dívida financeira | renda familiar |
|:----:|:----:|:---|
| 3000  | 1000 | 6000 |
| 2500  | 2500 | 5500 |
| 1000  | 3000 | 7000 |
| 10000 | 5000 | 16000 |

i. Transforme a lista de listas ```dados_financeiros``` no ndarray ```nd_financeiros```.
> ``` dados_financeiros[[3000, 2500, 1000, 10000],[1000, 2500, 3000, 5000],[6000, 5500, 7000, 16000]] ```

ii. Utilize o método ```.transpose ``` e certifique-se de que esse ndarray tenha uma linha por indivíduo e uma coluna por informação. Utilizando a indexação do numpy, imprima no output a segunda linha do array, depois a segunda coluna.

iii. Pratique aritmética com nearrays e calcule o endividamento total como:
$$endividamento\hspace{.2cm}total = \frac{custo \hspace{.2cm}fixo + dívida\hspace{.2cm}financeira}{renda\hspace{.2cm}familiar}$$
Guarde os resultados em uma variável chamada ```endividamento_total``` e verifique os resultados imprimindo o conteúdo dessa variável no output.

iv. Considere que há um erro de digitação que precisa ser corrigido: 3o indivíduo na verdade não possui renda familiar de R\\$7.000,00, mas sim R\\$ 10.000,00. Corrija esse valor e refaça os cálculos.


```python
# lista dados_financeiros
dados_financeiros = [[3000, 2500, 1000, 10000], [1000, 2500, 3000, 5000], [6000, 5500, 7000, 16000]]
dados_financeiros

#i) transforme essa lista em um ndarray

nd_financeiros = np.array(dados_financeiros)
print(nd_financeiros)
```

    [[ 3000  2500  1000 10000]
     [ 1000  2500  3000  5000]
     [ 6000  5500  7000 16000]]
    


```python
# ii) 
nd_financeiros_transpose = nd_financeiros.transpose()

print(nd_financeiros_transpose[1]) # segunda linha do array
print(nd_financeiros_transpose[:, 1]) # segunda coluna do array
```

    [2500 2500 5500]
    [1000 2500 3000 5000]
    


```python
# iii) Calcule o endividamento total

custo_fixo = nd_financeiros_transpose[0]
divida_financeira = nd_financeiros_transpose[1]
renda_familiar = nd_financeiros_transpose[2]

endividamento_total = (custo_fixo + divida_financeira) / renda_familiar

print("Endividamento Total:")
print(endividamento_total)
```

    Endividamento Total:
    [5.5        1.16666667 1.64285714]
    


```python
# iv)  corrigindo um valor específico

dados_financeiros = [[3000, 2500, 1000, 10000], [1000, 2500, 3000, 5000], [6000, 5500, 10000, 16000]]
nd_financeiros = np.array(dados_financeiros)

nd_financeiros_transpose = nd_financeiros.transpose()
```


```python
custo_fixo = nd_financeiros_transpose[0]
divida_financeira = nd_financeiros_transpose[1]
renda_familiar = nd_financeiros_transpose[2]

endividamento_total_corrigido = (custo_fixo + divida_financeira) / renda_familiar

print("Endividamento Total:")
print(endividamento_total_corrigido)
```

    Endividamento Total:
    [5.5        1.16666667 1.15      ]
    

### 4) É muito comum precisarmos identificar valores especiais e darmos tratamento a eles quer seja alterando-os quer seja descartando-os. 

O trecho de código abaixo gera um ndarray com números pseudo aleatórios. Considere que para efeitos do estudo que virá, devemos desconsiderar valores iguais a zero. Sendo assim:

i) crie um objeto ```bool_zero``` que traga uma sequencia de booleanos do mesmo tamanho que o objeto poi, e que vale ```True``` quando o valor de ```poi``` é zero, e ```False``` caso contrário.

ii) Conte quantos valores zero existem. Lembre-se de que no final das contas, ```True``` vale 1 para o Python, e ```False``` vale zero, então uma boa dica seria usar a função ```sum()```.

iii) Utilize a indexação booleana que você aprendeu para criar uma variável ```poi_nao_zero``` que aponta para os elementos de ```poi``` diferentes de zero. Dica: você vai pode inverter os elementos do objeto que criou em *ii)* ou escrever a comparação adequada.


```python
# objeto poi - obs: o comando np.random.seed(1234) garante que o mesmo resultado será gerado sempre
np.random.seed(1234)
poi = np.random.poisson(3, 100)

print(poi)
```

    [3 3 6 2 4 5 4 4 2 0 3 3 2 8 2 3 3 3 0 4 4 2 6 6 0 3 4 3 5 2 1 3 2 2 3 2 4
     4 5 7 3 5 3 3 2 2 3 6 2 2 4 3 5 2 5 3 0 2 1 1 4 4 4 6 2 4 1 2 5 5 3 4 1 4
     1 1 7 1 2 1 3 7 0 4 4 0 6 1 3 4 2 5 4 5 5 3 4 6 8 2]
    


```python
# i) crie o objeto bool_zero através do operador == 

bool_zero = (poi == 0)
bool_zero
```




    array([False, False, False, False, False, False, False, False, False,
            True, False, False, False, False, False, False, False, False,
            True, False, False, False, False, False,  True, False, False,
           False, False, False, False, False, False, False, False, False,
           False, False, False, False, False, False, False, False, False,
           False, False, False, False, False, False, False, False, False,
           False, False,  True, False, False, False, False, False, False,
           False, False, False, False, False, False, False, False, False,
           False, False, False, False, False, False, False, False, False,
           False,  True, False, False,  True, False, False, False, False,
           False, False, False, False, False, False, False, False, False,
           False])




```python
# ii) Conte a quantidade de zeros (ou some os elementos de bool_zero)

num_zeros = np.sum(bool_zero)
print(num_zeros)
```

    6
    


```python
# iii) utilize a indexação booleana para criar uma seleção de não-zeros
# dica: inverta o objeto bool_zero

poi_nao_zero = poi[~bool_zero]
print(poi_nao_zero)
```

    [3 3 6 2 4 5 4 4 2 3 3 2 8 2 3 3 3 4 4 2 6 6 3 4 3 5 2 1 3 2 2 3 2 4 4 5 7
     3 5 3 3 2 2 3 6 2 2 4 3 5 2 5 3 2 1 1 4 4 4 6 2 4 1 2 5 5 3 4 1 4 1 1 7 1
     2 1 3 7 4 4 6 1 3 4 2 5 4 5 5 3 4 6 8 2]
    


```python
qtd_valores_poi = poi.size
print("Quantidade de valores em poi:")
print(qtd_valores_poi)
```

    Quantidade de valores em poi:
    100
    


```python
qtd_valores_poi_nao_zero = poi_nao_zero.size
print("Quantidade de valores em poi_nao_zero:")
print(qtd_valores_poi_nao_zero)
```

    Quantidade de valores em poi_nao_zero:
    94
    
