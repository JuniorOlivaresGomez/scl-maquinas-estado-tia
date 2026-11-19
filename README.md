# scl-maquinas-estado-tia

Repositorio paso a paso para la programación de una máquina que realiza mangas en la industria metalúrgica.

## Hardware y Software
* **PLC:** Siemens S7-1200 (CPU 1215C)
* **IDE:** TIA Portal V19
* **Simulación:** S7-PLCSIM

## Temario y Módulos

| Módulo | Tema | Lo que programas tú |
| :---: | :--- | :--- |
| **M00** | Entorno: proyecto con tu 1215C, PLCSIM, repositorio | Repositorio en GitHub |
| **M01** | SCL básico: ciclo de scan, tipos, conversiones, FC | `FC_EscalarAnalogica` |
| **M02** | Timers y flancos (y la trampa del timer dentro de un `IF`) | `FB_Antirrebote`, `FB_Intermitente` |
| **M03** | Datos: UDT y DB en lugar de marcas `%M` | `UDT_CilindroIO`, `DB_Planta` |
| **M04** | Capa de I/O + simulador de planta | `FC_Read_IO`, `FC_Write_IO`, `FB_SimCilindro` |
| **M05** | FB de actuador: modos, interlocks, watchdog | `FB_Cilindro` |
| **M06** | Máquina de estados (lecciones 1 y 2) | `FB_Secuencia` |
| **M07** | Gestor de modos (FSM jerárquica) | `FB_GestorModos` |
| **M08** | Analógica: modelo de horno, on/off, `PID_Compact` | `FB_SimHorno`, `FB_ControlHisteresis` |
| **M09** | Diagnóstico: historial con tu FIFO, "esperando..." | `FB_HistorialFSM` |
| **M10** | HMI + `DB_SCADA` + V-Box | `FC_SCADA` + pantallas |
| **M11** | Integrador: máquina de mangas | Proyecto completo |
| **M12** | Seguridad funcional y normas | Evaluación de riesgos + arquitectura |