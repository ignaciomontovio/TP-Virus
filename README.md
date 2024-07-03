# TP-

## Pendientes:

-  Ver si podemos balancer la variable target, (todas las metricas nos dab bajas para el caso de positivos)

- Tratar las variables faltantes solo estamos haciendo:
    
        ("LVLImputer", ColImputer(imputer=SimpleImputer(strategy='mean'), columns=["LVL"])),
        ("EdadImputer", ColImputer(imputer=SimpleImputer(strategy='mean'), columns=["Edad"])),
        ("LaboralDummies", ColDummy(columns=["Laboral"])),
        ("GeneroDummies", ColDummy(columns=["Genero"], delete='Genero_Desconocido')),
        ("BLD03Scaler", ColScaler(scaler=MinMaxScaler(), columns=["BLD03"])),
        ("BLD02Scaler", ColScaler(scaler=MinMaxScaler(), columns=["BLD02"])),
        ("BLD01Scaler", ColScaler(scaler=MinMaxScaler(), columns=["BLD01"])),
        ("LVLScaler", ColScaler(scaler=MinMaxScaler(), columns=["LVL"]))


- Probar otros scalers, strategias etc...
- Ver validacion Cruzada
- Ver sesgo de seleccion y fuga de datos

- en la parte de tratamiento de variables no estamos haciendo nada relevante, hace falta ese scaler a todo el dataset? o podemos tener los scalers del pipeline y ya?

- escala casi siempre todas las variables creo deberiamos hacerlo

- en varios colab elige que variables utilizar y cuales no (en base a la correlacion?) ver si eso mejora las metricas

- Describir bien los pasos a realizar para produccion en el MD del notebook