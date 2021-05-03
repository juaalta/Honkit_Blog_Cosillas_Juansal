# Lectura de ficheros INI sin secciones con Inno Setup desde código

En este post voy a poner un código de ejemplo en el cual se parsea un fichero INI sin secciones (fichero INI estilo UNIX) desde el Inno Setup.
Para esto hay que crear el código en la sección [Code] de este programa.

``` delphi
[Code]
var
    ConfigValues:    TArrayOfString;

function LeeFicheroConfiguracion (FileName: String): Boolean;
begin
    Result := LoadStringsFromFile (FileName, ConfigValues);
end;

function ObtieneValorEtiqueta (Etiqueta: String; var Value: String): Boolean;
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
            Value := copy (ConfigValues [I], L + 1,
                Length (ConfigValues [I]) - L);
            Result := TRUE;
            Exit;
        end;
    end;
    Result := FALSE;
end;

function EscribeValorEtiqueta (Etiqueta: String; Value: String): Boolean;
var
    I:        LongInt;
    L:        LongInt;
    A:        LongInt;
    S:        String;
begin
    S := Etiqueta + '=';
    L := Length (S);
    A := GetArrayLength (ConfigValues);
    For I := 0 to A - 1 do
    begin
        if (copy (ConfigValues [I], 1, L) = S) then
        begin
            ConfigValues [I] := S + Value;
            Result := TRUE;
            Exit;
        end;
    end;
    SetArrayLength (ConfigValues, A + 1);
    ConfigValues [A] := S + Value;
    Result := FALSE;
end;

function EscribeFicheroConfig (FileName: String): Boolean;
var
    bRet:    Boolean;
begin
    // FileName -> Backup.
    bRet := FileCopy (FileName,
        ExpandConstant ('{tmp}\' + ExtractFileName (FileName)),
        FALSE);
    if (bRet) then
    begin
        bRet := SaveStringsToFile (FileName, ConfigValues, FALSE);
        if (bRet) then
        begin
            Result := TRUE;
            Exit;
        end else
        begin
            // Maybe the backup file should be copied back here?
        end;
    end;
    Result := FALSE;
end;
```

Espero que le sirva a la gente que haya tenido el mismo problema que yo.
