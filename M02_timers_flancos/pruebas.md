# Pruebas - M02

Entorno: TIA Portal V19, S7-PLCSIM, CPU 1215C DC/DC/DC

## FB_Antirrebote v0.1

Banco: iTiempo = T#3S; flancos contados con contadores en DB_Test_M02.

| # | Accion | Esperado Salida | Esperado ContSubidas / ContBajadas | Obtenido | OK |
|---|---|---|---|---|---|
| 1 | Entrada a TRUE y mantener 5 s | TRUE ~3 s despues | 1 / 0 | TRUE, 1 / 0 | OK |
| 2 | Entrada a FALSE y mantener 5 s | FALSE ~3 s despues | 0 / 1 | FALSE, 0 / 1 | OK |
| 3 | Entrada TRUE 1 s y vuelve a FALSE | Sigue FALSE | 0 / 0 | FALSE, 0 / 0 | OK |
| 4 | Rebotes en menos de 3 s, dejar en TRUE | TRUE ~3 s despues del ultimo cambio | 1 / 0 | TRUE, 1 / 0 | OK |
| 5 | Con salida TRUE: entrada FALSE 1 s y vuelve a TRUE | Sigue TRUE | 0 / 0 | TRUE, 0 / 0 | OK |

Nota: el caso 5 detecto un error de la primera version (flancos calculados
sobre los timers en lugar de la salida filtrada).

## FB_Intermitente v0.1

Banco: TP de 60 s para habilitar; pulsos contados con flanco manual en OB1.

| # | Configuracion | Accion | Esperado | Obtenido | OK |
|---|---|---|---|---|---|
| 1 | On 1 s, Off 2 s | Habilitar 60 s | ~20 pulsos | 20 | OK |
| 2 | On 10 s, Off 2 s | Deshabilitar con baliza encendida | Apaga inmediato | Apaga inmediato | OK |
| 3 | On 1 s, Off 10 s | Deshabilitar en fase apagada y rehabilitar antes de 10 s | Empieza encendida | Empieza encendida | OK |
| 4 | On 100 ms, Off 100 ms | Habilitar 60 s | ~300 pulsos | 300 | OK |
| 5 | On 1 s, Off 10 s | Primera habilitacion tras arrancar la CPU | Empieza encendida | Empieza encendida | OK |

Nota: periodo real = Ton + Toff + 2*Tc (Tc = tiempo de ciclo de OB1).
En PLCSIM Tc es muy pequeno, por eso salio exacto; con Tc = 10 ms la
prueba 4 daria ~273 pulsos.

## Experimento: timer dentro de un CASE (FB_Trampa)

| Version | 1.a vez en estado 1 | 2.a vez en estado 1 |
|---|---|---|
| A: timer dentro del CASE | 5 s | No espera: vuelve al estado 2 de inmediato |
| B: timer fuera del CASE | 5 s | 5 s |

Causa: en la version A el timer no se llama en el estado 2 y queda con Q = TRUE;
al volver al estado 1 no ve flanco en IN y salta. En la version B se llama
siempre y se reinicia con IN = FALSE.

## FB_FiltroPT1 v0.1

Banco: llamado en OB30 (100 ms) con iTs = 0.1.

| # | Verificacion | Esperado | OK |
|---|---|---|---|
| 1 | Escalon X 0 -> 100 con Tf = 1.0 | Sube suave; > 99 a los 5 s | OK |
| 2 | Tf = 0 | Y = X inmediato, ErrorFiltro = FALSE | OK |
| 3 | Reset a mitad de la subida | Y salta a X | OK |
| 4 | Tf = -1 | ErrorFiltro = TRUE, Y = X | OK |
| 5 | STOP -> RUN con X = 50 | Y arranca en 50 | OK |