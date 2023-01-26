---
layout: post
title: "Configuración Oracle-Entity Framework"
---


# Configurar conexión dinamica (para más de un esquema) Entity framework para oracle .net

La carpeta DbOracleContext contiene 2 archivos para este propósito:

![hello](/images/OracleEntity/estructuraModel.PNG)


1. DBConnectionType: lista de conexiones que pueden ser usadas en el DB context

```c#
namespace WMServices.Models.DbOracleContext
{
    public enum DBConnectionType
    {
        ClvConnection = 004,
        SanConnection = 065
    }
}
```

Para el ejemplo se requieren dos tipos de conexiones.


2. DBOracleContext: Archivo de configuración del DB context. 

```c#
  public class DbOracleContext : DbContext
    {
        public string _schema = "";
        public  DbOracleContext(DBConnectionType connectionType)
        : base(new OracleConnection(setConnection(connectionType)), true)
        {
            _schema = setSchema(connectionType);
        }
    }
```
si no se requiere exponer el valor de _schema puede declararse con el modificador de acceso private.

Se declara el constructor de la clase con un parametro tipo DBConnectionType.

El fragmento :base inicia un objeto de la clase OracleConnection al que se le inyecta un método de la clase setConnection que recibe el parámetro connectionType y regresa la cadena de conexión correspondiente al valor requerido.

```c#
   private static string setConnection(DBConnectionType connectionType)
        {
            string connString = "";
            if (connectionType == DBConnectionType.ClvConnection)
            {
                connString = ConfigurationManager.ConnectionStrings["WMSCLV"].ConnectionString;
            }
            else if (connectionType == DBConnectionType.SanConnection)
            {
                connString = ConfigurationManager.ConnectionStrings["WMSSAN"].ConnectionString;
            }

            return connString;
        }
```

El método setConnection realiza una comparación entre el parámetro connectionType y los tipos de coneexiones contenidas en la clase DBConnectionType para devolver la cadena de conexión correspondiente.

