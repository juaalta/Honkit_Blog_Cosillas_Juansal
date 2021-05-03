# Lectura de ficheros INI sin secciones con Inno Setup desde código (continuación)

Este post es una continuación del anterior y voy a añadir un nuevo método, el cual se encarga de comprobar si una etiqueta existe en el fichero.

``` delphi
function ExisteEtiqueta (Etiqueta: String): Boolean;
var
    I:        LongInt;
    L:        LongInt;
    S:        String;
begin
    S := Etiqueta + '=';
    L := Length (S);
    For I := 0 to GetArrayLength (ConfigValues) - 1 do
    begin
        if (copy (ConfigValues [I], 1, L) = S) then
        begin
            Result := TRUE;
            Exit;
        end;
    end;
    Result := FALSE;
end;
```
