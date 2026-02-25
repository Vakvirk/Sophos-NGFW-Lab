# NGFW Lab – Dokumentacja techniczna

## 1. Cel projektu
Celem projektu było zaprojektowanie i wdrożenie wirtualnego środowiska sieciowego
z wykorzystaniem zapory NGFW, umożliwiającego testowanie routingu, segmentacji sieci,
polityk bezpieczeństwa, VPN oraz mechanizmów IDS/IPS.

---

## 2. Zakres projektu
Projekt obejmuje:
- konfigurację zapory NGFW
- routing L3 między segmentami sieci
- segmentację LAN / DMZ
- reguły firewall i NAT
- wdrożenie IDS/IPS
- testy bezpieczeństwa i weryfikację działania

---

## 3. Środowisko

### 3.1 Sprzęt
- Laptop: Ryzen 7, 16 GB RAM

### 3.2 Oprogramowanie
- Hypervisor: VMware Workstation Pro
- NGFW: Sophos Firewall (VM)
- Systemy:
  - Linux (LAN)
  - Windows (LAN)
  - Linux Web Server (DMZ)

## 4. Topologia sieci

### 4.1 Adresacja IP

| Segment | Zakres |
|-------|-------|
| WAN | DHCP |
| LAN | 192.168.10.0/24 |
| DMZ | 192.168.20.0/24 |

---

## 5. Konfiguracja

### 5.1 Interfejsy NGFW
- WAN – DHCP
- LAN – 192.168.10.1/24
- DMZ – 192.168.20.1/24

### 5.2 Routing
- NGFW pełni rolę routera dla wszystkich segmentów
- Domyślna trasa skierowana na interfejs WAN

---

## 6. Polityki bezpieczeństwa

### 6.1 Reguły firewall

| Źródło | Cel | Usługa | Akcja | Opis |
|------|-----|-------|------|-----|
| LAN | Internet | Any | Allow | Dostęp użytkowników do Internetu |
| LAN | DMZ | Any | Deny | Ograniczenie lateral movement |
| Internet | DMZ | HTTP/HTTPS | Allow | Publiczny serwer WWW |

---

## 7. NAT
- Source NAT (SNAT) dla ruchu LAN → WAN
- Destination NAT (DNAT) dla publikacji serwera WWW w DMZ

---

## 8. IDS / IPS
- Włączony moduł IDS/IPS
- Monitorowanie ruchu LAN → DMZ
- Detekcja skanów portów i prób exploitacji

---

## 9. Testy i weryfikacja

### 9.1 Testy funkcjonalne
- LAN → Internet: OK
- LAN → DMZ (SSH): BLOCKED
- Internet → DMZ (HTTP): OK

### 9.2 Testy bezpieczeństwa
- Skan portów (nmap) z LAN → alert IDS
- Próba nieautoryzowanego dostępu → zablokowana

---

## 10. Napotkane problemy i rozwiązania

**Problem:** Brak dostępu do Internetu z sieci LAN  
**Przyczyna:** Brak reguły NAT  
**Rozwiązanie:** Dodanie SNAT na interfejsie WAN

---

## 11. Wnioski
Projekt pozwolił na zdobycie praktycznego doświadczenia w konfiguracji NGFW,
projektowaniu segmentacji sieci oraz analizie zdarzeń bezpieczeństwa.

---

## 12. Możliwe rozszerzenia
- VPN typu remote-access
- VLAN tagging
- Centralne logowanie (SIEM)
- Wysoka dostępność (HA)

---

## 4. Topologia sieci
