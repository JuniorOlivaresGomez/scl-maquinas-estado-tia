# scl-maquinas-estado-tia

Repositorio paso a paso para la programación de una máquina que fabrica mangas aislantes y exotérmicas para la industria de fundición, con SCL y máquinas de estado (IEC 61131-3).

## Hardware y Software
* **PLC:** Siemens S7-1200 (CPU 1215C DC/DC/DC)
* **IDE:** TIA Portal V19
* **Simulación:** S7-PLCSIM, S7-PLCSIM Advanced 6.0, Factory IO
* **HMI / SCADA:** WinCC (TIA Portal), Wecon V-Box

## Temario y Módulos

| Módulo | Tema | Bloques | Estado |
| :---: | :--- | :--- | :---: |
| **M00** | Entorno: proyecto 1215C, PLCSIM, repositorio | — | ✅ |
| **M01** | SCL básico: ciclo de scan, tipos, conversiones, FC | `FC_EscalarAnalogica`, `FC_Escalar4a20` | ✅ |
| **M02** | Timers, flancos y FB_FiltroPT1 | `FB_Antirrebote`, `FB_Intermitente` | ✅ |
| **M03** | Datos: UDT y DB en lugar de marcas `%M` | `UDT_CilindroIO`, `DB_Planta` | ✅ |
| **M04** | Capa de I/O + simulador de planta | `FC_Read_IO`, `FC_Write_IO`, `FB_SimCilindro` | ✅ |
| **M05** | FB de actuador: modos, interlocks, watchdog | `FB_Cilindro` | ✅ |
| **M06** | Máquina de estados (modelo de Moore) | `FB_Secuencia` | ⏳ |
| **M07** | Gestor de modos (FSM jerárquica) | `FB_GestorModos` | ⏳ |
| **M08** | Analógica: modelo de horno, on/off, `PID_Compact` | `FB_SimHorno`, `FB_ControlHisteresis` | ⏳ |
| **M09** | Diagnóstico: historial de transiciones con [FIFO circular](https://github.com/JuniorOlivaresGomez/fifo-circular-scl), alarmas | `FB_HistorialFSM` | ⏳ |
| **M10** | HMI + `DB_SCADA` + V-Box | `FC_SCADA` + pantallas | ⏳ |
| **M11** | Integrador: máquina de mangas | Proyecto completo | ⏳ |
| **M12** | Seguridad funcional y normas | Evaluación de riesgos + arquitectura | ⏳ |

✅ Terminado · 🔄 En curso · ⏳ Pendiente