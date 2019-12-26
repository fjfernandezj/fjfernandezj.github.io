---
layout: post
title: Introducción a la Econometría con WooldRige
subtitle: Primer post
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [econometrics, R]
comments: true
---

# Análisis de Regresión con datos de corte transversal Simple

## El modelo de regresión Simple

### Ideas claves
* El modelo de regresión simple puede utilizarse para estudiar la relación entre dos variables

* Se parte de la premisa que **_y_** y **_x_** son dos variables que representan a una población se desea "explicar **_y_** en términos de **_X_**"

- Un modelo que "explique **_y_** en términos de **_x_**" se establece a través de la ecuación:


$$
\begin{align*}
  & y = \beta_0 + \beta_1x + u
\end{align*}
$$

* La ecuación $\eqref{eq:lm}$ define el modelo de regresión lineal simple.

* La variable $u$, llamada **término de error**, o **perturbación** en la relación, representa factores distintos a $x$ que afectan a $y$.  

* La ecuación $\eqref{eq:lm}$ también resuelve le problema de la relación funcional entre $y$ y $x$. Si los demás factores en $u$ permanecen constantes,de manera que el cambio en $u$ sea cero, $\Delta u = 0$, entonces $x$ tiene un efecto lineal sobre $y$:

$$
\begin{equation}
\Delta y = \beta_1 \Delta x  si  \Delta u = 0
\label{eq:Du}
\tag{2}
\end{equation}
$$
* Por tanto, el cambio en $y$ es simplemente $\beta_1$ multiplicado por el cambio en $x$. Esto significa $\beta_1$ es el **parámetro de la pendiente** en la relación entre $y$ y $x$, cuando todos los demás factores en $u$ permanecen constantes.

* La linealidad de la ecuación $\eqref{eq:lm}$ implica que todo cambio de $x$ en una unidad tiene siempre el mismo efecto sobre $y$, sin importar el valor inicial de $x$.

## Obtención de las estimaciones de mínimos ordinarios
* Para esimar los parámetros $\beta_0$ y $\beta_1$ de la ecuación $\eqref{eq:lm}$ se necesita tomar una muestra de la población. Sea ${(x_i,y_i):i=1,...,n}$ una muestra aleatoria de tamaño $n$ tomada de la población. De esta muestra aleatoria de $y$ y $x$, de acuerdo a Wooldrige (2016, sección 2.2), las estimaciones de mínimos cuadrados ordinarios (OLS) son:

$$
\begin{equation}
\hat{\beta_0} = \hat{y} - \hat{\beta_1} \hat{x}  
\label{eq:beta0}
\tag{3}
\end{equation}
$$
$$
\begin{equation}
\hat{\beta_1} =  {COV(x,y) \over VAR(x)}  
\label{eq:beta1}
\tag{4}
\end{equation}
$$

* Basado en estos parámetros estimados, la linea de regresión de Mínimos Cuadrados Ordinarios es:

$$
\begin{equation}
\hat{y}  = \hat{\beta_0} + \hat{\beta_1} \hat{x}  
\label{eq:ols}
\tag{5}
\end{equation}
$$
Para una muestra dada, solo necesitamos calcular los cuatro estadisticos $\hat{y}$, $\hat{x}$, $Cov(x,y)$, y $Var(x)$ e insertarlas en las ecuaciones anteriores. 

A continuación veremos 3 ejemplos de regresión simple obtenidos empleando datos reales. Hay que tener ojo de que estas no necesariamente implican una relación causal. Para esto luego veremos las propiedades estadísticas de los estimadores de MCO. 

### Ejemplo 2.3 Sueldo de los Directores Generales (CEO) y rendimiento sobre el capital
En la población de los directores generales, sea $y$ el sueldo (salary) en miles de dolares. De manera que $y = 856.3$ corresponde a un suelo anual de 856,300 y $y = 1,452.6$ corresponde a un sueldo de 1,452,600. Sea $x$ el promedio, en los últimos tres años, del rendimiento sobre el capital (roe) en las empresas de los CEO. (El rendimiento sobre el capital se define en términos de utilidad neta como porcentaje de acciones comunes.) Por ejemplo, si $roe = 10$, el rendimiento promedio sobre el capital es 10 por ciento. 

Para analizar esto se utiliza la base de datos CEOSAL1.dta, la cual contiene información correspondiente al año 1990, sobre 209 CEO; estos datos fueron obtenidos de *Business Week* (5/6/91). En esta muestra, el sueldo anual promedio es 1,281,120, y los sueldos menor y mayorson 223,000 y 14,822,000, respectivamente. La media del rendimiento sobre capital en 1988, 1989 y 1990 es 17.18% y los valores menor y mayor son 0,5 y 56.3%, respectivamente. 

Para estudiar la relación entre esta medida del desempeño de una empresa y el pago que reciben los CEO, se postula el modelo

$$
\begin{equation}
salary  = \beta_0 + \beta_1 roe + u  
\label{eq:Ex2.3}
\tag{6}
\end{equation}
$$
En el siguiente script se calculan los 4 estadisticos que se necesitan para las ecuaciones $\eqref{eq:beta0}$ y $\eqref{eq:beta1}$ de manera que se puedan calcular manualmente las formulas de OLS
```javascript
library(foreign)

ceosal1 <- read.dta("data/ceosal1.dta")

#Ingredientes para las formulas de OLS
cov(ceosal1$roe, ceosal1$salary)

var(ceosal1$roe)

mean(ceosal1$salary)

mean(ceosal1$roe)

# Calculo manual de coeficientes de OLS
(b1hat <- cov(ceosal1$roe,ceosal1$salary)/var(ceosal1$roe))

(b0hat <- mean(ceosal1$salary) - b1hat*mean(ceosal1$roe))

# Calculo automático a través de comando lm (linear model)
lm(ceosal1$salary ~ ceosal1$roe)
```

De esta manera la linea de regresión MCO (luego del calculo del intercepto y la pendiente) que relaciona sueldo (salary) y rendimiento sobre capital (roe)

$$
\begin{equation}
\hat{salary}  = 963.2 + 18.5roe + u  
\label{eq:Ex2.3_res}
\tag{7}
\end{equation}
$$
¿Cómo se interpreta esta ecuación?
Primero, si el rendimiento sobre el capital es 0, $roe = 0$, entonces el sueldo que se predice corresponde al intercepto, 963.191, es decir, 963,191, dado que salary se mide en miles. Luego, el cambio que se predice para el sueldo en función del cambio en el roe se exresa como $\Delta\hat{salary}=18,501$ ($\Delta roe$). Esto significa que cuando el rendimiento sobre el capital aumente en un punto porcentual, $\Delta roe = 1$, se predice que el sueldo variará aproximadamente en 18.5, es decir, 18,500. 

En el siguiente script se puede ver como guardar los resultados de la regresión en una variable CEOregress y luego usarla como un argumento para el comando **abline** para agregar una linea de regresion a un gráfico de puntos 

```javascript
#Regresion de MCO
CEOregres <- lm(ceosal1$salary ~ ceosal1$roe)

#Scatter plot (grafico de puntos) --> restringiendo eje y
plot(ceosal1$roe, ceosal1$salary, ylim = c(0,4000))

# Agregar linea de regresión
abline(CEOregres)
```

## Ejemplo 2.4 Salario y Educación
Para la población de personas en la fuerza de trabajoen 1976, sea $y = wage (salario)$, donde $wage$ se mide en dólares por hora. Entonces, si para una determinada persona $wage = 6.75$, significa que su salario por hora es 6.75 dolares. Sea $x = educ$ años de educación; por ejemplo, $educ = 12$ corresponde a haber terminado el bachillerato. Como el salario promedio de la muestra es 5,90 dolares, el índice de precios al consumidor indica que esta cantidad es equivalente a 19,06 dolares de 2003.

Utilizando la base de datos *WAGE1.dta*. estudiaremos la relacion entre educación y salario, siendo nuestro modelo de regresión: 
$$
\begin{equation}
wage  = \beta_0 + \beta_1 education + u
\label{eq:wage01}
\tag{8}
\end{equation}
$$
En el siguiente script analizaremos los datos:

```javascript
library(foreign)

wage1 <- read.dta("data/wage1.dta")

# regresión MCO
lm(wage1$wage ~ wage1$educ)

```

Se obtiene la siguiente linea de refresión de MCO (o función de regresion muestral) ($n = 526$):

$$
\begin{equation}
\hat(wage)  = -0.90 + 0.54 education 
\label{eq:wage02}
\tag{9}
\end{equation}
$$
El intercepto -0.90 significa literalmente que para una persona sin ninguna educación el sueldo por hora que se predice es -90 centavos por hora (lo cual no tiene sentido). Por eso ojo con la interpretación de este resultado. Esta linea de regresión no es adecuada para niveles de educación muy bajos.

Por otro lado la pendiente estimada de la ecuación $\eqref{eq:wage02}$ implica que un año adicional de educación hace que el salario por hora aumente 54 centavos por hora.

## Ejemplo 2.5 Resultados de una votación y gastos de campaña
La siguiente base de datos a analizar contiene información en gastos de campaña y los resultados de campañacorrespondientes a 173 contiendas bipartidistas por la càmara de Representantes de Estos Unidos , en 1988.

En la base de datos, en cada contienda hay dos candidatos, A y B. Sea *voteA* el porcentaje de votos obtenido por el candidato A y *shareA* el porcentaje del total de los gastos de campaña atribuidos al candidato A. El modelo de regresión 

$$
\begin{equation}
voteA  = \beta_0 + \beta_1 shareA + u
\label{eq:vote01}
\tag{10}
\end{equation}
$$

Es estimado en el siguiente script:

```javascript
library(foreign)

vote1 <- read.dta("data/vote1.dta")

# regresión MCO
(VOTEres <- lm(vote1$voteA ~ vote1$shareA) )

# grafico de dispersión con línea de regresión
plot(vote1$shareA, vote1$voteA)
abline(VOTEres)
```

La regresión de MCO resultó ser:

$$
\begin{equation}
\hat(voteA)  = 26.81 + 0.464 shareA 
\label{eq:vote02}
\tag{11}
\end{equation}
$$

## Propiedades de MCO en cualquier muestra de datos
### Coeficientes, valores ajustados y residuales

En esta sección se verán otras propiedades algenraicas de  la línea de regresión ajustada de MCO. Varias de la propiedades pueden parecer muy simples. Sin embargo, entenderlas ayudará a comprender lo que pasa con las estimaciones de MCO y con los los estadísticos con ellos relacionados al manipular los datos de ciertas maneras (por ejemplo cambiando las unidades de medida de variables dependientes e independientes).

Se supone que las estimaciones del intercepto y la pendiente,  $\hat{\beta_0}$ y $\hat{\beta_1}$, han sido obtenidas para los datos muestreales dados. Una vez que se tienen $\hat{\beta_0}$ y $\hat{\beta_1}$, se puede obtener el valor ajustado $\hat{y_i}$ correspondiente a cada observación ($\eqref{eq:ols}$). Por definición todos los valores ajustados $\hat{y_i}$       
