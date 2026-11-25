# Pruebas - M03

Entorno: TIA Portal V19, S7-PLCSIM, CPU 1215C DC/DC/DC

## UDT_CilindroIO - propagacion de cambios

| # | Accion | Esperado | OK |
|---|---|---|---|
| 1 | Agregar campo `Habilitado : Bool` en UDT_CilindroIO y compilar | Cil1 y Cil2 de DB_Planta muestran `Habilitado` sin editar el DB | OK |
| 2 | Borrar `Habilitado` del UDT y compilar | Desaparece de Cil1 y Cil2 | OK |

Conclusion: un cambio en la definicion del UDT se aplica a todas las
variables de ese tipo. Con Struct declaradas a mano habria que editar
cada una.

## FC_BloqueoIncoherencia v0.1

Banco: llamada en OB1 para "DB_Planta".Cil1 y "DB_Planta".Cil2.
Valores escritos con Modify now en la tabla Prueba_M03.

| # | Escenario | SensAtras | SensAdelante | BobinaAvance (antes) | Esperado | OK |
|---|---|---|---|---|---|---|
| 1 | Cil1 iniciando un avance (normal) | 1 | 0 | 1 | Bobina sigue TRUE; IncoherenteCil1 = FALSE | OK |
| 2 | Cil1 con sensor danado (ambos activos) | 1 | 1 | 1 | Bobina pasa a FALSE; IncoherenteCil1 = TRUE | OK |
| 3 | Cil2 normal mientras Cil1 incoherente | 1 | 0 | 1 | Bobina de Cil2 sigue TRUE; IncoherenteCil2 = FALSE | OK |

## Experimento: parametro Input vs InOut

| Seccion de ioCil | Resultado |
|---|---|
| InOut | Compila; la FC escribe las bobinas del cilindro original |
| Input | No compila: el bloque intenta escribir en un parametro de solo lectura |

Conclusion: la seccion del parametro se elige segun lo que el bloque
necesita hacer. Input (solo lectura) deja que el compilador impida
modificaciones accidentales; InOut solo cuando el bloque debe escribir.