# Ansible: Automatizované nasazení NGINX pro statický web

Tento projekt je ukázka **Infrastructure as Code**: pomocí **Ansible** automaticky připraví Ubuntu server pro hostování statického webu na **NGINX**.  
Cílem je mít nasazení, které je **opakovatelné (idempotentní)**, snadno rozšiřitelné a obsahuje i základní bezpečnostní nastavení serveru.

---

## Co projekt dělá

Po spuštění playbooku projekt na cílovém serveru:

- nainstaluje a nakonfiguruje **NGINX**
- nasadí statický web do **`/opt/static-sites`** (vygenerovaný ze šablony)
- zpřístupní web na **portu 80 (HTTP)**
- nastaví **UFW firewall** (povolí pouze **22/SSH** a **80/HTTP**)
- vytvoří dedikovaného uživatele pro web a nastaví oprávnění k souborům
- provede **SSH hardening** (zakáže root login, povolí přihlášení jen přes SSH klíč)
- zapne **automatické bezpečnostní aktualizace** (`unattended-upgrades`)
- nainstaluje a aktivuje **Fail2Ban** (ochrana proti brute-force útokům)
- ověří funkčnost pomocí HTTP kontroly (validace odpovědi a očekávaného obsahu)

---

## Technologie

- Ansible
- NGINX
- Ubuntu Linux
- UFW, Fail2Ban, unattended-upgrades
- Jinja2 šablony

---

## Struktura repozitáře

inventory/ # definice hostů
group_vars/ # konfigurace (proměnné)
roles/nginx/ # role: instalace + konfigurace NGINX + šablony
playbooks/ # doplňkové playbooky (firewall, ssh, security, validace)
site.yml # hlavní playbook

## Spuštění

```bash
ansible-playbook -i inventory/hosts.ini site.yml





