# Crazyflie Web-Simulator

Flugcode (Python, im Stil der cflib-`MotionCommander`) direkt im Browser ausführen und in **3D** ansehen — ganz ohne Installation.

**Live:** https://jscepik-source.github.io/crazyflie-web-simulator/

## Features
- Python im Browser via **Pyodide** (kein Server, kein Setup)
- **3D-Visualisierung** (Three.js): Drohne mit drehenden Rotoren, höhenfarbene Flugbahn, drehbare Kamera
- **Hindernisse** (Säulen) mit simuliertem **Multiranger** zum Ausweichen
- **Ringe** (Tore) zum Durchfliegen – werden grün, sobald durchflogen
- **Säulen & Ringe frei im Code positionierbar** (`OBSTACLES` / `RINGS`)
- **Live-Geschwindigkeitsdiagramm** (horizontal/vertikal)

## Nutzung
`index.html` öffnen (oder die Live-URL). Flugcode links eingeben → **▶ Simulieren**.

## Echter cflib-Code einfügbar
Typischer Crazyflie-Code läuft direkt – ein Kompatibilitäts-Shim leitet ihn auf die Sim-Drohne um:

```python
import cflib.crtp
from cflib.crazyflie import Crazyflie
from cflib.crazyflie.syncCrazyflie import SyncCrazyflie
from cflib.positioning.motion_commander import MotionCommander
from cflib.utils.multiranger import Multiranger

with SyncCrazyflie(URI, cf=Crazyflie()) as scf:
    with Multiranger(scf) as mr:
        with MotionCommander(scf, default_height=1.0) as mc:
            mc.forward(0.5)
```

Hinweise: kein echtes pybullet/keine Hardware; `time.sleep()` treibt die Simulation voran; der Multiranger erkennt die Säulen (`OBSTACLES`).
