# Aqualia Integration for Home Assistant

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge)](https://github.com/hacs/integration)
[![Home Assistant](https://img.shields.io/badge/Home--Assistant-Sensor-blue.svg?style=for-the-badge)](https://www.home-assistant.io)

Integración personalizada para Home Assistant que te permite consultar el consumo de agua directamente desde la **Oficina Virtual de Aqualia** e integrarlo en tu panel de Energía.

La integración obtiene los datos históricos reales reportados por tu contador inteligente y los inyecta de forma retroactiva como estadísticas a largo plazo (LTS) en Home Assistant, evitando vacíos y desfases temporales.

---

## Características

- 💧 **Sensor de Volumen de Agua**: Reporta el volumen acumulado de consumo (en litros).
- 📊 **Panel de Energía**: Totalmente compatible con la sección de Agua del panel de Energía oficial de Home Assistant.
- 🕒 **Histórico Retroactivo**: Inyecta automáticamente curvas de consumo históricas por hora de forma retroactiva para que no pierdas precisión en tus estadísticas a largo plazo.
- 🇪🇸 **Traducciones**: Flujo de configuración amigable disponible en Español e Inglés.

---

## Instalación

### Opción 1: HACS (Recomendada)

1. Abre **HACS** en tu interfaz de Home Assistant.
2. Haz clic en los tres puntos verticales en la esquina superior derecha y selecciona **Repositorios personalizados**.
3. Pega la URL de este repositorio: `https://github.com/mcrespov/aqualiaHS`
4. Selecciona **Integración** como categoría y haz clic en **Añadir**.
5. Busca la integración **Aqualia** en la tienda de HACS y haz clic en **Descargar**.
6. Reinicia Home Assistant.

### Opción 2: Instalación Manual

1. Descarga el código de este repositorio.
2. Copia la carpeta `custom_components/aqualia/` completa en el directorio `custom_components/` de tu instalación de Home Assistant.
3. Reinicia Home Assistant.

---

## Configuración

Una vez instalada la integración y tras reiniciar Home Assistant:

1. Ve a **Ajustes > Dispositivos y Servicios**.
2. Haz clic en **Añadir integración** en la esquina inferior derecha.
3. Busca **Aqualia** en la lista.
4. Introduce el **Usuario** y **Contraseña** de tu cuenta de la Oficina Virtual de Aqualia.
5. Selecciona la dirección de suministro del contrato que deseas monitorizar del desplegable.
6. ¡Listo! Se creará un nuevo sensor con tu número de contrato: `sensor.aqualia_XXXXXX`.

---

## Integración con el Panel de Energía

Para añadir el consumo de agua a tu panel de energía:

1. Ve a **Ajustes > Tableros > Energía**.
2. En la sección **Consumo de agua**, haz clic en **Añadir sensor de agua**.
3. Selecciona tu sensor `sensor.aqualia_XXXXXX` de la lista de opciones.
4. Guarda los cambios. Los datos históricos comenzarán a renderizarse progresivamente en tu tablero.

---

## Solución de Problemas

- **El sensor muestra `disponible` pero no hay datos iniciales**:
  El API de Aqualia solo actualiza lecturas periódicamente. La primera carga de datos puede tardar un poco dependiendo de la Oficina Virtual. Puedes usar el servicio `aqualia.reset_statistics` en **Herramientas de Desarrollador > Servicios** para forzar una importación del histórico completo desde el alta de tu contrato.
- **Frecuencia de actualización**:
  Por defecto, la integración realiza peticiones de actualización cada 1 hora para evitar el bloqueo del IP por parte de los servidores de Aqualia.
