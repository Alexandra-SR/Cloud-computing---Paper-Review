# Cloud-computing Paper-Review

# Autoscaling Proactivo para Kubernetes

Con el rápido desarrollo de la tecnología en la última década, el cloud computing ha ganado popularidad. La principal característica del cloud computing es la elasticidad, que permite a los propietarios de aplicaciones gestionar cargas de trabajo impredecibles, aprovisionando o desaprovisionando recursos según la demanda para mejorar el rendimiento mientras se reducen costos.

El autoscaling es un proceso esencial en la gestión de recursos en entornos de cloud computing, y puede ser categorizado en dos tipos: reactivo y proactivo.

## Tipos de Autoscaling

### Autoscaling Reactivo
Los enfoques reactivos realizan acciones de escalado analizando el estado actual del sistema estableciendo reglas o umbrales predefinidos. Se basan en métricas a nivel de infraestructura, como la utilización de CPU y memoria. Sin embargo, elegir los valores correctos para los umbrales es difícil debido a la fluctuación continua de la carga de trabajo.

### Autoscaling Proactivo
Los enfoques proactivos analizan datos históricos, predicen el futuro y toman decisiones de escalado. En este contexto, se propone un marco de autoscaling proactivo para Kubernetes.

## Diseño del Sistema

El diseño del sistema se basa en el bucle monitor-analizar-planear-ejecutar (MAPE) y consta de los siguientes componentes:

- **Load Balancer**: Actúa como una puerta de enlace que distribuye las peticiones entrantes a los nodos Kubernetes.
- **Recolector de Métricas de Aplicación**: Monitorea el equilibrio de carga y recopila métricas de aplicación.
- **Servidor de Monitoreo**: Recibe y almacena información del recolector en una base de datos de series temporales.
- **K8S Master**: Controla el clúster Kubernetes con componentes como etcd, kube-scheduler, kube-control-manager y kube-apiserver.
- **K8S Minion**: Aloja y ejecuta los pods siguiendo las instrucciones del maestro.

## Autoscaler Personalizado Proactivo

El autoscaler personalizado proactivo es el núcleo del sistema y consta de las siguientes fases:

### Fase de Monitoreo
El servidor de monitoreo recopila datos de red y de los pods en ejecución para su análisis y planificación.

### Fase de Análisis (Servicio de Pronóstico Bi-LSTM)
En esta fase, se utiliza un modelo de predicción Bi-LSTM para predecir la carga de trabajo futura en función de los datos históricos. Los Bi-LSTM son redes neuronales que se utilizan para mejorar la precisión de las predicciones.

### Fase de Planificación (Servicio de Gestión de Adaptación)
En esta fase, se calcula el número de pods necesarios para satisfacer la carga de trabajo futura. Se utiliza un algoritmo que decide si escalar hacia arriba o hacia abajo, considerando un valor mínimo de pods y una estrategia de eliminación de recursos (RRS).

### Fase de Ejecución
El motor Kubernetes recibe el comando de escalado de la fase de planificación y ajusta el número de réplicas de pod.

## Modelo de Predicción Bi-LSTM

El modelo de predicción Bi-LSTM consta de dos capas que procesan datos históricos y se utiliza para predecir la carga de trabajo futura. Se ha demostrado que este modelo supera a los modelos LSTM y ARIMA tanto en precisión como en velocidad de predicción.

## Experimentación y Evaluación

El sistema se ha evaluado utilizando conjuntos de datos reales y se ha comparado con modelos LSTM y ARIMA. Se han utilizado métricas como el error cuadrático medio (MSE), el error cuadrático medio raíz (RMSE) y el error absoluto medio (MAE) para evaluar la precisión de las predicciones.

## Resultados y Conclusiones

Los resultados de los experimentos muestran que el modelo de predicción Bi-LSTM logra una mayor precisión y velocidad de predicción que los modelos LSTM y ARIMA. Además, el autoscaler personalizado proactivo propuesto supera al autoscaler horizontal de pods predeterminado de Kubernetes en términos de aprovisionamiento y desaprovisionamiento de recursos.

En resumen, este sistema de autoscaling proactivo basado en Kubernetes ofrece una solución eficaz para gestionar cargas de trabajo impredecibles en entornos de cloud computing, mejorando el rendimiento y reduciendo costos de manera significativa.
