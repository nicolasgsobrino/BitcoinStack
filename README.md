# BitcoinStack


## 🧱 Capa 1: Infraestructura base (mínimo viable)

Esta capa incluye todo lo necesario para que BitcoinStack funcione como producto desde el primer despliegue:

### 1. Despliegue del nodo Bitcoin

* Software: `bitcoind` (Bitcoin Core)
* Configuración:

  * Modo pruned o full
  * RPC habilitado (para APIs)
  * Directorios persistentes (`.bitcoin`)
* Automatización:

  * Script en Bash / Ansible / Terraform para instalarlo en cloud o servidor local
  * Healthcheck + logs

### 2. Despliegue del nodo Lightning

* Software: `LND` o `Core Lightning`
* Requisitos:

  * Conexión directa con el nodo `bitcoind`
  * Gestión de wallet integrada (autogenerada o importada)
  * Canal preconfigurado con nodo de liquidez (opcional)
* Automatización:

  * Instalación y configuración básica
  * Apertura de canal inicial
  * Webhook para detectar pagos

### 3. API REST BitcoinStack (backend)

* Framework: Flask / FastAPI (Python), o Express (Node)
* Funciones principales:

  * Consultar balance y transacciones
  * Crear pagos (on-chain y LN)
  * Crear facturas
  * Enviar sats
  * Leer eventos (pagos recibidos, etc.)
* Seguridad:

  * Autenticación por token/API key
  * Logs de auditoría

### 4. Panel de Administración (frontend)

* Framework: React / Vue / Svelte
* Funcionalidades:

  * Dashboard con actividad
  * Envío y recepción de pagos
  * Gestión de claves y usuarios
  * Visualización de logs y trazabilidad

### 5. Infraestructura de despliegue

* Opciones:

  * Docker Compose para despliegue local o testing
  * Terraform + Ansible para AWS o nube privada
  * Soporte posterior para Kubernetes

---

## 🧠 Capa 2: Servicios avanzados sobre la base

Una vez desplegado lo anterior, se pueden añadir módulos como:

* **LNURL-auth** para login sin contraseña
* **Webhook engine** para flujos automatizados (pagos → tareas)
* **Contabilidad BTC** con trazabilidad por proyecto/usuario
* **Gestor de identidades** (por clave pública)
* **Firmas remotas y BitVM (experimental)**
* **Microservicios empresariales** que exponen APIs y se pagan en sats

---

## 📁 Estructura del proyecto (ejemplo)

```
bitcoinstack/
├── api/                   # Backend REST
│   ├── routes/
│   ├── services/          # Funciones Bitcoin y LN
│   └── config/
├── frontend/              # Panel web
│   ├── components/
│   └── views/
├── infra/                 # Docker, Terraform, Ansible
├── docs/                  # Documentación técnica
└── scripts/               # Despliegue inicial, generación de wallets, etc.
```

