# Questão 1

## Letra a )

A questão já nos define que $Q_v = I - \beta vv^*$ e $Q_vx = \| x \| e_1$. Vamos analisar, agora, o que é pedido. Primeiramente, vamos verificar que $v = x - \|x \| e_1$,

$$ Q_vx = \| x \| e_1 $$
$$ (I - \beta vv^*) x = \| x \| e_1 $$
$$ \beta v(v^* x) = x - \| x \| e_1 $$
$$  v =  \frac{x -\| x \| e_1}{\beta (v^* x)} $$

Como $\beta$ é uma constante qualquer, podemos definir nesse caso, sem perda de generalidade, $\beta = \frac{1}{(v^* x)}$, e portanto

$$ v = x - \| x \| e_1$$

$$ v = \begin{bmatrix} x_1 - \| x \| \\ x_2 \\ \vdots \\ x_n\end{bmatrix}$$

Agora, vamos verificar quem é $\beta$,  primeiramente, vamos dar uma olhada em $v^*x$. Podemos perceber que todas as entradas de $v$ são idênticas a de $x$, a menos da primeira, que é $x_1 - \| x \|$. Logo o produto interno $v^*x$ pode ser definido como 

$$ (x_1 - \| x \|)x_1 + \sum_{i = 2}^{n}x_i^2$$
$$ = \sum_{i = 1}^{n}x_i^2 - \|x\|x_1$$
$$=  \| x \|^2 - \|x\|x_1 $$
$$= \|x\|(\|x\| - x_1)$$
$$ \Longrightarrow \beta = \frac{1}{\|x\|(\|x\| - x_1)}$$

Portanto, a primeira igualdade de $\beta$ pedida pela questão foi provada, verifiquemos as outras

$$ \beta =  \frac{(\|x\| + x_1)}{\|x\|(\|x\| - x_1)(\|x\| + x_1)} = \frac{(\|x\| + x_1)}{\|x\|(\|x\|^2 - x_1^2)}$$

Sabemos que $\|x\|^2 = \sum_{i = 1}^{n}x_i^2 \Longrightarrow \|x\|^2  - x_1^2= \sum_{i = 2}^{n}x_i^2 = \|y\|^2$, como $y$ é definido pela questão, assim

$$\beta = \frac{(\|x\| + x_1)}{\|x\|\|y\|^2} $$

## Letra b )

Vamos verificar que alterações o sinal de $x_1$ pode provocar nas fórmulas para $\beta$, ou seja, segundo o informado pela questão, em qual das fórmulas estamos sujeitos a cancelamento numérico a depender do sinal de $x_1$, acredito que seja um pouco mais fácil de compreender através de como o $\textit{Trefethen}$ explica isso

Pelo que entendemos, o que queremos evitar aqui é o problema evitado por $\textit{Trefethen}$ ao selecionar $v$ como 

$$ v = sign(x_1)\|x\|e_1 + x$$

Ele faz isso para que $\|v\|$ seja a maior possível. Vamos identificar isso na prática, o que a formulação dele mudaria para nós é que

$$ v = \begin{bmatrix} x_1 + sign(x_1) \| x \| \\ x_2 \\ \vdots \\ x_n\end{bmatrix}$$

Ou seja, o que queremos evitar é a subtração entre $x_1$ e $\|x\|$.

1) Na primeira fórmula $$\beta = \frac{1}{\|x\|(\|x\| - x_1)}$$ temos a subtração $(\|x\| - x_1)$ que nos é favorável quando o sinal de $x_1$ é negativo, resultando na soma entre os dois termos.

2) Podemos identificar que na segunda fórmula, $$\frac{(\|x\| + x_1)}{\|x\|(\|x\|^2 - x_1^2)}$$ encontramos esse problema bem presente, já que independentemente do sinal de $x_1$ estamos sujeitos a esse erro por conta de $(\|x\|^2 - x_1^2)$.

3) Na terceira fórmula, $$\beta = \frac{(\|x\| + x_1)}{\|x\|\|y\|^2} $$ podemos perceber que $(\|x\| + x_1)$ nos é favorável quando o sinal de $x_1$ é positivo.

## Letra c )

A função criada implementa a lógica formalizada pelas questões acima para calcular os parâmetros e $v$ e $\beta$ dos refletores

## Letra d )

Consideremos $v$ como foi definido pela questão como uma função vetorial $v(x) = x - \|x\|e_1$, dessa forma, vamos calcular sua derivada em relação a $x$. Com $x$ tendo cada uma de suas entradas independentes, o que queremos calcular aqui é então a matriz Jacobiana

$$ J(v) = \begin{bmatrix} 
        \frac{\partial v_1}{\partial x_1} & \dots & \frac{\partial v_1}{\partial x_n} \\ 
        \vdots                            & \ddots&         \vdots                     \\ 
        \frac{\partial v_n}{\partial x_1} & \dots & \frac{\partial v_n}{\partial x_n}
        \end{bmatrix} $$

Para calcularmos, sabemos que 

$$ v = \begin{bmatrix} x_1 - \| x \| \\ x_2 \\ \vdots \\ x_n\end{bmatrix}$$

E portanto, vamos analisar cada entrada:

$$ \frac{\partial v_i}{\partial x_j} = 
\left\{
\begin{aligned}
1, \quad \text{se } i = j \\
0, \quad \text{se } i \neq j
\end{aligned}

\quad

\right. 

\text{para } i, j= 2, \dots,n$$

Vamos, agora, analisar as derivadas parciais de $v_1$ com relação as entradas de $x$, que sabemos que será da forma 

$$ \frac{\partial v_1}{\partial x_i} = \frac{x_1 - \| x \|}{\partial x_i} = \frac{x_1}{\partial x_i} - \frac{\| x \|}{\partial x_i} \quad \text{para } i = 1,\dots,n$$

Sabemos que 
$$ \frac{x_1}{\partial x_i} = 
\left\{
\begin{aligned}
1, \quad \text{se } i = j \\
0, \quad \text{se } i \neq j
\end{aligned}

\right.
\quad
\text{para } i= 1, \dots,n$$

$$\|x\| = \sqrt{\sum_{i=1}^{n}x_1^2}, \quad y = \sum_{i=1}^{n}x_1^2  \Longrightarrow   \frac{\|x\|}{\partial x_i} = \frac{\partial \|x\|}{\partial y} \frac{\partial y}{\partial x_i} = \frac{1}{ 2\sqrt{y}} 2 x_i = \frac{\partial x_1}{\|x\|}$$

Portanto, nossa matriz se torna 

$$ J(v) = \begin{bmatrix} 
        1 -  \frac{\partial x_1}{\|x\|}& - \frac{\partial x_2}{\|x\|} & \dots & - \frac{\partial x_n}{\|x\|}\\ 
                                  & 1 &                      &        \\ 
          &  & \ddots &  \\
          &  & & 1
        \end{bmatrix}_{n \times n}
        
= I_{n \times n} + \begin{bmatrix} 
        -\frac{\partial x_1}{\|x\|} & \dots & -\frac{\partial x_n}{\|x\|}\\ 
           \\
          & 0_{(n -1) \times n} \\
           \\
        \end{bmatrix}_{n \times n}
        
= I + e_1 \frac{x^*}{\|x\|}$$

Sabemos que o condicionamento absoluto de uma função $f$ é dado em termos de sua matriz Jacobiana, assim

$$ k =  \|J\| = \| I + e_1 \frac{x^*}{\|x\|}\| \leq  \| I \| +  \| e_1 \frac{x^*}{\|x\|}\| = 1 + \frac{1}{\|x\|}\|e_1x^*\| = 1 +  \frac{1}{\|x\|}\|e_1\|\|x\|$$
Como $\|e_1\| = 1$, então

$$ k \leq 1+ \frac{\|x\|}{\|x\|} = 2$$

## Letra e )

Como requisitado pela questão faremos testes com vetores $x$ com entradas aleatórias nos tipos $\textit{Float32}$ e $\textit{Float64}$


## Letra f ) 

Sabemos que a matriz $Q_v$ não está definida como normalmente. $\textit{Trefthen}$ define $Q_v = I - 2\frac{vv^*}{v^*v}$, portanto, $\beta$ em função apenas de $v$ é

$$ \beta =  \frac{2}{v^*v} $$

## Letra g )

Temos que o condicionamento relativo de um problema tem a seguinte fórmula:
$$
k = \hat{k} \frac{\Vert x \Vert}{\Vert v \Vert}
$$
Onde $\hat{k}$ é o condicionamento absoluto. Em paralelo temos:
$$
v = x - \Vert x \Vert e_1 = \begin{bmatrix}x_1 - \Vert x \Vert  \\ x_2 \\ \vdots \\ x_n \end{bmatrix}
$$
Disso conseguimos deduzir:
$$
\Vert v \Vert^2 = (x_1 - \Vert x \Vert)^2 + \sum^n_{i=2} x^2_i = x_1^2 - 2x_1 \Vert x \Vert + \Vert x \Vert^2 + \sum^n_{i=2} x^2_i
$$
Agregando o somatório a $x_1$: 
$$
\Vert v \Vert^2 = - 2x_1 \Vert x \Vert + \Vert x \Vert^2 + \Vert x \Vert^2 = 2 \Vert x \Vert (\Vert x \Vert - x_1)
$$
Substituindo o resultado encontrado na fórmula do condicionamento encontramos o seguinte resultado:
$$
k = \hat{k} \frac{\Vert x \Vert}{\sqrt{2 \Vert x \Vert (\Vert x \Vert - x_1)}}
$$
Portanto, quanto mais x se aproxima de $e_1$ o denominador da expressão encontrada tende a zero e portanto o condicionamento
explode.

Uma boa fórmula para $v$ que mitiga o problema do condicionamento afetado pela proximidade de $x$ a $e_1$ pode ser encontrada baseando-se
nos resultados obtidos no item b), onde definimos $v$ da seguinte maneira:
$$
v = x + sig(x_1) \Vert x \Vert e_1
$$

Já que assim o módulo de $x_1$ sempre estaria se distanciando de 0 e mantendo $x$ longe da direção de $e_1$ impedindo que o condicionamento exploda.


# Questão 2 

## Letra a )

Nesse caso, nós já conhecemos os parâmetros $v$ e $\beta$ dos refletores, assim, vamos verificar o que nós precisamos computar. Queremos calcular $$Q_vb = (I - \beta vv^*) b = b - \beta(v^*b) v = b - \alpha v$$

Para conseguirmos fazer o calculo com $v$ e $b$ de tamanhos diferentes vamos aplicar $v$ apenas na parte inferior correspondente de $b$ através da indexação

## Letra b )

## Letra c )

O que nós queremos fazer agora é generalizar nossa função criada acima para calcular as reflexões em uma matriz, dessa forma a operação será $$Q_v A = (I - \beta v v^*)A = A - \beta v(v^*A)$$

## Letra d )

A aplicação da da matriz $Q_v$ pela direita faz $$AQ_v = A(I - \beta vv^*) = A- \beta(Av)v^* $$

## Letra e )

## Letra f )

# Questão 3 

## Letra a)

Vamos analisar melhor o que é esse tipo de matriz que nos foi dada:

$$ A(w) = \begin{bmatrix} 0 & 1 \\ -w^2 & 0\end{bmatrix}$$

Primeiramente, dado que a letra c) pede para fazermos, vamos verificar o que acontece quando fazemos $A(w)^2$

$$ A(w)^2 = \begin{bmatrix} 0 & 1 \\ -w^2 & 0\end{bmatrix}\begin{bmatrix} 0 & 1 \\ -w^2 & 0\end{bmatrix} = \begin{bmatrix}  -w^2 & 0 \\ 0 &  -w^2\end{bmatrix} = -w^2I$$

O que conseguimos deduzir disso, à princípio é que seja $\lambda$ um autovalor de $A(w)$ e $v$ seu autovetor associado, então $$A(w)^2 v = \lambda^2v \Longrightarrow \lambda^2 = -w^2 \Longrightarrow \lambda_1 = \sqrt{-w^2} = iw \quad \text{e} \quad \lambda_2 = - \sqrt{-w^2} = -iw $$

Ou seja, nossos autovalores só possuem a parte complexa.

Vamos encontrar nossos autovetores, sabemos que $(A - \lambda I)v = 0$, assim

$$ \begin{bmatrix} -\lambda & 1 \\ -w^2 & -\lambda\end{bmatrix} \begin{bmatrix} v_1 \\ v_2\end{bmatrix} = \begin{bmatrix} 0 \\ 0\end{bmatrix} \Longrightarrow v_2 = iwv_1 \quad \text{ou} \quad v_2 = -iwv_1$$

Dessa forma, $$ v_1 = \begin{bmatrix} 1 \\ iw\end{bmatrix} \quad v_2 = \begin{bmatrix} 1 \\ -iw\end{bmatrix}  $$

A partir dessas conclusões, podemos esperar que com $ w \rightarrow 0^+ $ nossos autovalores $|\lambda_1| , |\lambda_2| \rightarrow 0$ e nossos autovetores $v_1, v_2 \rightarrow \begin{bmatrix} 1 \\ 0\end{bmatrix}$. Vamos verificar em código,

## Letra b )

Fazendo os cálculos, basicamente, verificando $A^*A$, encontrando os valores singulares, verificando que $V=I$, encontrando $U$, chegamos à conclusão de que a SVD de $A(w)$ é

$$ A(w) = \begin{bmatrix} 0 & 1 \\ -1 & 0\end{bmatrix} \begin{bmatrix} w^2 & 0 \\ 0 & 1\end{bmatrix} \begin{bmatrix} 1 & 0 \\ 0 & 1\end{bmatrix}$$

Sabemos que $$k(A) = \frac{\sigma_{max}}{\sigma_{min}}$$

Logo, como $w^2 \leq 1$ para $w \in [0,1]$, então temos que $$k(A) = \frac{1}{w^2}$$

## Letra c )

Primeiramente vamos demonstrar $A(\omega)^2 = - \omega I $:

$$
A(\omega)^2 = \begin{bmatrix} 0 & 1 \\ -\omega^2 & 0 \end{bmatrix}
\begin{bmatrix} 0 & 1 \\ -\omega^2 & 0 \end{bmatrix}

= \begin{bmatrix} -\omega^2 & 0 \\ 0 & -\omega^2 \end{bmatrix}
= -\omega^2 \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}
= -\omega^2 I
$$

E para a dedução, sabems que:
$$
e = \sum_{i=0}^{\infty} \frac{x^n}{n!}
$$
E portanto:
$$
e^{t A(\omega)} = \sum_{i=0}^{\infty} \frac{(t A(\omega))^n}{n!}
$$
Abrindo nós obtemos:
$$
e^{t A(\omega)} = \frac{(t A(\omega))^0}{0!} + \frac{(t A(\omega))^1}{1!} + \frac{(t A(\omega))^2}{2!} + \frac{(t A(\omega))^3}{3!} + ...
= I + t A(\omega) - \frac{t^2  \omega^2 I}{2!} - \frac{t^3  \omega^2 A(\omega)}{3!} + ...\\
$$
Dividindo os termos de expoente ímpar por $\omega$:
$$
e^{t A(\omega)} = I + \frac{t A(\omega)}{\omega} - \frac{t^2  \omega^2 I}{2!} - \frac{t^3  \omega^3 A(\omega)}{3! \omega} + ...\\
$$
Chegamos a dois somatórios um para os termos de grau ímpar e outro para termos de grau par:
$$
e^{t A(\omega)} = \sum_{i=0}^{\infty} \frac{(-1)^n}{(2n)!} (\omega t)^{2n} I + \sum_{j=0}^{\infty} \frac{(-1)^n}{(2n + 1)!} (\omega t)^{2n + 1} A(\omega)
$$
Analisando as parcelas dessa soma conseguimos enxergar as semelhanças desses somatórios com as séries de taylor refentes ao cosseno e seno, respectivamente:

$$
\cos{x} = \sum_{i=0}^{\infty} \frac{(-1)^n}{(2n)!} (x)^{2n} 
$$
$$
\sin{x} = \sum_{j=0}^{\infty} \frac{(-1)^n}{(2n + 1)!} (x)^{2n + 1}
$$

Multiplicados por $ I $ e $A(\omega)$ nessa ordem. Por fim, chegamos em:
$$
e^{t A(\omega)} = \cos{(\omega t)} I + \frac{\sin{\omega t}}{\omega} A(\omega)
$$
**Como queriamos demonstrar.**

Quando $\omega \rightarrow 0^+$:

$$
\lim_{\omega \rightarrow 0^+} \cos{(\omega t)} I + \frac{\sin{\omega t}}{\omega} A(\omega)
$$
$$
= \cos{(0)} I + \lim_{\omega \rightarrow 0^+} \begin{bmatrix}0 & \frac{\sin{\omega t}}{\omega}
\\ -\omega \sin{\omega t} & 0\end{bmatrix}
= I + \begin{bmatrix} 0 & t \\ 0 & 0 \end{bmatrix}
= \begin{bmatrix} 1 & t \\ 0 & 1 \end{bmatrix}
$$
Verificando os somatórios:
$$
\lim_{\omega \rightarrow 0^+} e^{t A(\omega)} = I + \begin{bmatrix} 0 & t \\ 0 & 0 \end{bmatrix} + \sum_{i=2}^{\infty} \frac{(t A(0))^n}{n!} 
$$
Mas $A(0)$ é a matriz nilpotente e portanto os demais termos da soma serão iguais a zero:

$$
\lim_{\omega \rightarrow 0^+} e^{t A(\omega)} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} + \begin{bmatrix} 0 & t \\ 0 & 0 \end{bmatrix} + 0
= \begin{bmatrix} 1 & t \\ 0 & 1 \end{bmatrix}
$$

O que bate com o resultado que encontramos anteriormente.
