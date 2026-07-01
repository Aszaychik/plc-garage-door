# plc-garage-door

A residential garage door controller built with IEC 61131-3 Structured Text, running on OpenPLC Runtime v4.

Developed as a learning project to explore PLC programming concepts — from basic I/O to safety interlock logic and IT/OT integration via Modbus TCP.

## Features

| Step | Feature                                           | Status |
| ---- | ------------------------------------------------- | ------ |
| 1    | Power indicator lamp                              | 🔄     |
| 2    | Open door (UP contactor + limit switch)           | ⬜     |
| 3    | Close door (DOWN contactor + limit switch)        | ⬜     |
| 4    | Contactor interlock (UP/DOWN never simultaneous)  | ⬜     |
| 5    | Obstacle photo-eye (auto-reverse on obstruction)  | ⬜     |
| 6    | Warning lamp (2 Hz flash while door is moving)    | ⬜     |
| 7    | Auto-close timer (close after 5 min if left open) | ⬜     |
| 8    | Go remote control via Modbus TCP                  | ⬜     |

## Stack

- Language: Structured Text (IEC 61131-3)
- Runtime: OpenPLC v4
- Integration (step 8): Go + Modbus TCP

## I/O map

| Variable       | Address | Direction | Description                    |
| -------------- | ------- | --------- | ------------------------------ |
| POWER_ON       | %I0.0   | Input     | Main power switch              |
| OPEN_PB        | %I0.1   | Input     | Open pushbutton                |
| CLOSE_PB       | %I0.2   | Input     | Close pushbutton               |
| UP_LIMIT       | %I0.3   | Input     | Door fully open limit switch   |
| DOWN_LIMIT     | %I0.4   | Input     | Door fully closed limit switch |
| OBSTACLE_PE    | %I0.5   | Input     | Photo-eye obstruction sensor   |
| UP_CONTACTOR   | %Q0.0   | Output    | Motor up direction contactor   |
| DOWN_CONTACTOR | %Q0.1   | Output    | Motor down direction contactor |
| GARAGE_LAMP    | %Q0.2   | Output    | Power indicator lamp           |
| WARNING_LAMP   | %Q0.3   | Output    | Motion warning lamp            |

## Conventional commits

This project follows [Conventional Commits](https://www.conventionalcommits.org/).

```
feat(step-1): add power indicator lamp
feat(step-2): add open door logic with UP contactor latch
feat(step-3): add close door logic with DOWN contactor latch
fix(step-4): enforce contactor interlock via state bits
feat(step-5): add obstacle photo-eye reversal
feat(step-6): add 2Hz warning lamp using TP oscillator
feat(step-7): add auto-close timer after 5 min
feat(step-8): integrate Go Modbus TCP remote control
```

## Local setup

```bash
# Install OpenPLC Runtime
git clone https://github.com/openplc/openplc-runtime
cd openplc-runtime && ./install.sh

# Run runtime
sudo systemctl start openplc-runtime

# Open project in OpenPLC Editor
openplc ~/Developer/plc-garage-door
```

## License

MIT
