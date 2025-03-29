# Templates for proxmox

TODO: gjør det sikrere

Før vi kjører i gang med opentofu så må vi ha noen templates i Proxmox

For å gjøre det enkelt så lager vi tre templates med cloud-init, så det ligner på ting som ville vært i sky. Mye mulig jeg tar helt feil her, men sånn er det.

Jeg har prøvd å finne gode måter å automatisere dette på, med packer, ansible eller bare python+proxmox apiet. Ansible ser ut som kunne godt, men det er mye koding for noe som er enklere med litt bash som root i Proxmox. Så automatisering er TODO her, mulig med hjelp fra [denne bloggen](https://homelabing.fr/how-to-automate-proxmox-ve-using-ansible/).

Jeg har satt opp tre templates

- Fedora
- Ubuntu
- Rocky Linux

## OPNSense

For mye jobb å sette opp dette med automatisk templating, så da er det en todo å automatisere denne.

## Fedora

```console

```

## Ubuntu

Her har jeg bare endret apalards script ([lenke til blogpost](https://www.apalrd.net/posts/2023/pve_cloud/))

```console
$ qm create 9000 --name vyos2 --memory 2048 --net0 virtio,bridge=vmbr0
$ qm importdisk 9000 /root/tmp/vyos-2025.03.23-0020-rolling-generic-amd64.qcow2 pve-zfs
$ qm set 9000 --virtio0 pve-zfs:vm-9000-disk-0
$ qm set 9000 --boot order=virtio0
```

Så setter vi opp cloud-init etter det Proxmox mener er rett ([lenke til docs](https://pve.proxmox.com/wiki/Cloud-Init_Support))

```console
$ qm set 9000 --ide2 local-lvm:cloudinit
$ qm set 9000 --boot order=virtio0
$ qm set 9000 --serial0 socket --vga serial0
```

Og så helt til slutt lage et template

```console
$ qm template 9000
```

# Notater om sikkerhet

Ja, jeg har delt interne ip addresser, og nei jeg tenker det er et lite problem når det er 192.168.0.0/16 addresser. Hvis sikkerheten i ditt indre nettverk er avhengig av, eller veldig mye bedre, dersom du skjuler ip addressene dine....
