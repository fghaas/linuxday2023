<!-- .slide: data-timing="1" --> 
# Fragen <!-- .element class="hidden" -->

* * *


<!-- .slide: data-timing="1" --> 
## Monoblock <!-- .element class="hidden" -->
Warum eine Monoblock-Wärmepumpe?

Sind die nicht laut und ineffizient?

<!-- Note -->


<!-- .slide: data-timing="1" --> 
## Radiatoren <!-- .element class="hidden" -->

Was habt ihr mit den Radiatoren gemacht?


<!-- .slide: data-timing="1" --> 
## Kühlung <!-- .element class="hidden" -->

Wärmepumpenheizung als Kühlung?

Wie funktioniert das?


<!-- .slide: data-timing="1" --> 
## Förderungen <!-- .element class="hidden" -->

Was ist mit Genehmigungen, Anzeigen, Förderungen?


<!-- .slide: data-timing="1" -->
## Home Assistant <!-- .element class="hidden" -->

Wie betreibst du Home Assistant?

* Raspberry Pi 4 mit Ubuntu Jammy <!-- .element class="fragment fade-in-then-semi-out" -->
* Rootless Podman mit docker-compose <!-- .element class="fragment fade-in-then-semi-out" -->
* loginctl --enable-linger homeassistant <!-- .element class="fragment fade-in-then-semi-out" -->
* systemctl --user start docker-compose <!-- .element class="fragment fade-in-then-semi-out" -->


<!-- .slide: data-timing="1" -->
## Home Assistant systemd unit <!-- .element class="hidden" -->

```yaml
[Unit]
Description=Podman via docker-compose
Wants=network-online.target
After=network-online.target
RequiresMountsFor=%t/containers

[Service]
Environment=PODMAN_SYSTEMD_UNIT=%n
Environment=DOCKER_HOST=unix:///%t/podman/podman.sock
Restart=on-failure
RemainAfterExit=true
TimeoutStartSec=60
TimeoutStopSec=60
ExecStart=/usr/bin/docker-compose up -d --remove-orphans
ExecStop=/usr/bin/docker-compose stop
Type=oneshot
WorkingDirectory=%h

[Install]
WantedBy=default.target
```
