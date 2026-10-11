# ptia-fitqual-ai

Proyecto de la materia PTIA (Principios y Tecnologías de IA), semestre 2026-2, Escuela Colombiana de Ingeniería Julio Garavito.

FitQual AI es un modelo de visión por computadora que reconoce un alimento en una foto (clasificación de 101 clases de Food-101). La estimación de calorías y macronutrientes con una tabla nutricional por porción estándar hace parte del diseño del proyecto, pero no está implementada en este hito.

## Resultados (conjunto de prueba de Food-101)

| Métrica | Valor |
|---|---|
| Top-1 | 69,7 % |
| Top-5 | 90,7 % |

MobileNetV3 con la base congelada, 5 épocas. Son resultados preliminares.

## Estructura del notebook

El notebook `notebooks/fitqual_entrenamiento.ipynb` se organiza en seis bloques.

### 1. Diseño del problema y del modelo
- Clasificación de 101 clases (Food-101).
- Entrada: imagen RGB de 224x224. Salida: clase del alimento.
- Capa de salida densa con softmax, pérdida Sparse Categorical Crossentropy, optimizador AdamW y métricas Top-1 y Top-5.

### 2. Datos
- Carga de Food-101 con TensorFlow Datasets.
- División en entrenamiento, validación (10 % del train) y prueba (partición oficial).
- Análisis exploratorio: imágenes por clase, ejemplos y efecto del data augmentation.

### 3. Modelo
- MobileNetV3 (Keras Applications) preentrenado en ImageNet, con las capas congeladas.
- Capa final reemplazada por una capa densa de 101 salidas.

### 4. Entrenamiento y evaluación
- Prueba rápida con un subconjunto y luego entrenamiento completo con `model.fit`.
- Curvas de loss y accuracy (entrenamiento y validación).
- Top-1 y Top-5 sobre el conjunto de prueba.
- Análisis de errores: pares de clases más confundidas, matriz de confusión de esas clases y ejemplos de aciertos y errores con su confianza.
- Guardado de los pesos del modelo.

### 5. Inferencia
- Función que recibe una foto y devuelve las 3 clases más probables con su confianza.

### 6. Conclusiones
- Resultados, limitaciones y trabajo futuro.

## Cómo ejecutarlo
1. Abrir el notebook en Google Colab y activar la GPU (Entorno de ejecución → Cambiar tipo de entorno → T4 GPU).
2. Ejecutar todas las celdas. Se pide acceso a Google Drive, donde se guardan los pesos y el historial de entrenamiento.
3. La descarga de Food-101 pesa unos 5 GB y el entrenamiento completo tarda cerca de 50 minutos.
4. Las dependencias están en `requirements.txt`.

Los pesos entrenados (`fitqual.weights.h5`) no están en el repositorio: [enlace a Drive].

## Limitaciones
- Una clase por foto: con varios alimentos, el modelo propone uno solo.
- No puede responder "no lo conozco": siempre asigna una de las 101 clases.
- Food-101 tiene sobre todo platos occidentales y casi no incluye comida colombiana.
- Las métricas se midieron sobre Food-101, no sobre fotos de usuarios reales.

## Herramientas
- Python, TensorFlow/Keras y Google Colab (GPU T4).

## Fuentes
- Food-101: Bossard, Guillaumin y Van Gool (2014).
- MobileNetV3: Howard et al. (2019).
- Uso de IA: se usó Claude (Anthropic) como asistente de programación y redacción.


## Autoría
- Daniel Felipe Sua: 
- Juan David Munar
