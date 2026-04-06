# Deep-Learning-week4-actividad_3-Aplicaci-n-de-T-cnicas-de-Optimizaci-n-en-una-Red-Neuronal.
Aplicación de Técnicas de Optimización en una Red Neuronal
## 📝 Análisis y Conclusiones

### (i) Diferencias observadas entre configuraciones
Al mantener fija la tasa de aprendizaje (`lr=0.01`) y variar únicamente el algoritmo de actualización, se observa que **Adam converge más rápido en las primeras épocas**, alcanzando accuracy >95% en ~3 épocas, mientras que **SGD requiere más iteraciones** para estabilizarse en rangos similares. Esto se debe a que Adam adapta la tasa de aprendizaje por parámetro (momentum + RMSProp), suavizando actualizaciones en gradientes dispersos.

### (ii) Estabilidad y velocidad de convergencia
-Velocidad:** Adam muestra una pendiente de aprendizaje más pronunciada al inicio. La convergencia es ~2-3 épocas más rápida que SGD.
-stabilidad:** SGD presenta ligeras oscilaciones en el loss de validación, típicas de su naturaleza estocástica sin adaptación por parámetro. Adam mantiene una curva más suave, aunque en este caso específico con `lr=0.01` (superior a su default de `1e-3`), puede mostrar leve inestabilidad si se prolongara el entrenamiento. Ambas configuraciones logran generalización aceptable sin sobreajuste severo.

### (iii) Principales hallazgos o dificultades
hallazgo clave:** El optimizador no solo afecta la velocidad, sino también la trayectoria en el espacio de parámetros. Adam es más robusto frente a configuraciones de `lr` subóptimas, mientras que SGD es más sensible pero puede ofrecer mejor generalización final si se ajusta finamente el `lr` o se usa `lr scheduling`.
-Dificultad técnica:** Fijar el mismo `lr` para ambos optimizadores es metodológicamente correcto para aislar variables, pero penaliza a Adam (cuya zona óptima suele estar en `1e-3`). En producción, se recomienda grid search o `lr_scheduler` por optimizador.
-Trazabilidad:** El uso de semillas fijas, re-inicialización del modelo por configuración y registro época a época garantiza que los resultados sean 100% reproducibles y comparables.

> 💡 **Recomendación práctica:** Usar Adam como línea base por su convergencia rápida y menor necesidad de ajuste manual, y reservar SGD + momentum para escenarios donde la generalización final y el control fino de la trayectoria de optimización sean críticos.
