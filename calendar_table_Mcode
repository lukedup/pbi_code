let
    #"Fecha inicio" = DateTime.Date(#date(2022, 6, 1)),
    #"Fecha final" = Date.From(DateTime.LocalNow()),
    Duración = Duration.Days((#"Fecha final"- #"Fecha inicio")) + 1,
    #"Lista días" = List.Dates(#"Fecha inicio", Duración, #duration(1,0,0,0)),
    #"Convertida en tabla" = Table.FromList(#"Lista días", Splitter.SplitByNothing(), null, null, ExtraValues.Error),
    #"Columnas con nombre cambiado" = Table.RenameColumns(#"Convertida en tabla",{{"Column1", "Fecha"}}),
    #"Tipo cambiado" = Table.TransformColumnTypes(#"Columnas con nombre cambiado",{{"Fecha", type date}}),
    #"Año insertado" = Table.AddColumn(#"Tipo cambiado", "Año", each Date.Year([Fecha]), Int64.Type),
    #"Mes insertado" = Table.AddColumn(#"Año insertado", "NMes", each Date.Month([Fecha]), Int64.Type),
    #"Nombre del mes insertado" = Table.AddColumn(#"Mes insertado", "Mes Largo", each Date.MonthName([Fecha]), type text),
    #"Primeros caracteres insertados" = Table.AddColumn(#"Nombre del mes insertado", "Mes Corto", each Text.Start([Mes Largo], 3), type text),
    #"Trimestre insertado" = Table.AddColumn(#"Primeros caracteres insertados", "NTrimestre", each Date.QuarterOfYear([Fecha]), Int64.Type),
    #"Día insertado" = Table.AddColumn(#"Trimestre insertado", "NDia", each Date.Day([Fecha]), Int64.Type),
    #"Nombre del día insertado" = Table.AddColumn(#"Día insertado", "Dia Largo", each Date.DayOfWeekName([Fecha]), type text),
    #"Poner En Mayúsculas Cada Palabra" = Table.TransformColumns(#"Nombre del día insertado",{{"Dia Largo", Text.Proper, type text}}),
    #"Primeros caracteres insertados1" = Table.AddColumn(#"Poner En Mayúsculas Cada Palabra", "Dia Corto", each Text.Start([Dia Largo], 3), type text),
    #"Semana del año insertada" = Table.AddColumn(#"Primeros caracteres insertados1", "NSemana", each Date.WeekOfYear([Fecha]), Int64.Type),
    #"Día de la semana insertado" = Table.AddColumn(#"Semana del año insertada", "NDia de la semana", each Date.DayOfWeek([Fecha]), Int64.Type)
in
    #"Día de la semana insertado"
