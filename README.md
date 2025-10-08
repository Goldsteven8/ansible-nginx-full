# Ansible - NGINX Deployment (Tasks 2–8)

Tento projekt ukazuje použití **Ansible** pro automatizovanou konfiguraci a nasazení webového serveru **NGINX** a splňuje úkoly 2 až 8.

---

## Struktura projektu (Úkol 2)
Projekt má strukturu podle best practices:

inventory/ # Inventory soubory s definicí hostů
group_vars/ # Proměnné pro skupiny hostů
roles/nginx/ # Role pro instalaci a konfiguraci NGINX
├─ tasks/ # Hlavní úkoly pro NGINX
├─ handlers/ # Handlery, např. restart NGINX
└─ templates/ # Šablony (index.html.j2, nginx_site.j2)
playbooks/ # Playbooky pro úkoly 4–8
site.yml # Hlavní playbook pro nasazení NGINX
README.md # Tento soubor

**Poznámky:**
- Playbooky jsou **idempotentní** – opakované spuštění nezpůsobí nežádoucí změny.
- Vše je dokumentováno v README.md.

---

## Proměnné (group_vars/all.yml)

```yaml
ansible_python_interpreter: /usr/bin/python3
web_user: webappi
web_root: /opt/static-sites
nginx_site_name: static-site
Úkol 3 – Nasazení služby

Instalace a konfigurace NGINX

Webové soubory budou umístěny v /opt/static-sites

Generování jednoduchého index.html pomocí Ansible šablony

Web dostupný na portu 80

NGINX běží pod uživatelem webappi

Výchozí konfigurace NGINX je nahrazena vlastní šablonou

Úkol 4 – Firewall (UFW)

Povolen port 22 a 80

Blokování ostatních příchozích spojení

Firewall aktivní

Úkol 5 – Uživatel a oprávnění

Vytvoření dedikovaného uživatele wwwebapp

Webové soubory a procesy běží pod tímto uživatelem

Úkol 6 – Zabezpečení SSH

Zakázáno přihlášení pro root (PermitRootLogin no)

Povolené přihlášení pouze přes SSH klíč (PasswordAuthentication no)

Úkol 7 – Aktualizace a ochrana

Automatické bezpečnostní aktualizace (unattended-upgrades)

Instalace a aktivace Fail2Ban

Ochrana proti brute-force útokům

Úkol 8 – Validace funkčnosti

Test HTTP odpovědi NGINX pomocí Ansible uri modulu

Kontrola, že obsah webu odpovídá očekávané hodnotě

Výsledek testu je hlášen jako úspěch nebo selhání

Spuštění playbooků
# Hlavní playbook pro NGINX
ansible-playbook -i inventory/hosts.ini site.yml

# Úkoly 4–8
ansible-playbook -i inventory/hosts.ini playbooks/firewall.yml
ansible-playbook -i inventory/hosts.ini playbooks/users.yml
ansible-playbook -i inventory/hosts.ini playbooks/ssh.yml
ansible-playbook -i inventory/hosts.ini playbooks/security.yml
ansible-playbook -i inventory/hosts.ini playbooks/validate_web.yml

Poznámky
Playbooky jsou idempotentní – opakované spuštění nezpůsobí nežádoucí změny.

Webové soubory se nacházejí v /opt/static-sites.

NGINX běží pod uživatelem wwwebapp.

Šablony jsou v roles/nginx/templates a role obsahuje i handlers pro restart služby.

Celý projekt je připraven pro snadné nasazení a rozšíření.

Struktura playbooků
playbooks/
├─ firewall.yml       # Úkol 4
├─ users.yml          # Úkol 5
├─ ssh.yml            # Úkol 6
├─ security.yml       # Úkol 7
└─ validate_web.yml   # Úkol 8

Struktura role NGINX
roles/nginx/
├─ tasks/
│  └─ main.yml        # Instalace a konfigurace NGINX
├─ handlers/
│  └─ main.yml        # Restart NGINX
└─ templates/
   ├─ index.html.j2
   └─ nginx_site.j2

