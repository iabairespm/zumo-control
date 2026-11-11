# Zumo Control

Control web para un robot zumo (Arduino UNO + L298N) con módulo Bluetooth BLE
(HM-10 / BT05 / "HC-06 BLE"). Usa Web Bluetooth: abrir en **Chrome para Android**.

Envía los comandos de una letra que entiende `zumo_bt.ino`:
`F B L R S` (mover / stop), `G I H J` (diagonales), `1`–`9` y `q` (velocidad).

Mantener apretado un botón mueve el robot; al soltar se envía `S`.
