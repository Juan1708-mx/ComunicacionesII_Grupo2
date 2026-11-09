# Tabla de pruebas — Escenario S4 (QPSK vs 16QAM con AWGN) — Grupo 2

**Parámetros fijos en todas las pruebas:** Rs = 32 kbaud · SPS = 8 · fs = Rs × SPS = 256 kS/s · pulso rectangular (`h = [1]*Sps`) · ruido AWGN complejo (`analog_noise_source`, seed = 0) · constelaciones normalizadas a Es = 1.

**Única variable que cambia:** `noise_amp`.

**Archivos GRC:** `S4_QPSK_AWGN_Grupo2.grc` y `S4_16QAM_AWGN_Grupo2.grc` (copias de `Modulaciones_basadas_en_constelaciones_AWGN.grc`; solo se cambió la tabla de símbolos, la escala fija de la constelación y la visualización: 256 puntos en la señal temporal y PSD con promedio *Medium*).

## Relaciones usadas

| Magnitud | Fórmula | QPSK | 16QAM |
|---|---|---|---|
| Bits por símbolo | k = log2(M) | 2 | 4 |
| Tasa de bits | Rb = Rs · k | 64 kbps | 128 kbps |
| Tasa de muestreo | fs = Rs · SPS | 256 kS/s | 256 kS/s |
| Ancho de banda entre nulos (pulso rectangular) | BW = 2 · Rs | 64 kHz | 64 kHz |
| Eficiencia espectral | Rb / BW | 1 bit/s/Hz | 2 bit/s/Hz |
| Distancia mínima (Es = 1) | QPSK: √2 · 16QAM: 2/√10 | 1.414 | 0.632 |
| SNR por muestra | SNR = Es / noise_amp² → −20·log10(noise_amp) dB | igual | igual |

Con la misma potencia, los puntos de 16QAM están 2.24 veces más cerca (≈ 7 dB): para la misma separación relativa frente al ruido, 16QAM necesita unos 7 dB más de SNR.

## Tabla resumen

| Prueba | Severidad | noise_amp | SNR por muestra | QPSK: d_min/2σ | QPSK: Ps teórica* | 16QAM: d_min/2σ | 16QAM: Ps teórica* |
|---|---|---|---|---|---|---|---|
| A | Referencia | 0 | ∞ | ∞ | 0 | ∞ | 0 |
| B | Suave | 0.05 | 26.0 dB | 20.0 | < 10⁻¹² | 8.94 | < 10⁻¹² |
| C | Media | 0.20 | 14.0 dB | 5.00 | 5.7·10⁻⁷ | 2.24 | 3.8·10⁻² |
| D | Fuerte | 0.35 | 9.1 dB | 2.86 | 4.3·10⁻³ | 1.28 | 2.8·10⁻¹ |

\* σ = noise_amp/√2 es la desviación del ruido por eje (I o Q). Ps es la probabilidad teórica de decidir un símbolo equivocado a partir de **una muestra**, sin filtro acoplado (el GRC no tiene receptor). Un receptor con filtro acoplado promediaría las 8 muestras del símbolo y ganaría 10·log10(8) ≈ 9 dB.

Los valores en dB de la PSD se leyeron sobre las capturas y son aproximados.

## Análisis por prueba

### A · Referencia (noise_amp = 0)

**QPSK.** La constelación muestra los 4 símbolos ideales en (±0.707, ±0.707), con potencia promedio unitaria. La señal temporal tiene escalones de 31.25 µs (1/Rs) con niveles ±0.707 en I y Q. La PSD tiene la forma sinc² del pulso rectangular: pico del lóbulo principal ≈ −28 dB, nulos en ±32, ±64 y ±96 kHz (múltiplos de Rs) y primer lóbulo lateral ≈ 13 dB por debajo del pico. El ancho de banda entre nulos es 64 kHz = 2Rs.

**16QAM.** La constelación muestra 16 símbolos en una cuadrícula 4×4 (±0.316, ±0.949). Cada eje toma 4 niveles, por lo que se transportan 4 bits por símbolo y Rb sube a 128 kbps con la misma Rs. La PSD es igual a la de QPSK (mismo nivel, mismos nulos, mismo BW de 64 kHz): el ancho de banda depende de Rs y del pulso, no de M. Esto confirma la primera parte de la hipótesis H1. La distancia mínima baja de 1.414 a 0.632.

### B · Suave (noise_amp = 0.05, SNR = 26 dB)

**QPSK.** Cada símbolo se convierte en una nube pequeña, muy lejos de los umbrales de decisión (d_min/2σ = 20). En la señal temporal aparece un rizado leve sobre los niveles ±0.707. En la PSD los nulos dejan de ser profundos (≈ −65 dB) porque el ruido blanco empieza a llenarlos; el lóbulo principal no cambia.

**16QAM.** Las 16 nubes siguen separadas y la cuadrícula se distingue sin dificultad (d_min/2σ = 8.9). Los 4 niveles de I y Q se reconocen en el tiempo. La PSD es prácticamente igual a la de QPSK B, lo que muestra que el ruido agregado es el mismo en las dos simulaciones. Este nivel marca el inicio de la degradación sin consecuencias prácticas.

### C · Media (noise_amp = 0.20, SNR = 14 dB) — condición principal

**QPSK.** Las 4 nubes crecen, pero siguen claramente separadas por el centro de la constelación (d_min/2σ = 5, Ps ≈ 6·10⁻⁷). En la señal temporal los dos niveles se distinguen a pesar del ruido. En la PSD el piso sube unos 12 dB respecto a B (20·log10(0.20/0.05) = 12 dB) y casi cubre los nulos; el lóbulo principal sigue visible.

**16QAM.** Con el mismo ruido, las nubes vecinas ya se tocan y la cuadrícula apenas se reconoce (d_min/2σ = 2.24, Ps ≈ 4·10⁻²). En la señal temporal es difícil separar los niveles ±0.316 de los ±0.949. La PSD es igual a la de QPSK C. Esta prueba resume el compromiso del escenario: con el mismo ancho de banda y el mismo ruido, 16QAM transporta el doble de bits, pero sus decisiones son unas 65 000 veces más propensas a error.

### D · Fuerte (noise_amp = 0.35, SNR = 9.1 dB)

**QPSK.** Las nubes son grandes y algunas muestras llegan cerca de los ejes, pero todavía se distinguen 4 grupos (d_min/2σ = 2.86, Ps ≈ 4·10⁻³). En la señal temporal los dos niveles se reconocen solo en promedio. En la PSD el piso sube ≈ 5 dB más (20·log10(0.35/0.20) = 4.9 dB), los nulos desaparecen y solo se distingue el lóbulo principal.

**16QAM.** La constelación es una nube continua; la cuadrícula desaparece (d_min/2σ = 1.28, Ps ≈ 0.28). En la señal temporal no se pueden identificar los 4 niveles. La PSD es igual a la de QPSK D. Con este nivel de ruido, 16QAM no sería utilizable sin un receptor con filtro acoplado, codificación o más potencia, mientras que QPSK aún conserva sus símbolos.

## Síntesis QPSK vs 16QAM

| Aspecto | QPSK | 16QAM | Evidencia |
|---|---|---|---|
| Rb con Rs = 32 kbaud | 64 kbps | 128 kbps (×2) | Cálculo y nº de niveles en la señal temporal |
| Ancho de banda | 64 kHz | 64 kHz (igual) | PSD de A: nulos en ±32 kHz en ambas |
| Eficiencia espectral | 1 bit/s/Hz | 2 bit/s/Hz | Rb / BW |
| Distancia mínima (Es = 1) | 1.414 | 0.632 (≈ 7 dB menos) | Constelaciones de A |
| Primera prueba con símbolos que se tocan | Ninguna (en D aún se separan) | C (14 dB) | Constelaciones de C y D |
| Efecto del ruido en la PSD | Piso sube igual | Piso sube igual | PSD de B, C, D |

**Conclusión:** la hipótesis H1 se confirma. Con la misma Rs, SPS, fs y ruido, 16QAM duplica la tasa de bits sin aumentar el ancho de banda, pero su menor distancia entre símbolos la hace visiblemente más sensible al AWGN: se degrada en la prueba media, mientras que QPSK resiste incluso la prueba fuerte. La PSD no permite ver esta diferencia (el espectro es igual en ambas); la constelación sí.

## Notas para las figuras

- La gráfica de constelación del GUI es más ancha que alta, por lo que las nubes se ven alargadas en horizontal. El ruido es circular (igual σ en I y Q); conviene aclararlo en el pie de figura.
- Las constelaciones muestran todas las muestras (8 por símbolo), no un valor por símbolo, porque el GRC no incluye un receptor.
