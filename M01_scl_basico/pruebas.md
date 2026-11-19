# Pruebas - FC_EscalarAnalogica v0.1

Entorno: TIA Portal V19, S7-PLCSIM, CPU 1215C DC/DC/DC
Tolerancia en qValor: ±0.01

| # | Proposito | iRaw | iLimInf | iLimSup | Esperado qValor | Esperado qFueraRango | Obtenido qValor | Obtenido qFueraRango | OK |
|---|---|---|---|---|---|---|---|---|---|
| 1 | Inicio de rango | 0 | 0.0 | 300.0 | 0.0 | FALSE | 0.0 | FALSE | OK |
| 2 | Mitad de rango | 13824 | 0.0 | 300.0 | 150.0 | FALSE | 150.0 | FALSE | OK |
| 3 | Fin de rango | 27648 | 0.0 | 300.0 | 300.0 | FALSE | 300.0 | FALSE | OK |
| 4 | Rebase | 30000 | 0.0 | 300.0 | 300.0 | TRUE | 300.0 | TRUE | OK |
| 5 | Rango con negativo | 13824 | -50.0 | 150.0 | 50.0 | FALSE | 50.0 | FALSE | OK |
| 6 | Rango invertido | 6912 | 100.0 | 0.0 | 75.0 | FALSE | 75.0 | FALSE | OK |
| 7 | Raw negativo | -100 | 0.0 | 300.0 | 0.0 | TRUE | 0.0 | TRUE | OK |
| 8 | Rebase + rango invertido | 30000 | 100.0 | 0.0 | 0.0 | TRUE | 0.0 | TRUE | OK |
| 9 | Frontera superior | 27649 | 0.0 | 300.0 | 300.0 | TRUE | 300.0 | TRUE | OK |