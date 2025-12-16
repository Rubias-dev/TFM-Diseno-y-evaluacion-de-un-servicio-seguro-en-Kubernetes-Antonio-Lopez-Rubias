**Arquitectura segura basada en Kubernetes para servicios web**

Este repositorio contiene el material desarrollado para el Trabajo Fin de Máster titulado:

“Diseño e implementación de una arquitectura segura basada en Kubernetes para servicios web”

El proyecto tiene como objetivo diseñar, desplegar y evaluar una arquitectura Kubernetes segura, aplicando buenas prácticas de segmentación, control de acceso, protección de credenciales y validación experimental de las medidas de seguridad implementadas.

**Descripción general**

La arquitectura propuesta despliega varios servicios web en un clúster Kubernetes, organizados mediante namespaces independientes y protegidos mediante controles de seguridad en distintas capas:

Segmentación lógica por namespaces

Control de acceso basado en RBAC

Aislamiento de red mediante NetworkPolicies

Protección de credenciales con Kubernetes Secrets

Cifrado de comunicaciones internas mediante service mesh (Linkerd)

Restricciones de recursos para mitigar riesgos de denegación de servicio

El entorno ha sido desplegado y validado en un clúster local basado en Minikube sobre WSL, aunque el diseño es extrapolable a otros entornos Kubernetes.

**Arquitectura del sistema**

La solución incluye los siguientes componentes principales:

WordPress: portal corporativo público

Aplicación PHP (CodeIgniter 4): aplicación privada para usuarios autenticados

MySQL: base de datos con esquemas lógicos independientes

phpMyAdmin: herramienta de administración restringida

Ingress Controller (NGINX): punto de entrada al clúster

Calico: políticas de red y aislamiento interno

Linkerd: cifrado mTLS y observabilidad del tráfico interno

Cada componente se despliega en su propio namespace, con flujos de comunicación explícitamente definidos.

**Seguridad**

El diseño sigue un enfoque de defensa en profundidad y security by design, alineado con:

OWASP Kubernetes Top 10

Recomendaciones CCN-CERT BP/27

Las medidas de seguridad han sido evaluadas mediante experimentos prácticos que validan, entre otros aspectos:

Prevención del movimiento lateral

Aplicación del principio de mínimo privilegio

Protección efectiva de secretos

Estabilidad del sistema bajo carga

**Despliegue del entorno**

Para reproducir el entorno es necesario disponer de:

Kubernetes funcional (por ejemplo, Minikube)

kubectl configurado

Ingress Controller compatible

Linkerd y Calico instalados

El despliegue se realiza aplicando los manifiestos en el siguiente orden:

kubectl apply -f kubernetes/namespaces/
kubectl apply -f kubernetes/roles/
kubectl apply -f kubernetes/politicasRed/
kubectl apply -f kubernetes/mysqlDeployment/
kubectl apply -f kubernetes/appDeployment/
kubectl apply -f kubernetes/wordpressDeployment/
kubectl apply -f kubernetes/phpmyadminDeployment/
kubectl apply -f kubernetes/ingress/


Tras el despliegue, se recomienda verificar el correcto funcionamiento de los servicios y aplicar las comprobaciones descritas en la memoria del proyecto.

**Validación y experimentos**

El proyecto incluye una fase de evaluación en la que se realizan distintos experimentos orientados a validar las medidas de seguridad implementadas, como:

Intentos de movimiento lateral desde pods no autorizados

Pruebas de permisos RBAC

Verificación de acceso a secretos

Pruebas de carga para evaluar la resiliencia del sistema

Los detalles completos de estos experimentos se encuentran documentados en la memoria del TFM.

**Licencia**

Este proyecto se distribuye con fines académicos y educativos.
El uso del código queda sujeto a las licencias de las herramientas y tecnologías utilizadas.

**Autor**

Antonio López Rubias
Trabajo Fin de Máster – Ciberseguridad
