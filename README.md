# Arquitectura-Backend-readme-

<!-- Output copied to clipboard! -->

<!-- You have some errors, warnings, or alerts. If you are using reckless mode, turn it off to see inline alerts.
* ERRORs: 0
* WARNINGs: 0
* ALERTS: 4 -->


# Arquitectura Backend


### Documento de diseño

[https://github.com/jorgevgut/airquality-mx/wiki/High-level-System-Design](https://github.com/jorgevgut/airquality-mx/wiki/High-level-System-Design)


#### Plantilla

[https://github.com/jorgevgut/curso_backend_platzi/blob/main/design_doc_template.md](https://github.com/jorgevgut/curso_backend_platzi/blob/main/design_doc_template.md)


### Revisión de diseño


### 



### Elaboración Arquitetura



# Escalabilidad: Throttling y RetryPolicies



Para Throttling sería mejor retornar un código 429 que es Too Many Requests en lugar de un error de servidor.


## Referencia: **Backoff exponencial**

Visitar: [https://aws.amazon.com/blogs/architecture/exponential-backoff-and-jitter/](https://aws.amazon.com/blogs/architecture/exponential-backoff-and-jitter/)

El Backoff exponencial es una técnica que se utiliza como parte de una estrategia de reintentos en sistemas escalables. Este consiste en que si tenemos un Cliente que manda peticiones a un servicio hospedado en la nube, cuando se encuentra un codigo de error en la respuesta del servicio, este suma un "delay" antes de volver a intentar enviar dicha petición.

Algunos ejemplos en los que se puede hacer uso de esta técnica son:



* Se tiene un servicio que procesa cientos de compras en linea por segundo, eventualmente un error de red ocasiona errores 500 de servidor, dada la perdida de conexión con la base de datos. Al recibir el cliente un error 500 por medio del protocolo HTTP, reintentar la petición con backoff exponencial y la petición tiene exito. En horas pico, puede llegar a intentar hasta 2 o 3 veces hasta que logra con exito procesar el requisito.

(x1)

Vale, en este reto no sé exactamente qué tengo que hacer xD, no tengo un servicio Cloud ahora mismo(?, pero resumiendo conceptos:

.

**Throtling**: Es básicamente hacer que tu servidor devuelva un error intencionado, no es un error real, yo regresaría un error 503 (Service Unavailable Error)

.

**BackOff**: Por lo que entiendo, es el cómo manejamos los retry’s, es decir, en lugar de hacer el retry un segundo después, podemos posponerlo a que se reintente en X segundos, cuando es posible que el servidor tenga menos requests

(x2)

**Throttiling**: patrón arquitectónico permite controlar la cantidad de recursos que una aplicación puede utilizar antes de estrangular los procesos no esenciales a favor de mantener a flote el servicio, evitando una interrupción o caída de instancias o aplicaciones.

**Circuite Brake**r: evita que una aplicación intente de manera reiterada una operación que con probabilidad vaya a fallar, permitiendo que esta continúe con su ejecución sin malgastar recursos mientras el problema no se resuelva. puede detectar cuando se ha resuelto el problema permitiendo de esta manera volver a ejecutar la operación comprometida.

BackOff: lo veo más como el estado cuando los recursos ya fueron sobre pasados y el back no responde.
