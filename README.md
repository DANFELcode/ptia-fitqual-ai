# ptia-fitqual-ai
Proyecto correspondiente a la materia PTIA(principios y tecnologias de ia) para el semestre 2026-2, modelo de visión por computadora  que reconoce un alimento en una foto y estima sus calorías y macronutrientes. 

## Estructura del notebook

El notebook `notebooks/entrenamiento.ipynb` se organiza en cinco bloques.

### 1. Diseño del problema y del modelo
- Clasificación de 101 clases (Food-101).
- Entrada: imagen RGB de 224x224. Salida: clase del alimento.
- Capa de salida con softmax, pérdida Cross-Entropy, optimizador AdamW y métricas Top-1 y Top-5.

### 2. Datos
- Carga de Food-101 con torchvision.
- División en entrenamiento, validación (10 % del train) y prueba (partición oficial).
- Análisis exploratorio: imágenes por clase, ejemplos y efecto del data augmentation.

### 3. Modelo
- MobileNetV3 preentrenado en ImageNet, con las capas congeladas.
- Capa final reemplazada por una de 101 salidas.

### 4. Entrenamiento y evaluación
- Prueba rápida con un subconjunto y luego entrenamiento completo.
- Curvas de loss y accuracy (entrenamiento y validación).
- Top-1 y Top-5 sobre el conjunto de prueba, con ejemplos de aciertos y errores.
- Guardado de los pesos del modelo.

### 5. Inferencia
- Función que recibe una foto y devuelve las 3 clases más probables con su confianza.

## Fuentes
- Food-101: Bossard, Guillaumin y Van Gool (2014).
- MobileNetV3: Howard et al. (2019).
- [Tutorial de transfer learning de PyTorch, si lo usan]
- Uso de IA: se usó Claude (Anthropic) como apoyo para [planear la estructura del notebook y explicar conceptos]. [Ajustar a lo que realmente hicieron]

## Autoría
- Daniel Felipe Sua: [parte]
- Juan David Munar: [parte]
