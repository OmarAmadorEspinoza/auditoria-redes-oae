# Auditoría y respaldo automatizado de dispositivos de red

![CI](https://github.com/OmarAmadorEspinoza/auditoria-redes-oae/actions/workflows/ci.yml/badge.svg)

Práctica 2B – Programación y Automatización de Redes (CI/CD con Python y Cisco DevNet Sandbox).

**Autor:** Omar Amador Espinoza

## ¿Qué hace?

- Se conecta por SSH (Netmiko) a un dispositivo Cisco IOS XE del DevNet Sandbox.
- Ejecuta solo comandos de lectura: `show running-config`, `show ip interface brief` y `show version`.
- Guarda un respaldo de la configuración en `respaldos/`.
- Extrae el hostname, cuenta las interfaces up/up y genera un reporte de auditoría.
- GitHub Actions valida la sintaxis y ejecuta las pruebas con pytest en cada push.

## Estructura

```
auditoria-redes-oae/
├── .github/workflows/ci.yml   # Pipeline de CI
├── tests/test_auditoria.py    # Pruebas unitarias
├── docs/                      # Documento de evidencias
├── auditoria.py               # Lógica de análisis (sin conexión)
├── ejecutar_auditoria.py      # Conexión SSH y generación de archivos
├── requirements.txt
└── .gitignore
```

## Uso

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# Pruebas
python -m pytest -v

# Ejecución contra el Sandbox (credenciales por variables de entorno)
export NET_DEVICE_HOST="..."
export NET_DEVICE_USER="..."
export NET_DEVICE_PASSWORD="..."
export NET_DEVICE_TYPE="cisco_xe"
export NET_DEVICE_PORT="22"
python ejecutar_auditoria.py
```

## CI vs CD

| Etapa | Qué pasa |
|-------|----------|
| CI | GitHub Actions instala dependencias, valida sintaxis y ejecuta pytest. |
| CD / ejecución controlada | Se ejecuta manualmente el script validado contra el Sandbox. |

## Seguridad

- No hay credenciales en el código ni en el repositorio.
- La carpeta `respaldos/` está en `.gitignore` porque contiene configuraciones reales.

## Documentación

Evidencias y conclusión de la práctica: [`docs/Practica_2B_OAE.pdf`](docs/Practica_2B_OAE.pdf)
