---
layout: post
title: "Crear un cadena sql con linq"
---

## Creando un INSERT query para grandes cantidades de registros

```C#
 private string CreateSql(List<PegsModel> list)
        {
            Console.WriteLine("escribiendo query...");
            string sql = "";
                sql =
                "begin " +
                string.Join("; ", list.Select(x => $"insert into " + "TABLE (field, " +
                    $" field1, field2, field3, field_date, field4," +
                    $" field5, field6, field7, field8, field_date) values ('{x.field}', '{x.field1}'," +
                    $" q'[{x.field2}]', {(x.field3.HasValue ? x.field3 : 0) }, TO_DATE('{x.field_date}', 'YYYY-MM-DD'), " +
                    $" '{x.field4}', '{x.field5}', '{x.field6}', {x.field7}, " +
                    $" '{x.field8}', TO_DATE('{x.field_date}', 'MM-DD-YYYY HH:MI:SS PM'))")) +
                    "; end;";
            return sql;
        }

```

La función comienza con el uso del método string.Join() el cual combina x cantidad de cadenas 
en una sola. El método recibe 2 argumentos: un separador, y un array o lista. 

Para extraer los elementos de la lista (valores agregados al query) se requiere usar el método lista.Select()
el método extrae los valores necesarios y los genera en una nueva lista.

```C#
 {(x.field3.HasValue ? x.field3 : 0) }
```

El fragmento anterior valida si el campo contiene algun valor, de ser así agrega el valor a la cadena, de lo contrario agrega un 0.