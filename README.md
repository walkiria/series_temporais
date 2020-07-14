# Series temporais

Estudo de series temporais 

### Clustering com series Temporais

Alguns pontos que devemos levar em consideração ao realizar uma tarefa de mineração de dados de series temporais:

- Normalização: é uma tarefa essencial para corrigir possiveis distorções. O tipo pmais usado é a normalização Z. Em que cada valor da serie é subtraido da media e dividido pelo desvio padrao:

$$
 \hat{x_i} = \frac{x_i - \mu}{\sigma}
$$

As referências mostram que a falta de normalização pode levar a taxas de erro  50\% maior. 

Outra forma de normalizar é utilizando o max min: 
$$
 \hat{x_i} = \frac{x_i - min(x)}{max(x) - min(x)}
$$

- Métricas de dissimilaridade para tarefas de cluster:
 - Minkowski
$$
dist(x,y) = (\sum_{1}^n |x_i - y_i |^p)^{1/p}
$$
 
 Pode derivar outras formulas dependendo do valor de p: 
 Euclidiana: $$p = 2$$ 
 Manhattan: $$p=1$$ 
 Chebyshew: $$p-> \inf$$
 
 Observa-se que pequenas variações no valor de p, levam a grandes variações na metrica. 
 
 
 - Dynamic Time Warping - DTW (não é uma metrica de distancia, pois não obedece a desigualdade de triangulo, diferentemente de Minkowski pode ser aplicada a series temporais de diversos tamanhos e não é sensivel ao deslocamenteo entre series temporais)
 
 Sejam duas series x, y:
 $$
 DTW(x,y) = min_w[\sum_{k=1}^p\delta(w_k)]
 $$

Compara um ponto com varios outros pontos independente do tempo.  Criaa uma matriz de distancia, e então encontra a melhor distancia. 

Sejam duas series x,y, para computar o valor para a matriz utilizamos a seguinte formula:
$$
| x_i - y_j | + min( D[i-1, j-1], D[i-1, j], D[i, j-1])
$$

Procura pelos valores adjacentes para encontrar o melhor alinhamento. Quanto menor o valor de DTW mais proximas as series são, se o valor for 0, estamos comparando a mesma serie. 









- LB- Keogh - alternativa a DTW, que apesar de apresentar resultados muito bons, tem alto custo computacional. Uma restrição é que só pode ser aplicada a series de mesmo tamanho. 


- Edit distance on real sequence - EDR - baseada na distância de Levenshtein. Proposta para series temporais multivariadas, mas que pode ser usada em series univariadas. Não é sensivel a curvas com deslocamento entre si e também pode ser usada para curvas de tamanhos diferentes. 


- Dice, Jaccard e Lorentzian: aplicaveis apenas a series de mesmo tamanho

- Cosine: aplicavel apenas a series de mesmo tamanho
$$
dist(x,y) = 1 - \frac{x.y}{||x||_2||y||_2}
$$

Sendo $$||x||_2$$ a norma euclidiana do vetor x. 


- Mahalamanobis: 
$$
dist(x,y) =  \sqrt{(x-y)^TS^{-1}(x-y)}
$$

- Distâncias baseadas na correlação de Pearson:


#### Complex Invariant Distance - CID 

Tecnica utilizada para series com muitos picos e vales:

$$
dist_{CID} = dist_Q(x.y).CF(x.y)
$$

em que distQ(.) é qualquer uma das dissimilaridades já vistas e CF(.) é um fator de correção que leva conta uma estimativa da complexidade relativa entre series

$$
CF(x,y) = \frac{max(CE(x).CE(y))}{min(CE(x).CE(y))}
$$
em que CE(.) é um estimador de complexidade da serie temporal, por exemplo: Kolmogorov, entropia, núrmo de trocas do sinal da derivada. 









Refs: 
1 - https://www.ppgee.ufmg.br/defesas/964M.PDF