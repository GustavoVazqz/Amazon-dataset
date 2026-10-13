Amazon Sales: ¿los descuentos mejoran la satisfacción del cliente?

Proyecto de portafolio de Business Intelligence: limpieza y transformación en SQL (SQLite + DBeaver) y dashboard en Power BI para analizar la relación entre descuentos, rating y reviews por categoría de producto.

> Escenario simulado: los stakeholders y la empresa son ficticios; los datos son un dataset público de Kaggle.

![Dashboard](docs/img/dashboard.png)

**Dashboard:** [https://github.com/GustavoVazqz/Amazon-dataset/blob/main/Amazon%20Report.pbix] · **Documento completo del proyecto:** [https://github.com/GustavoVazqz/Amazon-dataset/blob/main/Proyecto%20BI%20Amazon.pdf]  (docs/Proyecto_BI_Amazon.docx)

## Objetivo de negocio

Identificar qué categorías combinan mejor descuento con mejor percepción de valor (rating) y cuáles reducen el margen sin mejorar la satisfacción, para orientar la estrategia de descuentos y de pricing del próximo trimestre.

## Preguntas de negocio

1. ¿En qué categorías se está perdiendo margen con descuentos que no mejoran la percepción del cliente?
2. ¿El nivel de descuento está asociado con mejor o peor rating, y varía esta relación entre categorías?
3. ¿En qué categorías la brecha entre precio original y precio con descuento es mayor, y esas categorías convierten esa oferta en más reviews?

## Datos

- **Fuente:** [Amazon Sales Dataset (Kaggle)](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset)
- **Tamaño:** 1,465 registros y 16 columnas
- **Privacidad:** las columnas `user_id`, `user_name` y el texto de reseñas no se usan en el análisis ni aparecen en el dashboard.

## Proceso

1. **Limpieza en SQL** (`sql/limpieza_transformacion.sql`): precios y porcentajes de texto a número, extracción de la categoría principal (texto antes del primer `|`), exclusión de 1 registro con rating inválido y normalización de `rating_count`. La tabla original se conserva intacta.
2. **Modelo en Power BI:** tabla única a nivel producto con medidas DAX (rating promedio, descuento promedio, brecha de precio y ratio descuento-rating, con mínimo de 30 productos por categoría).
3. **Dashboard:** tarjetas KPI, reviews por categoría, dispersión rating vs. descuento, tabla de detalle por `product_id` y productos con rating menor a 3.5.

## Hallazgos principales

- El descuento por sí solo no explica la satisfacción: la correlación descuento-rating a nivel producto es de apenas −0.155.
- **Computers & Accessories** es la categoría de menor eficiencia descuento-rating entre las de volumen representativo: 54.0% de descuento promedio y 50% de brecha de precio, sin superar a Electronics en reviews.
- **Electronics** logra el doble de reviews (15.8M vs. 7.7M) con una brecha menor (41%), por lo que se sugiere mantener su estrategia.
- **OfficeProducts** muestra el rating más alto (4.31) con solo 12.4% de descuento, pero con apenas 31 productos se toma como referencia y no como destino de recursos.

**Recomendación:** revisar de forma gradual el descuento en Computers & Accessories y monitorear rating y reviews antes de ampliar el ajuste.

## Limitaciones

- Distribución muy desigual de productos por categoría: varias tienen 1 o 2 productos y no sostienen conclusiones.
- El dataset no incluye fechas, ventas ni costos: el número de reviews es solo un indicador aproximado del interés del cliente y el margen se aproxima con la brecha de precio.

## Estructura del repositorio

```
├── data/          # enlace a la fuente o tabla limpia (sin datos personales)
├── sql/           # scripts de limpieza y transformación
├── dashboard/     # archivo .pbix y PDF del reporte
├── docs/          # documento completo del proyecto y capturas (docs/img)
└── README.md
```

## Cómo se realizar el proceso de reproducción

1. Descarga del dataset desde Kaggle e importación en SQLite con DBeaver.
2. Ejecución `sql/limpieza_transformacion.sql` y exportación de la tabla limpia a CSV.
3. Abrir `dashboard/Amazon Report.pbix` en Power BI Desktop y actualiza la fuente de datos con tu CSV.

## Autor

**Gustavo Vázquez Reyes** · [www.linkedin.com/in/gustavo-vázquez-reyes-725101129] (ENLACE)
