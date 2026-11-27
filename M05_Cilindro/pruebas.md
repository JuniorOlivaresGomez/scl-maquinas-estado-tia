# M05 - FB_Cilindro: pruebas

Banco: DB_Test_M05, OB1 (iDB_Cil1 con banco completo, iDB_Cil2 con iAuto = FALSE),
simulador FB_SimCilindro en OB30 (Cil1 biestable, Cil2 monoestable).
Tabla de observacion: Prueba_M05. Tabla SIM: I_Reset, I_Cil1_Adelante, I_Cil1_Atras.

| # | Prueba | Esperado | Resultado |
|---|---|---|---|
| 1 | Manual sostenido | Avanza con ManAv; al soltar, bobina off y queda en 100 | OK |
| 2 | Automatico | Sigue CmdRe / CmdAv | OK |
| 3 | Ordenes contradictorias | Ninguna bobina | OK |
| 4 | Interlock en reposo | No se mueve, qEsperandoPermiso = TRUE, sin falla > 3 s | OK |
| 5 | Interlock a mitad de carrera | Bobina off, pero el biestable llega a 100; sin falla | OK |
| 6 | Watchdog de avance | iFallaAtascado -> codigo 1 a los 3 s, bobina off | OK |
| 7 | Rearme | Flanco de I_Reset -> codigo 0 | OK |
| 8 | Primera falla | Con codigo 1, ambos sensores activos -> sigue en 1 | OK |
| 9 | Rearme con causa presente | Reset con ambos sensores -> 3; sin adelante y reset -> 0 | OK |
| 10 | Independencia de Cil2 | Cil2 opera y sin falla mientras Cil1 esta en falla | OK |

## Llamadas en OB1 (Network 1, SCL)
OB1 esta en LAD con una red SCL, por eso no se exporta como fuente.

    "FC_Read_IO"();

    "iDB_Cil1"(iAuto := "DB_Test_M05".Auto,
               iCmdAutoAvanzar := "DB_Test_M05".CmdAv,
               iCmdAutoRetroceder := "DB_Test_M05".CmdRe,
               iManAvanzar := "DB_Test_M05".ManAv,
               iManRetroceder := "DB_Test_M05".ManRe,
               iPermisoAvanzar := "DB_Test_M05".PermisoAv,
               iPermisoRetroceder := "DB_Test_M05".PermisoRe,
               iTiempoMax := T#3S,
               iReset := "DB_Planta".Panel.Reset,
               ioCil := "DB_Planta".Cil1);

    "iDB_Cil2"(iAuto := FALSE,
               iTiempoMax := T#3S,
               iReset := "DB_Planta".Panel.Reset,
               ioCil := "DB_Planta".Cil2);

    "FC_BloqueoIncoherencia"(ioCil := "DB_Planta".Cil1,
                             qIncoherente => "DB_Test_M02".IncoherenciaCil1);
    "FC_BloqueoIncoherencia"(ioCil := "DB_Planta".Cil2,
                             qIncoherente => "DB_Test_M02".IncoherenciaCil2);

    "FC_Write_IO"();

## Observaciones
- La primera version fallo la prueba 9: SensIncoherentes (Temp) se leia sin
  haberse escrito nunca, asi que el codigo 3 no podia aparecer. La bobina solo
  se apagaba gracias a FC_BloqueoIncoherencia.
- Los valores por defecto corregidos (permisos TRUE, iTiempoMax T#3S) no llegaron
  al PLC hasta hacer STOP -> RUN: el valor de arranque no sobrescribe el valor
  actual en una carga en caliente.
- Al liberar el atasco con la falla activa, el cilindro biestable completo la
  carrera con la bobina apagada: una falla no detiene un biestable.