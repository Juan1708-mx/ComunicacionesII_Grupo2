# Fuentes y enlaces

## Referencias (formato IEEE)

[1] J. G. Proakis and M. Salehi, *Digital Communications*, 5th ed. New York, NY, USA: McGraw-Hill, 2008.
— Modulación M-QAM y M-PSK, energía promedio de la constelación, distancia mínima y probabilidad de error en AWGN. Sustenta la normalización Es = 1 y el cálculo de d_min.

[2] B. Sklar, *Digital Communications: Fundamentals and Applications*, 2nd ed. Upper Saddle River, NJ, USA: Prentice Hall, 2001.
— Relación entre bits por símbolo, tasa de bits y ancho de banda; compromiso entre eficiencia espectral y potencia (plano de eficiencia ancho de banda–potencia).

[3] A. Goldsmith, *Wireless Communications*. Cambridge, U.K.: Cambridge Univ. Press, 2005.
— Modulación adaptativa: elegir constelaciones más densas cuando la SNR lo permite. Sustenta el contexto profesional del escenario.

[4] 3GPP, "NR; Physical layer procedures for data," 3rd Generation Partnership Project, Tech. Spec. TS 38.214, Sec. 5.1.3.1 (tablas de MCS).
— Ejemplo real: en 5G NR el índice de calidad del canal (CQI) define si se usa QPSK, 16QAM o 64QAM; a mejor canal, mayor orden de modulación y mayor eficiencia espectral.

[5] GNU Radio Project, "noise_source_impl.cc," código fuente del bloque Noise Source (gr-analog). [En línea]. Disponible: https://gnuradio.org/cgit/gnuradio.git/tree/gr-analog/lib/noise_source_impl.cc
— Para el tipo complejo, la amplitud se divide entre √2 en cada componente; por eso la potencia total del ruido es noise_amp² y SNR = 1/noise_amp².

[6] GNU Radio Project, "chunks_to_symbols.h," *GNU Radio Manual and C++ API Reference*. [En línea]. Disponible: https://www.gnuradio.org/doc/doxygen/chunks__to__symbols_8h_source.html
— El bloque Chunks to Symbols asigna cada índice (grupo de k bits) a un punto de la tabla de símbolos.

[7] Escuela de Ingenierías Eléctrica, Electrónica y de Telecomunicaciones, UIS, "Proyecto Integrador de Comunicaciones II — Guía del estudiante," 2026.

## Software

- GNU Radio 3.10 — https://www.gnuradio.org
- radioconda (instalador de GNU Radio para Windows) — https://github.com/ryanvolz/radioconda

## Pendiente de verificar por el grupo

- Confirmar el acceso a [1]–[3] en la biblioteca de la UIS y anotar los capítulos usados en el informe.
- Para [4], anotar la versión (Release) consultada.
