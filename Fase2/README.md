# Fase 2 — Tx con RRC y receptor (Grupo 2, escenario S4)

Archivos:
- `S4_QPSK_TxRx_RRC_Grupo2.grc`
- `S4_16QAM_TxRx_RRC_Grupo2.grc`

Los dos son iguales salvo por la tabla de símbolos. Se construyeron a partir de los GRC de la Fase 1 (`S4_*_AWGN_Grupo2.grc`), siguiendo la Guía 2. No se recibió el archivo `..._Base_Tx.grc`.

## Cadena
Fuente de bits → símbolos (tabla normalizada, Gray) → **RRC Tx** (β = 0.35, span = 11, 89 coeficientes) → Throttle → **+ AWGN** (`noise_amp`, mismo modelo de la Fase 1) → **RRC Rx (filtro acoplado)** → **diagrama de ojo** → **Keep M in N** (1 de cada 8, `fase_muestreo`) → **constelación recuperada** → **Constellation Decoder** → comparación con los símbolos Tx retardados (`retardo_simbolos` = 11) → **SER estimada** (promedio de 10 000 símbolos).

## Controles en la ventana
| Control | Valor inicial | Para qué |
|---|---|---|
| Amplitud de ruido AWGN | 0 | Nivel de ruido de cada prueba |
| Roll-off del RRC (beta) | 0.35 | Ver cómo cambia la PSD (0.1 a 1.0) |
| Fase de muestreo | 0 | Instante de muestreo dentro del símbolo; 0 = apertura máxima del ojo |
| Retardo de alineación Tx-Rx | 11 | Retardo total de los dos RRC: 88 muestras = 11 símbolos |

## Resultados medidos en GNU Radio
| Prueba | noise_amp | SNR tras el filtro acoplado | SER QPSK medida (teoría) | SER 16QAM medida (teoría) |
|---|---|---|---|---|
| A | 0 | ∞ | 0 (0) | 0 (0) |
| B | 0.35 | 18.1 dB | 0 (≈ 0) | 5.0×10⁻⁴ (4.8×10⁻⁴) |
| C | 0.70 | 12.1 dB | 1.0×10⁻⁴ (5×10⁻⁵) | 0.103 (0.104) |
| D | 1.00 | 9.0 dB | 4.7×10⁻³ (5.0×10⁻³) | 0.282 (0.283) |

Pruebas adicionales (sin ruido):
- β = 0.1 / 0.35 / 1.0: ancho de banda ≈ 35.2 / 43.2 / 64 kHz.
- Fase de muestreo 4 (16QAM): SER = 0.788. Muestrear en el cruce del ojo arruina la recepción.

## Contenido de la carpeta
- `grc/`: los dos flujogramas.
- `capturas/`: las 34 capturas de pantalla (`F2_<mod>_<prueba>_<n>`).
- `figuras/`: figuras compuestas del informe.
- `Informe_fase_2.pdf`: documento IEEE de la Fase 2.
