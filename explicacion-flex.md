# Explicación del comportamiento Flex en el NAV

## Datos de partida

- Ancho del contenedor (nav): **1200 px**
- `flex-basis` inicial de **todos** los botones: **241 px** (igual para todos)

---

## index.html — NAV con 4 botones (`nav-4`)

### Cálculo del espacio sobrante

```
4 botones × 241 px = 964 px
Espacio sobrante: 1200 - 964 = 236 px
```

Los 4 botones juntos no llenan el nav; **sobran 236 px**.

### Cómo se reparte el sobrante con `flex-grow`

| Botón     | flex-grow | Partes del sobrante | Px extra | Ancho final |
|-----------|-----------|---------------------|----------|-------------|
| Inicio    | 3         | 3/6 del sobrante    | 118 px   | ≈ 359 px    |
| Nosotros  | 1         | 1/6 del sobrante    |  39 px   | ≈ 280 px    |
| Servicios | 1         | 1/6 del sobrante    |  39 px   | ≈ 280 px    |
| Productos | 1         | 1/6 del sobrante    |  39 px   | ≈ 280 px    |

**Total de partes:** 3 + 1 + 1 + 1 = 6

`flex-grow: 3` en "Inicio" hace que absorba el triple del espacio sobrante que
cada uno de los demás botones. Así se consigue que "Inicio" sea visiblemente
más ancho sin cambiar su `flex-basis`.

---

## index2.html — NAV con 5 botones (`nav-5`)

### Cálculo del espacio en déficit

```
5 botones × 241 px = 1205 px
Déficit: 1205 - 1200 = 5 px
```

Los 5 botones se pasan en 5 px; hay que **encoger**.

### Cómo se reparte el encogimiento con `flex-shrink`

Todos los botones tienen `flex-shrink: 1` (el mismo valor), por lo que el
déficit se distribuye de forma proporcional e igual entre los cinco.

| Botón     | flex-shrink | Reducción | Ancho final |
|-----------|-------------|-----------|-------------|
| Inicio    | 1           | 1 px      | 240 px      |
| Nosotros  | 1           | 1 px      | 240 px      |
| Servicios | 1           | 1 px      | 240 px      |
| Productos | 1           | 1 px      | 240 px      |
| Contacto  | 1           | 1 px      | 240 px      |

**5 × 240 px = 1200 px** → encajan exactamente en el contenedor.

Se podría haber hecho que solo algunos botones encogiesen (asignando
`flex-shrink: 0` a los que deben mantener su tamaño y un valor mayor en los
que deben ceder más espacio). En este caso se eligió repartir el encogimiento
de forma uniforme.

---

## Media queries

| Breakpoint    | Qué cambia                              | Por qué                                                                 |
|---------------|-----------------------------------------|-------------------------------------------------------------------------|
| max-width: 1200px | `.contenedor` pasa de 1200px a 100% | Evita scroll horizontal en pantallas más estrechas que el diseño fijo   |
| max-width: 768px  | `main` elimina su `margin-left`     | Sin espacio suficiente, el aside flotado desplazaría el contenido fuera |
