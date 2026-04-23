[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=23599173)
# Práctica 8

¡Adentrémonos en el increíble mundo del álgebra lineal numérica! OwO

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

Ejercicio 1: Cálculos con el polinomio característico
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

Ejercicio 2: El Método QR Simple
Programamos el método QR para calcular los eigenvalores de una matriz real A de tamaño nxn y suponiendo que la matriz A es simétrica.
Utilizamos la función `eigenvals` que recibe una matriz y un número de iteraciones. El método deberá regresar la matriz Ak después de las N iteraciones.





