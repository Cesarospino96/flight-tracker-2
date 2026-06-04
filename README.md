# ✈️ Rastreador de vuelos BOG → BAQ

Monitorea precios de vuelo **Bogotá → Barranquilla** el **9 de agosto 2026**,
filtra solo vuelos después de las **6PM**, y te avisa por **WhatsApp** cuando
el precio cae por debajo de **$150.000 COP** o alcanza un nuevo mínimo histórico.

Corre automáticamente cada hora usando **GitHub Actions** (gratis).

---

## 📦 Estructura

```
flight-tracker/
├── tracker.py              ← Script principal
├── requirements.txt        ← Dependencias Python
├── price_history.csv       ← Historial de precios (se genera al correr)
└── .github/
    └── workflows/
        └── track.yml       ← Automatización GitHub Actions
```

---

## 🚀 Configuración paso a paso

### 1. Obtener clave SerpAPI (gratis)

1. Regístrate en [serpapi.com](https://serpapi.com) — plan gratuito: 100 búsquedas/mes
2. Copia tu **API Key** desde el dashboard

### 2. Configurar Twilio WhatsApp

1. Crea cuenta en [twilio.com](https://twilio.com) — trial gratuito incluye crédito
2. Activa el **WhatsApp Sandbox**:
   - Ve a *Messaging → Try it out → Send a WhatsApp message*
   - Desde tu WhatsApp, envía el código que te indica (ej: `join silver-horse`) al número de Twilio
3. Anota:
   - **Account SID** (empieza con `AC...`)
   - **Auth Token**
   - **Número sandbox**: `whatsapp:+14155238886` (o el que te asigne)
   - **Tu número**: `whatsapp:+573001234567` (con código de país)

### 3. Crear repositorio en GitHub

```bash
git init
git add .
git commit -m "Rastreador de vuelos BOG-BAQ"
git remote add origin https://github.com/TU_USUARIO/flight-tracker.git
git push -u origin main
```

### 4. Agregar Secrets en GitHub

En tu repositorio → **Settings → Secrets and variables → Actions → New repository secret**

| Nombre del Secret         | Valor                                      |
|---------------------------|--------------------------------------------|
| `SERPAPI_KEY`             | Tu clave de SerpAPI                        |
| `TWILIO_ACCOUNT_SID`      | AC...                                      |
| `TWILIO_AUTH_TOKEN`       | Tu auth token de Twilio                    |
| `TWILIO_WHATSAPP_FROM`    | `whatsapp:+14155238886`                    |
| `TWILIO_WHATSAPP_TO`      | `whatsapp:+57XXXXXXXXXX` (tu número)       |

### 5. Probar manualmente

En GitHub → **Actions → Rastreador de vuelos BOG→BAQ → Run workflow**

---

## ⚙️ Personalizar

En `tracker.py`, puedes cambiar:

```python
MAX_PRICE = 150_000   # Sube o baja el umbral de alerta (COP)
MIN_HOUR  = 18        # Hora mínima de salida (formato 24h)
DATE      = "2026-08-09"
```

---

## 📊 Historial de precios

Cada ejecución guarda los precios en `price_history.csv`. Puedes descargarlo
desde la pestaña **Actions → [corrida] → Artifacts** para analizar la tendencia.

---

## 💡 Recibirás una alerta cuando:

- El precio más barato sea **menor a $150.000 COP**, O
- Se registre un **nuevo mínimo histórico** (aunque esté sobre el umbral)
