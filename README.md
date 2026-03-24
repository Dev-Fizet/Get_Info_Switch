# 🕵️‍♂️ L2NeighborFinder - Monitor de dispositivos vecinos a nivel 2

![Network Capture](https://img.shields.io/badge/Tool-NetworkCapture-blue) ![C#](https://img.shields.io/badge/Language-C%23-green) ![SharpPcap](https://img.shields.io/badge/Library-SharpPcap-orange) ![PacketDotNet](https://img.shields.io/badge/Library-PacketDotNet-red)

---

## 📜 Descripción

**L2NeighborFinder** es una herramienta de monitoreo de red a nivel 2 (capa de enlace), que detecta dispositivos vecinos mediante la captura pasiva de paquetes Ethernet, incluyendo tráfico ARP, IPv4, IPv6, CDP y LLDP.

Esta utilidad permite:

- 📡 Detectar y registrar direcciones MAC visibles en la red.
- 🔍 Identificar fabricantes mediante mapeo OUI.
- 🗂 Registrar los vecinos y sus propiedades (IP, VLAN, sistema operativo, etc.).
- 🛑 Monitorizar tráfico LLDP y CDP para identificar detalles extendidos de dispositivos Cisco y compatibles.
- 📝 Guardar actividad en logs CSV para posteriores análisis.

---

## 🚀 Funcionalidades principales

- Escaneo y monitorización de la interfaz de red elegida.
- Filtrado de paquetes relevantes (ARP, IP, IP6, LLDP, CDP).
- Mapeo dinámico de MACs y limpieza automática de entradas inactivas.
- Soporte de logs diarios formateados en CSV.
- Visualización en consola con detalle de cada dispositivo detectado.
- Visualización dinámica de la tabla MAC actual.
- Soporte de carga de base OUI para mostrar fabricantes.

---

## 🛠️ Requisitos

- Sistema operativo Windows (que soporte SharpPcap/WinPcap/Npcap).
- [Npcap](https://npcap.com/) instalado (modo promiscuo compatible).
- [.NET 6+ SDK](https://dotnet.microsoft.com/download) o compatible.
- Permisos de administrador para abrir interfaces en modo promiscuo.
- Dependencias NuGet:
  - SharpPcap
  - PacketDotNet

---

## 📋 Instalación

1. Clona el repositorio:

```bash
git clone https://github.com/tuusuario/L2NeighborFinder.git
cd L2NeighborFinder
```

2. Restaura paquetes NuGet y compila el proyecto:

```bash
dotnet restore
dotnet build
```

3. Asegúrate de tener un archivo `oui.txt` o `oui.csv` con las asignaciones OUI de fabricantes (opcional para mostrar nombres de vendor):

- Puedes descargar las listas oficiales desde IEEE o usar algun repositorio público.
- Colócalo en el mismo directorio del ejecutable.

---

## ⚙️ Uso

1. Ejecuta el programa como **Administrador** para capturar en modo promiscuo.

```bash
dotnet run --project L2NeighborFinder.csproj
```

2. Selecciona la interfaz de red Ethernet que desees monitorizar (por índice).

3. El programa comenzará a capturar y mostrar en tiempo real:

- Detalles de MACs detectadas.
- Información LLDP y CDP de dispositivos vecinos.
- Logs se almacenan en `logs/scan_log_YYYY-MM-DD.csv`.

4. Atajos en consola durante la ejecución:

| Tecla | Acción                           |
|-------|---------------------------------|
| `Q`   | Detener captura y salir          |
| `T`   | Mostrar tabla MAC monitorizada   |

---

## 📂 Archivos de logs

Los logs se guardan en la carpeta `logs/` con formato CSV:

| timestamp           | protocol | local_nic | local_mac | local_ipv4 | device_or_system | port_id | native_vlan_or_pvid | mgmt_ips | voice_vlan | vtp_domain | duplex | platform | software | capabilities | poe |
|---------------------|----------|-----------|-----------|------------|------------------|---------|---------------------|----------|------------|------------|--------|----------|----------|--------------|-----|

Ejemplo:

2024-04-26 12:30:15.123,MAC,eth0,00:11:22:33:44:55,192.168.1.10,"Cisco Systems (00:1b:54)",-,100,192.168.1.100,-,-,-,-,0x0800,-

---

## 🔧 Personalización

- `MAC_RELOG_SECONDS` — Frecuencia en segundos para re-log de misma MAC si sigue activa (default: 60s).
- `MAC_STALE_MINUTES` — Tiempo en minutos para considerar una MAC inactiva y eliminarla de la tabla (default: 30 min).

---

## ⚠️ Consejos y advertencias

- Ejecutar como administrador es obligatorio para abrir interfaces en modo promiscuo.
- Para obtener info de fabricantes, carga una base OUI actualizada (`oui.txt` o `oui.csv`).
- Se recomienda usar Npcap en modo compatible con WinPcap para Windows.
- Capturar tráfico en redes públicas o ajenas puede tener implicaciones legales. Use con responsabilidad.

---

## 📚 Referencias

- [SharpPcap GitHub](https://github.com/chmorgan/sharppcap)
- [PacketDotNet GitHub](https://github.com/chmorgan/packetnet)
- [IEEE OUI list](https://standards-oui.ieee.org/)
- [Npcap](https://npcap.com/)
- [Captura de paquetes y protocolos: TCP/IP Layers](https://en.wikipedia.org/wiki/OSI_model)

---

## 🧑‍💻 Contacto

Para dudas, propuestas o colaborar, abre un Issue en el repositorio o contacta con el mantenedor.

---

## 🎉 Gracias por usar L2NeighborFinder!

¡Esperamos que esta herramienta te facilite la administración y auditoría de tu red local a nivel 2! 🔍🌐
