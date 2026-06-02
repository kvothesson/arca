# arca

Compatible con **Claude Code** y **OpenAI Codex** — economía argentina en tiempo real.

## Qué hace

`/arca` trae datos económicos de Argentina al instante usando APIs oficiales y públicas.

## Instalación

```bash
claude --plugin-dir /ruta/a/arca
```

## Comandos y ejemplos

### `/arca` o `/arca dolar`

```
💵 Dólar — 3 may 2026

Oficial     $1.365  / $1.415
Blue        $1.380  / $1.400
Bolsa (MEP) $1.437  / $1.448
CCL         $1.492  / $1.494
Mayorista   $1.382  / $1.391
Cripto      $1.478  / $1.478
Tarjeta     $1.774  / $1.839

              (compra / venta)

Brecha blue vs oficial: +1,9%
```

---

### `/arca inflacion`

```
📈 Inflación — IPC Nacional

Último mes (mar 2026):   3,38%
Últimos 3 meses:         9,44%
Últimos 12 meses:       32,61%
Acumulado 2026:          9,44%

Fuente: INDEC — apis.datos.gob.ar
```

---

### `/arca sueldo 800000`

```
💼 Sueldo $800.000 ARS

Blue        u$s 571
MEP         u$s 552
CCL         u$s 535
Oficial     u$s 565
Tarjeta     u$s 434

Canasta básica total (región Pampeana, dic 2025): $417.680
```

---

### `/arca canasta`

```
🛒 Canasta Básica — dic 2025
     (región Pampeana — referencia AMBA)

No pobreza:    $417.680
No indigencia: $xxx.xxx

Variación vs mes anterior:  +3,8%
Variación vs año anterior:  +xx,x%

Fuente: INDEC. Dato más reciente disponible.
```

---

### `/arca tarifas`

Busca en fuentes oficiales (ENRE, ENARGAS, Boletín Oficial) y presenta lo más reciente con fecha y fuente.

---

## Fuentes

- **Dólar:** [dolarapi.com](https://dolarapi.com) / [bluelytics](https://bluelytics.com.ar) (respaldo)
- **Inflación y canasta:** [apis.datos.gob.ar](https://apis.datos.gob.ar) — INDEC oficial
- **Tarifas:** ENRE, ENARGAS, Boletín Oficial

Los datos son públicos y gratuitos. Este plugin no almacena ni transmite información del usuario.
