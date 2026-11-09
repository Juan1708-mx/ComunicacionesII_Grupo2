# Bitácora del proyecto — Grupo 2 (Escenario S4)

## 15/10/2026 — Ficha de decisión técnica

- Se eligió el escenario S4: aumentar la tasa de datos sin aumentar la tasa de símbolos.
- Decisiones: comparar QPSK y 16QAM con la misma Rs, SPS y fs (paquete A: Rs = 32 ksym/s, SPS = 8, fs = 256 kS/s), partiendo de `Modulaciones_basadas_en_constelaciones_AWGN.grc`.
- Perturbación: solo AWGN. Variable: nivel de ruido común. Pruebas: referencia, suave, media y fuerte.
- Hipótesis H1: con la misma Rs, 16QAM transportará más bits/s pero será visualmente más sensible al mismo nivel de ruido que QPSK.

## 07/11/2026 — Revisión de la guía y de los GRC del curso

- Se revisaron los cuatro GRC suministrados. Solo se usa el de constelaciones con AWGN; los de FSK quedan como referencia.
- Hallazgos del GRC base:
  - La tabla de símbolos viene con OOK `(0, 1)`.
  - La constelación tiene autoescala, lo que impide comparar capturas entre pruebas.
  - Rs, SPS y samp_rate ya coinciden con el paquete A de la ficha.
- Decisión: crear dos copias (`S4_QPSK_AWGN_Grupo2.grc` y `S4_16QAM_AWGN_Grupo2.grc`), cambiar solo la tabla de símbolos y fijar los ejes de la constelación en ±2.
- Decisión: normalizar las constelaciones a potencia promedio unitaria (QPSK ÷ √2, 16QAM ÷ √10) para que el mismo `noise_amp` dé el mismo SNR en ambas. Se usó mapeo Gray.

## 07/11/2026 — Prueba A (referencia)

- Se verificó QPSK: 4 puntos en (±0.707, ±0.707) y niveles ±0.707 en la señal temporal.
- Se verificó 16QAM: cuadrícula 4×4 en ±0.316 y ±0.949.
- En las dos modulaciones la PSD tiene forma sinc² con nulos en ±32 kHz (BW = 64 kHz).
- **Dificultad:** *File → Screen Capture* de GRC falló ("Failed to generate screen shot"). **Solución:** se usaron capturas de Windows (Win + Shift + S); más tarde la función sí funcionó.
- **Dificultad:** sin mouse no había clic derecho para configurar las gráficas. **Solución:** la configuración se hizo en las propiedades de los bloques y la pantalla se congeló con Win + Shift + S.
- **Dificultad:** la primera PSD quedó ampliada por un toque accidental en el touchpad. **Solución:** se reinició la simulación para recuperar la escala original.

## 08/11/2026 — Pruebas B, C y D

- Niveles elegidos: `noise_amp` = 0.05, 0.20 y 0.35 (SNR de 26, 14 y 9.1 dB). Se escogieron calculando d_min/2σ para que la prueba media separara el comportamiento de las dos modulaciones.
- Resultado: 16QAM se degrada en C (las nubes se tocan) y pierde la cuadrícula en D; QPSK mantiene sus 4 grupos incluso en D.
- **Dificultad:** la señal temporal de QPSK C quedó con escala de ±3.5. **Solución:** se repitió la captura con la escala estándar de ±2.

## 08–09/11/2026 — Reproducibilidad y figuras

- Se detectó que los 256 puntos de la señal temporal se habían configurado durante la ejecución y no estaban guardados en el GRC. Se fijaron en los bloques (Time Sink = 256 puntos, Frequency Sink con promedio Medium) y se guardaron los archivos.
- Se elaboraron las Figuras 1 (escenario contextual) y 2 (diagrama técnico) con apoyo de IA, y se revisaron sus parámetros.
- Se armó la tabla de pruebas con el análisis de cada prueba y el README.

## Pendiente

- Informe IEEE (LaTeX).
- Socialización.
- Subir los archivos al repositorio y revisar la lista de verificación de la guía.
