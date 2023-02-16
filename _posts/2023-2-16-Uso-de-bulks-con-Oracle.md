---
layout: post
title: "Uso de bulks para Oracle con c# y .net"
---

## Insertando +100000 registros con OracleBulkCopy

En la última entrada mostré como formar una cadena sql para insertar cantidades grandes de registros, sin embargo, esto carece de total seguridad ya que podría permitir inyección SQL además de problemas de performance, asi que tuve que encontrar una mejor forma de resolver el problema y ahí me encontré con la magía de los bulks para Oracle (los cuales pueden ser usados para SQL Server también).

Explicaré el uso con un poco de código:

```c#
private void InsertaRegistros(List<dynamic> list)
        {
            DbOracleContext context = new DbOracleContext();
            try
            {
                using (context.ConnectToDB(GetConnectionType(loc)))
                {
                    DataTable dataTable = new DataTable();

                    dataTable.Columns.Add("FIELD1", typeof(string));
                    dataTable.Columns.Add("FIELD2", typeof(string));
                    dataTable.Columns.Add("FIELD3", typeof(string));

                    for (int i = 0; i < list.Count; i++)
                    {
                        dataTable.Rows.Add(list[i].field,
                                            list[i].field2,
                                            list[i].field3);
                    }

                    using (OracleBulkCopy bulkCopy = new OracleBulkCopy(context.ConnectToDB(GetConnectionType(loc)), OracleBulkCopyOptions.UseInternalTransaction))
                    {
                        bulkCopy.BatchSize = 10000;
                        bulkCopy.BulkCopyTimeout = 0;
                        bulkCopy.DestinationTableName = "mfpegs";
                        bulkCopy.WriteToServer(dataTable);
                    }
                }
            }
            catch (Exception e)
            {

                throw;
            }
        }

´´´