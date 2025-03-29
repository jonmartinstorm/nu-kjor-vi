# Nu kjør vi!

En liksom sikker hjemmelab stort sett satt opp med IaC

## Mål

Målet er å ha en så godt som automatisert oppsett av en hjemmelab som også er rimelig sikker. Og det med bruk av stort sett verktøy med åpen kildekode.

### Tenkt arkitektur

Dette er et forsøk på å tegne arkitekturen.

```mermaid
architecture-beta
    group dmz[DMZ]
    group indre[Indre nettverk]
    group k8s[K8S cluster] in indre

    service internett(cloud)[internett]
    service ytrebr(server)[Ytre Brannmur]
    service indrebr(server)[Indre Brannmur]

    service guac(server)[Apache Guacamole] in dmz
    service filsluse(server)[filsluse] in dmz

    service freeipa(server)[FreeIpa VM] in indre
    service filserver(server)[Harbor og Gitea] in k8s
    service keyradius(server)[KeyCloak FreeRadius VM] in indre
    service database(database)[PostGRES] in indre

    service brukerpod(disk)[BrukerPod] in k8s
    service nextcloud(disk)[NextCloud] in k8s
    service mattermost(disk)[MatterMost] in k8s

    internett:R -- L:ytrebr
    ytrebr:R -- L:guac
    ytrebr:R -- L:filsluse
    indrebr:L -- R:guac
    indrebr:L -- R:filsluse
    indrebr:B -- T:brukerpod
    brukerpod:R -- L:mattermost
    brukerpod:R -- L:nextcloud
    freeipa:R -- L:keyradius
```

### Status PT

Her er vi i dag.

```mermaid
architecture-beta
    group indre[Indre nettverk]


    service ytrebr(server)[Ytre Brannmur]
    service tester(disk)[FedoraDesktop] in indre
    service host(internet)[Host]

    host:T -- B:tester
```

## Tech støff

Hva er det som hjemmelabben skal bestå av?

### Jern

- Lenovo Thinkcentre M920q Tiny, i9, 32GB RAM, 512GB SSD, WiFi

### Programvare

Nøkkelprogrammer:

- Proxmox VE [lenke](https://www.proxmox.com/en/)
- Rocky Linux [lenke](https://rockylinux.org/no-NO)
- Ubuntu 24.04 [lenke](https://ubuntu.com/)
- Fedora 41 [lenke](https://fedoraproject.org/)
- OPNsense/pfSense [lenke](https://opnsense.org/)
- FreeIPA [lenke](https://www.freeipa.org/)
- KeyCloak [lenke](https://www.keycloak.org/)
- kubernetes [lenke](https://kubernetes.io/)
- NextCloud [lenke](https://nextcloud.com/)
- MatterMost [lenke](https://mattermost.com/)
- apache guacemole [lenke](https://guacamole.apache.org/)
- Wiki.js [lenke](https://js.wiki/)
- OpenProject [lenke](https://www.openproject.org/)
- Plane [lenek](https://plane.so/)
- ERPNext [lenke](https://frappe.io/erpnext)
- Zarf [lenke](https://zarf.dev/)
- Kasm workspaces [lenke](https://kasmweb.com/)
- Harbor [lenke](https://goharbor.io/)
- Forgejo [lenke](https://forgejo.org/)

Verktøy:

- openTofu [lenke](https://opentofu.org/)
- ansible [lenke](https://docs.ansible.com/)

## Eksterne bruksanvisninger

Ting som jeg har brukt for å lære meg de diverse programvarene.

- apalrd's adventures [on youtube](https://www.youtube.com/@apalrdsadventures/videos)
- DevOps Directive [Complete Terraform Course - From BEGINNER to PRO! (Learn Infrastructure as Code)](https://youtu.be/7xngnjfIlK4?si=ZchQDAig5tDmNIJv)
- Christian Lempa [Proxmox virtual machine _automation_ in Terraform](https://youtu.be/dvyeoDBUtsU?si=VmtJZ-79wN5DhZaa)
- Learn Linux TV [Kasm Workspaces Simplified: The Essential Guide for New Users](https://youtu.be/U5-oNbNEJYI?si=P82qzUjAKjwV8IMi)
