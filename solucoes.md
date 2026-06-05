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

Vamos verificar que alterações o sinal de $x_1$ pode provocar nas fórmulas para $\beta$, ou seja, segundo o informado pela questão, em qual das fórmulas estamos sujeitos a cancelamento numérico a depender do sinal de $x_1$, acredito que seja um pouco mais fácil de compreender através de como o $\textit{Treften}$ explica isso

Pelo que entendemos, o que queremos evitar aqui é o problema evitado por $\textit{Treften}$ ao selecionar $v$ como 

$$ v = sign(x_1)\|x\|e_1 + x$$

Ele faz isso para que $\|v\|$ seja a maior possível. Vamos identificar isso na prática, o que a formulação dele mudaria para nós é que

$$ v = \begin{bmatrix} x_1 + sign(x_1) \| x \| \\ x_2 \\ \vdots \\ x_n\end{bmatrix}$$

Ou seja, o que queremos evitar é a subtração entre $x_1$ e $\|x\|$.

1) Na primeira fórmula $$\beta = \frac{1}{\|x\|(\|x\| - x_1)}$$ temos a subtração $(\|x\| - x_1)$ que nos é favorável quando o sinal de $x_1$ é negativo, resultando na soma entre os dois termos.

2) Podemos identificar que na segunda fórmula, $$\frac{(\|x\| + x_1)}{\|x\|(\|x\|^2 - x_1^2)}$$ encontramos esse problema bem presente, já que independentemente do sinal de $x_1$ estamos sujeitos a esse erro por conta de $(\|x\|^2 - x_1^2)$.

3) Na terceira fórmula, $$\beta = \frac{(\|x\| + x_1)}{\|x\|\|y\|^2} $$ podemos perceber que $(\|x\| + x_1)$ nos é favorável quando o sinal de $x_1$ é positivo.
