# Templates for proxmox

TODO: gjør det sikrere

Før vi kjører i gang med opentofu så må vi ha noen templates i Proxmox

For å gjøre det enkelt så lager vi tre templates med cloud-init, så det ligner på ting som ville vært i sky. Mye mulig jeg tar helt feil her, men sånn er det.

Jeg har prøvd å finne gode måter å automatisere dette på, med packer, ansible eller bare python+proxmox apiet. Ansible ser ut som kunne godt, men det er mye koding for noe som er enklere med litt bash som root i Proxmox. Så automatisering er TODO her, mulig med hjelp fra [denne bloggen](https://homelabing.fr/how-to-automate-proxmox-ve-using-ansible/) eller bare [den offisielle community utvidelsen](https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_module.html)

Jeg har satt opp tre templates

- Fedora
- Ubuntu
- Rocky Linux

## OPNSense

For mye jobb å sette opp dette med automatisk templating, så da er det en todo å automatisere denne.

## Fedora CoreOS

Her var det faktisk et supert verktøy som noen flinke folk i frankrike har laget ([lenke](https://wiki.geco-it.net/public:pve_fcos))

## Talos Linux

Og her er det et fint oppsett fra Olav S. Thoresen ([Talos cluster on Proxmox with Terraform](https://olav.ninja/talos-cluster-on-proxmox-with-terraform))

## Andre

Her har jeg bare endret apalards script ([lenke til blogpost](https://www.apalrd.net/posts/2023/pve_cloud/))

# Notater om sikkerhet

Ja, jeg har delt interne ip addresser, og nei jeg tenker det er et lite problem når det er 192.168.0.0/16 addresser. Hvis sikkerheten i ditt indre nettverk er avhengig av, eller veldig mye bedre, dersom du skjuler ip addressene dine....
