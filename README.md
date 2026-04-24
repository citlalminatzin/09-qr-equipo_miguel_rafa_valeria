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

## Introducción

En esta práctica implementamos el método QR para el cálculo de eigenvalores de matrices cuadradas reales. Los eigenvalores son uno de los conceptos más importantes del álgebra lineal, ya que describen el comportamiento de una transformación lineal sobre un espacio vectorial. Formalmente, dado un vector no nulo $v$ y una matriz $A$, decimos que $\lambda$ es un eigenvalor de $A$ si se cumple $Av = \lambda v$, es decir, la transformación únicamente escala al vector $v$ sin cambiar su dirección.

El cálculo de eigenvalores tiene aplicaciones en una enorme variedad de áreas: en física describe los modos normales de vibración de un sistema; en ingeniería se usa para el análisis de estabilidad de estructuras; en ciencias de la computación es la base del algoritmo PageRank de Google y de técnicas de compresión como PCA (Análisis de Componentes Principales); y en aprendizaje automático aparece en métodos de reducción de dimensionalidad y en el análisis espectral de grafos.

Para matrices pequeñas, los eigenvalores pueden calcularse de forma exacta resolviendo el polinomio característico $\det(A - \lambda I) = 0$. Sin embargo, para matrices grandes este enfoque es impráctico, ya que resolver un polinomio de grado $n$ es numéricamente inestable y computacionalmente costoso. Es aquí donde los métodos iterativos como el método QR cobran relevancia.

El método QR se basa en la factorización de una matriz $A$ como producto de una matriz ortogonal $Q$ y una matriz triangular superior $R$, de forma que $A = QR$. A partir de esta factorización se construye una sucesión de matrices similares entre sí que convergen a una forma triangular (o diagonal, si la matriz es simétrica), revelando los eigenvalores en la diagonal. En esta práctica partimos del cálculo analítico mediante el polinomio característico como referencia exacta, implementamos el método QR simple con un número fijo de iteraciones y finalmente lo extendemos con un criterio de parada basado en tolerancia para tener control sobre la precisión del resultado.



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

## Conclusiones

El método QR demostró ser una herramienta efectiva y confiable para el cálculo iterativo de eigenvalores. A lo largo de los tres ejercicios pudimos comparar el resultado analítico exacto obtenido mediante el polinomio característico con las aproximaciones sucesivas del método numérico, observando lo siguiente:

- El método converge rápidamente para matrices simétricas, en concordancia con el teorema QR: con apenas 10 iteraciones el error absoluto es prácticamente cero para la matriz trabajada.
- El criterio de tolerancia $\varepsilon$ del Ejercicio 3 ofrece un control más fino de la precisión sin necesidad de fijar el número de iteraciones de antemano, lo que lo hace más flexible que el método simple del Ejercicio 2.
- La factorización QR construida a partir de Gram-Schmidt funciona correctamente como bloque base del algoritmo iterativo, validando también la implementación de la práctica anterior.

En conjunto, esta práctica ilustra cómo un método numérico iterativo puede alcanzar la misma precisión que un cálculo analítico, con la ventaja de ser generalizable a matrices de cualquier tamaño donde el polinomio característico no es práctico de resolver directamente.


