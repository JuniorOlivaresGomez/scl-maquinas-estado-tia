# Pruebas - M01

Entorno: TIA Portal V19, S7-PLCSIM, CPU 1215C DC/DC/DC

## FC_EscalarAnalogica v0.1

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

## FC_Escalar4a20 v0.1

Configuracion: iLimInf = 0.0, iLimSup = 300.0, iValorFalla = 999.0
(valor de prueba distinto de cualquier resultado del escalado, para verificar la sustitucion)
Tolerancia: qValor ±0.01

| # | Proposito | iRaw | Esp. qValor | Esp. qFueraRango | Esp. qFalla | Esp. Baja / Alta / DesbAlto / DesbBajo | Obt. qValor | Obt. qFueraRango | Obt. qFalla | Obt. Baja / Alta / DesbAlto / DesbBajo | OK |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Inicio (4 mA) | 0 | 0.0 | F | F | F / F / F / F | 0.0 | F | F | F / F / F / F | OK |
| 2 | Mitad (12 mA) | 13824 | 150.0 | F | F | F / F / F / F | 150.0 | F | F | F / F / F / F | OK |
| 3 | Fin (20 mA) | 27648 | 300.0 | F | F | F / F / F / F | 300.0 | F | F | F / F / F / F | OK |
| 4 | Bajo rango sin falla (3.8 mA) | -346 | 0.0 | T | F | F / F / F / F | 0.0 | T | F | F / F / F / F | OK |
| 5 | Falla baja (3.0 mA) | -1728 | 999.0 | F | T | T / F / F / F | 999.0 | F | T | T / F / F / F | OK |
| 6 | Sobre rango sin falla (20.5 mA) | 28512 | 300.0 | T | F | F / F / F / F | 300.0 | T | F | F / F / F / F | OK |
| 7 | Falla alta (21.5 mA) | 30240 | 999.0 | F | T | F / T / F / F | 999.0 | F | T | F / T / F / F | OK |
| 8 | Desborde alto | 32767 | 999.0 | F | T | F / F / T / F | 999.0 | F | T | F / F / T / F | OK |
| 9 | Desborde bajo | -32768 | 999.0 | F | T | F / F / F / T | 999.0 | F | T | F / F / F / T | OK |

Corriente verificada en prueba previa: 3.8 mA -> 3.799768 mA; desborde alto -> 22.96239 mA.