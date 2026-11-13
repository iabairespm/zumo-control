# Zumo Control — AXEL - PM

Control web para un robot zumo (Arduino UNO + L298N) con módulo Bluetooth **BLE**
(HM-10 / BT05 / "HC-06 BLE"). Usa Web Bluetooth: abrir en **Chrome para Android**.

Página publicada: https://iabairespm.github.io/zumo-control/

> Los módulos BLE no funcionan con apps de Bluetooth clásico (por ejemplo "Bluetooth RC Controller").
> Sí funcionan esta página, Serial Bluetooth Terminal (pestaña LE) y Bluetooth Electronics.

## Funciones

- **Joystick de 8 direcciones** (cuanto más lejos del centro, más rápido) o **D-PAD**; se recuerda la elección.
- **Marchas 1–5** (30 / 50 / 60 / 80 / 100 %) y **TURBO** (100 % mientras se mantiene).
- **STOP = freno de emergencia**: frena y bloquea todo movimiento mientras se mantiene apretado.
- **Modo claro / oscuro** (sigue el tema del celular; también `?tema=light` o `?tema=dark`).
- Pantalla completa en horizontal, pantalla siempre encendida, vibración.
- Frena sola si la página pasa a segundo plano.
- Funciona **sin internet** una vez abierta (PWA con service worker).

## Conexión

- Busca servicios UART BLE en este orden: `0xFFE0`, `0xFFF0`, Nordic UART.
- Mientras el robot se mueve, reenvía el comando cada **150 ms** (el sketch frena solo si deja de recibir 500 ms).
- Quieto, manda `S` cada **2 s** para que el módulo/Android no corte la conexión por inactividad.
- Si la conexión se corta, **reintenta reconectar sola** (hasta 5 veces) sin volver a elegir el dispositivo.

## Protocolo (1 carácter por comando)

| Comando | Acción |
|---|---|
| `F` `B` | adelante / atrás |
| `L` `R` | giro izquierda / derecha |
| `G` `I` | adelante-izquierda / adelante-derecha |
| `H` `J` | atrás-izquierda / atrás-derecha |
| `S` `D` | stop (freno) |
| `0`–`9` | velocidad 0–90 % |
| `q` | velocidad 100 % |

La página manda velocidad y dirección juntas (ej. `8F`). Otros caracteres se ignoran.
El sketch del robot es `zumo_bt.ino` (v2: kick-start, freno activo y failsafe).

## Publicar cambios

Se publica con GitHub Pages desde la rama `main`. **Al cambiar archivos, subir la versión de
`CACHE` en `sw.js`** para que los celulares tomen la versión nueva al abrirla con internet.
