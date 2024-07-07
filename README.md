# PIPELINE que use
    ("DropColumns", ColumnDrop(["Genero", "hijos", "Laboral", "REC1", "REC2"])),
    ("BLD03Scaler", ColScaler(scaler=MinMaxScaler(), columns=["BLD03"])),
    ("BLD02Scaler", ColScaler(scaler=MinMaxScaler(), columns=["BLD02"])),
    ("BLD01Scaler", ColScaler(scaler=MinMaxScaler(), columns=["BLD01"])),
    #("REC3Scaler", ColScaler(scaler=MinMaxScaler(), columns=["REC3"])),
    ("LVLReplace", ReplaceValue("LVL",1000000, np.nan)), # Reemplazar los 1000000 por nan
    ("LVLImputer", ColImputer(imputer=SimpleImputer(strategy='mean'), columns=["LVL"])),
    ("LVLScaler", ColScaler(scaler=MinMaxScaler(), columns=["LVL"])),
    ("EdadImputer", ColImputer(imputer=SimpleImputer(strategy='median'), columns=["Edad"])),
    ("EdadTypeReplace",ColumnTypeModifier("Edad",int))

# Clases nuevas para el PIPELINE
    class ReplaceValue(BaseEstimator, TransformerMixin):
        def __init__(self, column, old_value, new_value):
            self.column = column
            self.old_value = old_value
            self.new_value = new_value
    
        def fit(self, X, y=None):
            return self
    
        def transform(self, X):
            Xc = X.copy()
            Xc.loc[:, self.column] = Xc[self.column].replace(self.old_value, self.new_value)
            return Xc
        
    class ColumnTypeModifier:
        def __init__(self, column_name, new_dtype):
            self.column_name = column_name
            self.new_dtype = new_dtype
        def fit(self, X, y=None):
            return self
        def transform(self, X):
            Xc = X.copy()
            Xc[self.column_name] = Xc[self.column_name].astype(self.new_dtype)
            return Xc
    class ColumnDrop:
        def __init__(self, columns_to_drop=[]):
            super().__init__()
            self.columns_to_drop=columns_to_drop
    
        def fit(self, X, y=None):
            return self
        
        def transform(self, X):
            Xc = X.copy()
            Xc = Xc.drop(self.columns_to_drop, axis=1)
            return Xc
