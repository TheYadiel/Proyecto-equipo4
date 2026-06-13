# Producto 1 - Red Empresarial (Equipo 4)

Materia: Conmutación y Enrutamiento (TI-203), ITLA
Plataforma: PNETLab

## Descripción

Este proyecto consiste en el diseño e implementación de una red empresarial de mediana escala para una organización con varios departamentos (académico, administrativo, financiero y de datacenter). La red está segmentada lógicamente mediante VLANs para separar el tráfico de cada área, y cuenta con alta disponibilidad de gateway mediante HSRP, de forma que si un router falla el otro toma el control sin interrumpir el servicio. A nivel de capa 2 se implementa EtherChannel y STP para tener enlaces redundantes y evitar bucles. El enrutamiento entre las distintas redes se realiza mediante OSPFv2, configurado inicialmente en área única pero pensado para poder escalar a un esquema multiárea. El proyecto se desarrolla y prueba en PNETLab, e incluye el plan de direccionamiento completo en IPv4 e IPv6 para cada VLAN.

## Direccionamiento asignado

IPv4: 172.22.0.0/15
IPv6: 2001:25:22::/48

## Plan IPv4 (VLSM)

**R1-Core**

| VLAN | Hosts requeridos | Hosts usables | Prefijo | Red | Gateway | Broadcast |
|---|---|---|---|---|---|---|
| Estudiantes | 1500 | 2046 | /21 | 172.22.0.0/21 | 172.22.0.1 | 172.22.7.255 |
| Docentes | 164 | 254 | /24 | 172.22.8.0/24 | 172.22.8.1 | 172.22.8.255 |
| Gestión | 29 | 30 | /27 | 172.22.9.0/27 | 172.22.9.1 | 172.22.9.31 |
| Voz | 16 | 30 | /27 | 172.22.9.32/27 | 172.22.9.33 | 172.22.9.63 |
| Blackhull | 10 | 14 | /28 | 172.22.9.64/28 | 172.22.9.65 | 172.22.9.79 |

**R2**

| Red | Hosts requeridos | Hosts usables | Prefijo | Red | Gateway | Broadcast |
|---|---|---|---|---|---|---|
| Académicos | 80 | 126 | /25 | 172.22.10.0/25 | 172.22.10.1 | 172.22.10.127 |
| Finanzas | 64 | 126 | /25 | 172.22.10.128/25 | 172.22.10.129 | 172.22.10.255 |
| Datacenter | 44 | 62 | /26 | 172.22.11.0/26 | 172.22.11.1 | 172.22.11.63 |
| Blackhull | 10 | 14 | /28 | 172.22.11.64/28 | 172.22.11.65 | 172.22.11.79 |
| P2P | 2 | 2 | /30 | 172.22.11.80/30 | 172.22.11.81 | 172.22.11.83 |

## Plan IPv6

Prefijos /64 asignados desde 2001:25:22::/48, en el mismo orden que IPv4 (la red más grande primero).

| Red | Prefijo IPv6 | Red | Gateway |
|---|---|---|---|
| Estudiantes | /64 | 2001:25:22:1::/64 | 2001:25:22:1::1 |
| Docentes | /64 | 2001:25:22:2::/64 | 2001:25:22:2::1 |
| Gestión | /64 | 2001:25:22:3::/64 | 2001:25:22:3::1 |
| Voz | /64 | 2001:25:22:4::/64 | 2001:25:22:4::1 |
| Blackhull R1 | /64 | 2001:25:22:5::/64 | 2001:25:22:5::1 |
| Académicos | /64 | 2001:25:22:6::/64 | 2001:25:22:6::1 |
| Finanzas | /64 | 2001:25:22:7::/64 | 2001:25:22:7::1 |
| Datacenter | /64 | 2001:25:22:8::/64 | 2001:25:22:8::1 |
| Blackhull R2 | /64 | 2001:25:22:9::/64 | 2001:25:22:9::1 |
| P2P | /64 | 2001:25:22:a::/64 | 2001:25:22:a::1 |

## Tecnologías implementadas

- VLANs y VTP para segmentación y propagación entre switches
- EtherChannel y STP para redundancia en capa 2
- HSRP para alta disponibilidad de gateway
- OSPFv2 para enrutamiento dinámico entre routers

## Estructura del repositorio

configs/      configuraciones de cada dispositivo
topologia/    diagrama y mapa de puertos
pruebas/      scripts y resultados de pruebas
README.md     este documento

## Estado del proyecto

Sprint 1: diseño de direccionamiento, topología y VLANs - completado
Sprint 2: VLANs, VTP, STP, EtherChannel, HSRP - en progreso
Sprint 3: OSPFv2, pruebas y documentación final - pendiente
