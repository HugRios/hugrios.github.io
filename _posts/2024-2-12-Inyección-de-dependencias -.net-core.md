## Inyección de dependencias ##
### .Net Core ###

Principios: 
+ Se realiza una única contrucción del objeto
+ El objeto se llama cuando se requiera pero el objeto ya esta contruido
+ Los controladores que utilizan el objeto no se preocupan por los cambios realizados en el objeto

Esto soporta el principio inyección de dependencias.

### Tipos de inyección de dependencias ###
Transient (tránsito): distinta en cada solicitud (siempre va a ser diferente).
Scoped : el mismo objeto por cada solicitud a nivel request (mismo valor para una solicitud, diferente para solicitudes distintas)
Singleton: el mismo para todas las solicitudes (siempre el mismo valor)

![Ejemplo](./images/inyeccion.png "Ejemplo valores")

fuente: <https://www.youtube.com/watch?v=srPGwwMwAoA>
