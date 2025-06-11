---
layout: post
title: "Estructuras de datos"
---

## Tablas Hash ##
¿Que resuelven las tablas hash?

**Busquedas rápidas:** Encontrar un dato usando una clave sin tener que recorrer toda una lista o base de datos.
**Inserción rápida:** Agregar datos sin mucho costo de tiempo.
**Eliminación rápida:** Quitar datos rápidamente sin recorrer toda la estructura.
**Asociar pares clave-valor:** Guardar datos relacionados, por ejemplo, nombre → teléfono.

Y saber esto acercar de las tablas esta bien, pero ¿Que problemas en la vida real puedo resolver usando *tablas hash*?

- Buscar datos por identificador único (login de apps)
- Contar ocurrencia de palabras en un texto
- Implementar bases de datos en memoria o caches para accesos rápido
- detectar duplicados en una lista
- Mapear configuraciones o parámetros para acceso rápido.

**¿Y en la vida real?** 
Una agenda telefonica sencilla, un sistema de login... E iremos descubriendo más.

**Pero... ¿y cómo funcionan?**

Para el ejemplo de la agenda telefónica:

se usa un par key-value, como en la imagen se necesita una función hash que convierta el valor en un índice y así asignarlo dentro de un bucket (o posición dentro del array).
 
Ejemplo con un array tamaño 10:
 para el VALOR "Lisa" con NÚMERO 521-8976

 Función Hash
    5+2+1+8+9+7+6 = 38
    38 % 10;    
    resultado = 8

El Número de lisa estará guardado en el bucket (posición) 8 del array.



![Ejemplo](/images/Estructuras/hash.png "Ejemplo valores")

Bueno ¿y en el código?

veamos...

**Ejemplo c#**

```c# 

class HashTable{
    
    private const int Size = 10 // bucket tamaño fijo en 10
    private LinkedList<KeyValue>[] buckets; //lista 

    public HashTable(){
        buckets = new LinkedList<KayValue>[Size];
        for(int i = 0; i< Size: i++){
            buckets[i] = new LinkedList<KeyValue>();
        }
    }
}

´´´