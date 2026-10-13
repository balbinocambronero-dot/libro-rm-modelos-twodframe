# Modelos TwoDFrame — Resistencia de Materiales

Modelos de cálculo para **TwoDFrame** (`.2df`) de los **110 ejercicios** del manual de Resistencia de Materiales de Balbino Cambronero Martínez (Universidad de Castilla-La Mancha, ETSII Albacete).

Con ellos se puede:

- **comprobar** con el ordenador las reacciones y los diagramas obtenidos a mano;
- **experimentar**: cambiar cargas, geometría, rigideces o vínculos y ver al instante cómo cambia la respuesta de la estructura;
- **aprender a modelar**, partiendo de un archivo de referencia por ejercicio.

**Descarga completa (ZIP):** [main.zip](https://github.com/balbinocambronero-dot/libro-rm-modelos-twodframe/archive/refs/heads/main.zip)

---

## Estructura del repositorio

```
libro-rm-modelos-twodframe/
├── bloque-01-vigas-isostaticas/                  (10 modelos)
├── bloque-02-cerchas-isostaticas/                (10 modelos)
├── bloque-03-vigas-inclinadas-isostaticas/       (10 modelos)
├── bloque-04-porticos-isostaticos/               (10 modelos)
├── bloque-05-marquesinas-isostaticas/            (10 modelos)
├── bloque-06-vigas-gerber/                       (10 modelos)
├── bloque-07-vigas-hiperestaticas/               (10 modelos)
├── bloque-08-porticos-hiperestaticos/            (10 modelos)
├── bloque-09-cerchas-hiperestaticas/             (10 modelos)
├── bloque-10-vigas-inclinadas-hiperestaticas/    (10 modelos)
├── bloque-11-porticos-de-naves-industriales/     (10 modelos)
├── resultados_reacciones.csv
├── esfuerzos_extremos_barra.csv
└── README.md
```

| Bloque | Contenido | Carpeta |
|:-:|---|---|
| 1 | Vigas isostáticas | [bloque-01](bloque-01-vigas-isostaticas) |
| 2 | Cerchas articuladas isostáticas | [bloque-02](bloque-02-cerchas-isostaticas) |
| 3 | Vigas inclinadas isostáticas | [bloque-03](bloque-03-vigas-inclinadas-isostaticas) |
| 4 | Pórticos isostáticos | [bloque-04](bloque-04-porticos-isostaticos) |
| 5 | Marquesinas isostáticas | [bloque-05](bloque-05-marquesinas-isostaticas) |
| 6 | Vigas continuas con rótulas (Gerber) | [bloque-06](bloque-06-vigas-gerber) |
| 7 | Vigas hiperestáticas | [bloque-07](bloque-07-vigas-hiperestaticas) |
| 8 | Pórticos hiperestáticos | [bloque-08](bloque-08-porticos-hiperestaticos) |
| 9 | Cerchas hiperestáticas | [bloque-09](bloque-09-cerchas-hiperestaticas) |
| 10 | Vigas inclinadas hiperestáticas | [bloque-10](bloque-10-vigas-inclinadas-hiperestaticas) |
| 11 | Pórticos de naves industriales | [bloque-11](bloque-11-porticos-de-naves-industriales) |

### Nombre de los archivos

Cada modelo se llama `Ej_BB-NN_título.2df`, donde **BB** es el número de bloque y **NN** el número de ejercicio dentro del bloque. Por ejemplo:

```
bloque-01-vigas-isostaticas/Ej_01-01_viga-biapoyada-con-carga-puntual-centrada.2df
```

corresponde al **ejercicio 1.1** del libro.

---

## Cómo abrir los modelos

1. Instale la **edición académica de TwoDFrame**, gratuita para uso no comercial: <https://www.ralfmartinhansen.de>. Los modelos se han comprobado con la versión **2026.000**.
2. Descargue el ZIP completo (enlace de arriba) o un modelo concreto: entre en la carpeta del bloque, abra el archivo y pulse el botón de descarga (*Download raw file*).
3. En TwoDFrame: **Archivo → Abrir** y seleccione el archivo `.2df`.
4. En la pestaña **Resultados**, elija en **Diagrama** el resultado deseado (reacciones, flectores, cortantes o axiles) y acepte el cálculo.
5. Compare con la solución del libro o con los CSV de este repositorio.

### Criterios de modelado

- **Unidades y ejes:** m, kN y kN·m. Eje X horizontal, positivo hacia la derecha; eje Z vertical, positivo hacia arriba. Nudos y barras llevan los mismos nombres que en el libro.
- **Vínculos:** las rótulas se modelan liberando el momento en el extremo de barra. El apoyo móvil sobre plano inclinado se representa con una biela perpendicular al plano de rodadura; su axil es la reacción normal. Los asientos se introducen como desplazamientos impuestos; en esos nudos el programa muestra el desplazamiento y la reacción se obtiene por equilibrio.
- **Cargas:** se respeta la definición del enunciado (por metro de barra, por proyección horizontal o perpendicular a la barra). El peso propio está desactivado.
- **Rigideces:** se emplean E, A e I del enunciado. Cuando el método manual supone barras axialmente indeformables, el modelo asigna un área muy grande para reproducir esa hipótesis; basta sustituirla por el área real para obtener la solución matricial completa y valorar la diferencia.

---

## Archivos CSV

Ambos usan **punto y coma (`;`) como separador** y **coma decimal**, por lo que se abren directamente en Excel o LibreOffice con configuración regional española.

### `resultados_reacciones.csv`

Reacciones de los 110 ejercicios (468 filas), contrastando la solución del libro con la de TwoDFrame.

| Columna | Significado |
|---|---|
| `Ejercicio` | Número de ejercicio en el libro (p. ej. `1.1`) |
| `Componente` | Reacción: nudo + dirección (`Ax`, `Ay`, `By`…) |
| `Libro [kN, kN·m]` | Valor obtenido en el libro |
| `TwoDFrame [kN, kN·m]` | Valor calculado con el modelo |
| `Coincide` | `sí` si la diferencia es ≤ 0,5 % o ≤ 0,02 kN |

**Verificación:** las 468 reacciones coinciden.

### `esfuerzos_extremos_barra.csv`

Esfuerzos en los dos extremos de todas las barras de los 110 modelos (610 filas), obtenidos con TwoDFrame.

| Columna | Significado |
|---|---|
| `Ejercicio` | Número de ejercicio en el libro |
| `Barra` | Nombre de la barra (nudo origen + nudo final, p. ej. `AB`) |
| `N origen`, `V origen`, `M origen` | Axil, cortante y flector en el extremo origen [kN, kN·m] |
| `N final`, `V final`, `M final` | Axil, cortante y flector en el extremo final [kN, kN·m] |

Los valores son los de los diagramas de esfuerzos en cada extremo (por ejemplo, en la viga del ejercicio 1.1 el cortante pasa de +20 kN en el origen a −20 kN en el final).

---

## Autor y referencia

**Balbino Cambronero Martínez** — Departamento de Mecánica Aplicada e Ingeniería de Proyectos, ETSII Albacete, Universidad de Castilla-La Mancha.

TwoDFrame: Hansen, R. M. (2026). *TwoDFrame*, edición académica. <https://www.ralfmartinhansen.de>
