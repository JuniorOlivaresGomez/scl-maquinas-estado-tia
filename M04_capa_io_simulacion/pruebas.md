# Pruebas - M04

Entorno: TIA Portal V19, S7-PLCSIM V19 (Tabla SIM), CPU 1215C DC/DC/DC + SM 1234
Simulador de cilindros en OB30 (100 ms): Cil1 biestable, Cil2 monoestable, carrera 1,5 s.

| # | Verificacion | Resultado observado | OK |
|---|---|---|---|
| 1 | Paro NC: I_Stop_NC FALSE / TRUE | Panel.Stop = TRUE / FALSE | OK |
| 2 | Posicion inicial | Cil1 y Cil2 en 0 %, SensAtras = TRUE | OK |
| 3 | Avance Cil1 (biestable) | 26,7 % a 0,6 s (ambos sensores FALSE); 100 % a 2,5 s, SensAdelante = TRUE; se detiene en 100 | OK |
| 4 | Memoria valvula biestable | Bobina en 0: permanece en 100 % | OK |
| 5 | Retroceso Cil1 | Vuelve a 0 %, SensAtras = TRUE; permanece al apagar la bobina | OK |
| 6 | Monoestable Cil2 | Avanza a 100 %; sin bobina vuelve solo a 0 % (resorte) | OK |
| 7 | Falla inyectada: atasco | Con iFallaAtascado = TRUE la posicion no cambia; al quitarla, se mueve | OK |
| 8 | Salidas bloqueadas en simulacion | BobinaAvance = TRUE y Q_Cil1_Avance = FALSE | OK |
| 9 | Modo real | Sensores desde %I; BobinaAvance = TRUE -> Q_Cil1_Avance = TRUE | OK |
| 10a | 4-20 mA, 12 mA (Raw 13824) | Valor = 150.0, Falla = FALSE | OK |
| 10b | 4-20 mA, 3 mA (Raw -1728) | Valor = 300.0 (valor seguro), Falla = TRUE, FallaBaja = TRUE | OK |
| 10c | 4-20 mA, 21,5 mA (Raw 30240) | Valor = 300.0, Falla = TRUE, FallaBaja = FALSE (falla alta) | OK |

Errores encontrados y corregidos durante las pruebas:
- FC_Read_IO: faltaba NOT en la lectura del paro NC (Panel.Stop quedaba TRUE).
- FB_SimCilindro: faltaba LIMIT de la posicion; la valvula monoestable llevo Pos a -2160 %.

Nota: la Tabla SIM de PLCSIM V19 solo acepta DEC sin signo o Hex para palabras.
Los valores negativos se escriben en complemento a dos (ej. -1728 = 16#F940).