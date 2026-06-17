# SIU-2-INFRA

Infra del stack SIU (frontend + api + mysql) detras de Traefik.

Cada entorno es una carpeta autocontenida con su propio `docker-compose.yml` y su
`.env`. No hay overrides ni `-f`: se entra a la carpeta y se levanta.

```
prod/   -> cd prod && docker compose up -d
dev/    -> cd dev  && docker compose up -d   (monta el codigo del host para hot-reload)
```

- Lo **estructural** (nombres de contenedor, hosts, dockerfile, restart, red) esta
  explicito en cada `docker-compose.yml`.
- El `.env` de cada carpeta solo lleva **config/secretos** que se inyectan en los
  contenedores. Compose lo levanta solo, sin `--env-file`.
- Para empezar: `cp .env.example .env` dentro de la carpeta y completar. El `.env`
  no se versiona.

Dev y prod conviven en la misma maquina: son proyectos Docker distintos (`siu-dev`
y `siu`), cada uno con su propia MySQL, y comparten solo la red externa de Traefik
(`net-nammu`).
