# 🧠 Proyecto: Raspberry Pi DNS Sinkhole con dnsmasq

Este proyecto convierte una Raspberry Pi en un **servidor DNS personalizado** con capacidad de bloqueo de publicidad, rastreadores y dominios no deseados, usando `dnsmasq`. Es una solución liviana, eficiente y educativa para comprender cómo funciona DNS a nivel de red.

---

## 🎯 Objetivo

* Entender el funcionamiento de un servidor DNS
* Montar un DNS personalizado y funcional
* Integrar una lista negra de dominios para bloqueo de publicidad
* Usar una Raspberry Pi como dispositivo de red 24/7

---

## 🧱 Infraestructura

| Elemento            | Detalle                             |
| ------------------- | ----------------------------------- |
| Dispositivo         | Raspberry Pi (con cooler, 24/7)     |
| OS                  | Debian/Raspbian                     |
| Software DNS        | `dnsmasq`                           |
| Interfaz activa     | `127.0.0.1`, `192.168.1.X` (IP LAN) |
| Forwarders externos | `8.8.8.8`, `1.1.1.1`                |

---

## 🧰 Instalación

```bash
sudo apt update
sudo apt install dnsmasq dnsutils -y
```

---

## 🛠️ Configuración básica

### Hacer backup del archivo original:

```bash
sudo cp /etc/dnsmasq.conf /etc/dnsmasq.conf.original
```

### Editar configuración principal:

```bash
sudo nano /etc/dnsmasq.conf
```

### Contenido base:

```ini
domain-needed
bogus-priv
no-resolv
server=8.8.8.8
server=1.1.1.1
listen-address=127.0.0.1,192.168.1.78
cache-size=1000
log-queries
log-facility=/var/log/dnsmasq.log
```

📌 Reemplazar `192.168.1.78` por la IP real de tu Raspberry en la red LAN.

---

## 🧪 Verificación de funcionamiento

### Ver estado del servicio:

```bash
sudo systemctl status dnsmasq
```

### Consultar dominio:

```bash
dig @127.0.0.1 google.com
```

Debe devolver una IP válida (no error).

---

## 🔒 Integración de lista negra de dominios (bloqueo de publicidad)

### 1. Descargar lista tipo Pi-hole:

```bash
wget https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts -O adblock_hosts.txt
```

### 2. Convertirla al formato dnsmasq:

```bash
grep "^0.0.0.0" adblock_hosts.txt | awk '{print "address=/" $2 "/127.0.0.1"}' | sudo tee /etc/dnsmasq.d/adblock.conf > /dev/null
```

### 3. Reiniciar servicio:

```bash
sudo systemctl restart dnsmasq
```

### 4. Probar bloqueo:

```bash
dig @127.0.0.1 ads.google.com
```

Debe devolver:

```txt
;; ANSWER SECTION:
ads.google.com. 0 IN A 127.0.0.1
```

---

## 💡 Explicación técnica

* `dnsmasq` actúa como **servidor DNS local**
* Escucha en `127.0.0.1` (localhost) y en `192.168.1.78` (red LAN)
* Si no tiene la respuesta, la busca en `8.8.8.8` o `1.1.1.1`
* Si el dominio está en su lista negra (`/etc/dnsmasq.d/adblock.conf`), responde con `127.0.0.1`, bloqueando la solicitud

---

## 🌐 Aplicación en red real

Podés apuntar cualquier dispositivo de tu red (PC, celular, router) a la Raspberry como servidor DNS:

**Ejemplo en Linux:**

```bash
echo "nameserver 192.168.1.78" | sudo tee /etc/resolv.conf
```

**Ejemplo en Windows:** configurar DNS manual en IPv4 → `192.168.1.78`

---

## 📊 Posibilidades de expansión

* Agregar scripts para actualizar la lista negra automáticamente
* Agregar DHCP al `dnsmasq` y hacer que actúe como servidor central
* Integrar Suricata o Pi-hole para estadísticas y detección
* Redirigir ciertos dominios a servicios propios (DNS hijack defensivo)
* Complementar con VPN (próximo proyecto)

---

## ✅ Resultado final

* DNS local funcional en Raspberry
* Respuestas con caché y resolución externa
* Sistema de bloqueo activo por dominios
* Usable desde otros dispositivos de la red
* Control total sobre el comportamiento DNS

---

## 🧠 Conclusión

Este proyecto demuestra comprensión real de:

* Cómo funciona DNS
* Cómo interceptar tráfico y personalizar respuestas
* Cómo montar un servicio de red productivo en una Raspberry Pi
* Cómo trabajar con listas externas y automatizar su integración

> Proyecto válido como parte de un portfolio técnico SOC / Blue Team / Networking
