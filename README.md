# Otamatone2MIDI

Repositorio con parches de Pure Data y un proyecto de Carla para usar un Otamatone como controlador MIDI.

**Descripción:**
- Este repositorio contiene parches en Pure Data (.pd) que detectan el tono/nota desde la señal de audio del Otamatone y la convierten a mensajes MIDI, además de un archivo de proyecto de Carla guardado (`otamatone.carxp`).

**Archivos incluidos:**
- `otamatone_pitch.pd`: parche principal para detección de pitch y conversión a MIDI.
- `otamatone_notes.pd`: mapeo de notas / utilidades para generar notas MIDI.
- `test_otamatone.pd`: parche de pruebas y debug.
- `otamatone.carxp`: proyecto de Carla con los plugins y rutas previstas.

**Requisitos:**
- QJackCtl (interfaz para JACK)
- Pure Data (pd)
- Carla (host de plugins, usa JACK y MIDI)
- (opcional) `a2jmidid` o herramientas similares para puentear MIDI ALSA ⇄ JACK si es necesario

En distribuciones basadas en Debian/Ubuntu:

```
sudo apt update
sudo apt install qjackctl puredata carla a2jmidid
```

**Pasos rápidos de uso:**
1. Abrir `QJackCtl` y arrancar el servidor JACK (ajusta sample rate y frames/buffer según tu tarjeta).
2. Ejecutar `a2jmidid -e` si necesitas exportar puertos MIDI ALSA a JACK (opcional, depende de tu configuración).
3. Abrir Pure Data y cargar `otamatone_pitch.pd` (o `test_otamatone.pd` para pruebas).
4. En Pure Data: `Media` → `Audio Settings` → seleccionar `JACK` como backend y activar `DSP`.
5. Conectar la entrada de audio (micrófono o línea donde conectes el Otamatone) al parche de Pure Data.
6. Abrir `Carla` y cargar el proyecto `otamatone.carxp` o los plugins que prefieras.
7. Usar el diálogo de conexiones de JACK (QJackCtl o Carla Patchbay) para enrutear la salida MIDI de Pure Data hacia la entrada MIDI del instrumento en Carla.
8. Toca el Otamatone: Pure Data detecta pitch/nota y envía mensajes MIDI; Carla recibe dichos mensajes y controla los plugins.

**Consejos y solución de problemas:**
- Asegúrate de que JACK está corriendo antes de iniciar Pure Data o Carla.
- Ajusta el tamaño de buffer y sample rate si hay latencia o clicks.
- Si no ves puertos MIDI de Pure Data, verifica la configuración MIDI en Pd y considera usar `a2jmidid`.
- Usa `QJackCtl` → `Connect` para comprobar y conectar manualmente puertos de audio y MIDI.

