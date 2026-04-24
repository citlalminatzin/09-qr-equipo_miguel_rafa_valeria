# Práctica 8

## Integrantes

- Domínguez León José Miguel
- Lazcano Flores Valeria
- Sánchez García Rafael

## Uso e instalación
Instalamos los paquetes en el siguiente orden:
-`collections`
-`numbers`
Ejecutamos de la siguiente manera:
- gram_schmidt.py: Calcula la factorización de gram-schmidt para una matriz de tamaño nxn
- qr.py: 
Realiza la factorización QR de una matriz M.
 
    Q: matriz cuyas columnas son los vectores ortonormales (unitaria)
    R: matriz triangular superior
 
    Idea:
      - Las columnas de M son los vectores que le pasamos a Gram-Schmidt
      - Gram-Schmidt nos devuelve columnas ortonormales → esas forman Q
      - R se obtiene como $$Q^T * M  (porque A = QR  =>  Q^T A = Q^T QR = IR = R)$$
- linear_solve.py: soluciona el sistema de ecuaciones lineales Ax = b 
- eigenvalues.py: 
    Realiza n iteraciones del algoritmo QR para calcular
    los eigenvalores de A

    Cada iteración:
     1. Factorizamos $$A^{k-1}= Q * R$$
     2. Calculamos $$A^{k}= R* Q $$   ← ojo: orden invertido

    La matriz $$A^{k}$$ converge a una matriz (casi) diagonal
    donde cada entrada $$A[i][j]$$ es un eigenvalor

    Devuelve la estimación de los eigenvalores
- main.py: resuelve los ejercicios 1, 2, 3.


## Ejercicios 

En esta práctica implementamos métodos fundamentales del álgebra lineal que permiten transformar matrices y el cálculo de sus eigenvalores.

### Ejercicio 1: Cálculos con el Polinomio Característico 
Por medio del método del polinomio característico, calculamos los eigenvalores de la siguiente matriz

$$
A =
\begin{bmatrix}
5 & -2  \\
-2 & 8 
\end{bmatrix}
$$

Calculamos el polinomio característico de la matriz mediante la función: `polinomio_caracteristico_2x2`
Posteriormente calculamos el determinante de dicho polinomio mediante la función:
`discriminante`
Obtenemos las raíces del polinomio característico mediante la función:
`formula_cuadratica`, y obtenemos dichos eigenvalores.


### Ejercicio 2: El Método QR Simple
Programamos el método QR para calcular los eigenvalores de una matriz real $A$ de tamaño n×n, suponiendo que la matriz $A$ es simétrica.

Utilizamos la función `eigenvals` que recibe una matriz y un número de iteraciones $N$. El método regresa la matriz $A^k$ después de las $N$ iteraciones, extrayendo los eigenvalores de su diagonal.

El algoritmo QR simple es el siguiente:

- **Inicialización:** $A_0 = A$, factorizamos $A_0 = Q_0 R_0$
- **Iteración $m$:** $A_m = R_{m-1} Q_{m-1}$, factorizamos $A_m = Q_m R_m$

Conforme $m$ crece, los valores en la diagonal de $A_m$ se aproximan a los eigenvalores de $A$.

Con **10 iteraciones** sobre la matriz del Ejercicio 1, se comparan los eigenvalores obtenidos con los exactos calculando el error absoluto $|\lambda_{\text{exacto}} - \lambda_{\text{QR}}|$.

### Ejercicio 3: El Método QR con Control de Precisión

Extendemos el método QR agregando un criterio de parada basado en una tolerancia $\varepsilon$: el algoritmo detiene las iteraciones cuando todos los elementos fuera de la diagonal de $A^k$ son menores que $\varepsilon$.

La función `eigen_epsilon` recibe:
- Matriz $A$ cuadrada y simétrica
- Número máximo de iteraciones $N$
- Tolerancia $\varepsilon$ (precisión deseada)

Y devuelve la matriz $A^k$ una vez que los valores fuera de la diagonal son menores que $\varepsilon$, o bien cuando se alcanza el número máximo de iteraciones.

Probamos con la matriz del Ejercicio 1, tolerancia $\varepsilon = 1 \times 10^{-10}$ y $N = 1000$ iteraciones. La diagonal de la matriz resultante coincide con los eigenvalores del Ejercicio 1:

$$
\text{diag}(A^k) \approx [\lambda_1,\ \lambda_2] = [4.0,\ 9.0]
$$




