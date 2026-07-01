# plc-garage-door

A residential garage door controller built with IEC 61131-3 Structured Text, running on OpenPLC Runtime v4.

Developed as a learning project to explore PLC programming concepts — from basic I/O to safety interlock logic and IT/OT integration via Modbus TCP.

## Features

| Step | Feature                                           | Status |
| ---- | ------------------------------------------------- | ------ |
| 1    | Power indicator lamp                              | ✅     |
| 2    | Open door (UP contactor + limit switch)           | ✅     |
| 3    | Close door (DOWN contactor + limit switch)        | ✅     |
| 4    | Contactor interlock (UP/DOWN never simultaneous)  | ✅     |
| 5    | Obstacle photo-eye (auto-reverse on obstruction)  | ⬜     |
| 6    | Warning lamp (2 Hz flash while door is moving)    | ⬜     |
| 7    | Auto-close timer (close after 5 min if left open) | ⬜     |
| 8    | Remote control via Modbus TCP                     | ⬜     |

## Stack

- Language: Structured Text (IEC 61131-3)
- Runtime: OpenPLC v4
- Integration (step 8): Go + Modbus TCP

## I/O map

| Variable          | Address | Direction | Description                      |
| ----------------- | ------- | --------- | -------------------------------- |
| `UP_BUTTON`       | %I0.1   | Input     | Open pushbutton                  |
| `DOWN_BUTTON`     | %I0.2   | Input     | Close pushbutton                 |
| `OBSTACLE_PE`     | %I0.5   | Input     | Photo‑eye obstruction sensor     |
| `CONTRACTOR_UP`   | %Q0.0   | Output    | Motor up contactor               |
| `CONTRACTOR_DOWN` | %Q0.1   | Output    | Motor down contactor             |
| `POWER_LAMP`      | %Q0.2   | Output    | Power indicator lamp (always ON) |
| `WARNING_LAMP`    | %Q0.3   | Output    | Motion warning lamp (flashing)   |

> **Internal flags (not mapped to physical I/O):**
>
> - `UP_LIMIT` and `DOWN_LIMIT` are simulated based on `DOOR_POSITION` (0 = closed, 100 = open).
> - `DOOR_POSITION` is an `INT` variable tracking door travel.
