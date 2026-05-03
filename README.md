# arca

Plugin de Claude Code — economía argentina en tiempo real.

## Qué hace

`/arca` trae datos económicos de Argentina al instante: tipos de cambio, inflación, valor de la canasta básica y conversión de sueldos. Usa APIs oficiales y públicas, sin intermediarios.

## Instalación

```bash
claude --plugin-dir /ruta/a/arca
```

## Uso

```
/arca                    # todos los tipos de cambio
/arca dolar              # idem
/arca inflacion          # IPC último dato + acumulado
/arca sueldo 800000      # convierte $800k a dólares en todos los tipos
/arca canasta            # canasta básica total e indigencia
/arca tarifas            # servicios públicos actualizados
```

## Fuentes

- **Dólar:** [dolarapi.com](https://dolarapi.com) / [bluelytics](https://bluelytics.com.ar) (respaldo)
- **Inflación y canasta:** [APIs del Estado](https://apis.datos.gob.ar) — INDEC oficial
- **Tarifas:** ENRE, ENARGAS, Boletín Oficial

Los datos son públicos y gratuitos. Este plugin no almacena ni transmite información del usuario.
