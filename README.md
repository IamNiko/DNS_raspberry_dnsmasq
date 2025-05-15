## 🔐 Proyecto: Raspberry Pi DNS Sinkhole con dnsmasq

Este proyecto convierte una Raspberry Pi en un servidor DNS personalizado con capacidad de bloquear publicidad, rastreadores y dominios maliciosos. Está configurado manualmente usando `dnsmasq` y aprovecha listas negras públicas compatibles con Pi-hole. Representa un ejercicio técnico sólido en redes y seguridad defensiva.

### 🧰 Tecnologías utilizadas:
- Raspberry Pi (con refrigeración 24/7)
- dnsmasq
- Linux CLI
- Listas negras tipo Pi-hole (StevenBlack)

### 🧪 Funcionalidades principales:
- Resolución de dominios con caché
- Reenvío inteligente a DNS públicos (Google, Cloudflare)
- Bloqueo de dominios a través de lista personalizada
- Redirección de tráfico no deseado a `127.0.0.1`
- Aplicable a toda la red local

👉 Ver el proyecto completo en [`Dns Sinkhole Raspberry.md`](./Dns%20Sinkhole%20Raspberry.md)

## 🔐 Project: Raspberry Pi DNS Sinkhole using dnsmasq

This project turns a Raspberry Pi into a custom DNS server capable of blocking ads, trackers, and malicious domains. It is manually configured using `dnsmasq` and leverages public blacklist sources compatible with Pi-hole. It demonstrates a strong technical foundation in networking and blue team defense.

### 🧰 Technologies used:
- Raspberry Pi (24/7 with cooling)
- dnsmasq
- Linux CLI
- Pi-hole-style blacklist (StevenBlack)

### 🧪 Key features:
- Domain name resolution with cache
- Smart forwarding to public DNS (Google, Cloudflare)
- Domain blocking via custom list
- Redirects unwanted domains to `127.0.0.1`
- Usable across the entire local network

👉 Full project documentation in [`Dns Sinkhole Raspberry.md`](./Dns%20Sinkhole%20Raspberry.md)
