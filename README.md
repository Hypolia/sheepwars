# Hypolia SheepWars

Mini-jeu SheepWars : arène, moutons spéciaux, HUD, heartbeat orchestrateur, retour au hub.

Images publiées :

- `ghcr.io/hypolia/sheepwars` : le plugin, lancé en sidecar à côté du serveur.
- `ghcr.io/hypolia/sheepwars-server` : rspigot avec le template de `server/`.

Dépend de [`hypolia/sdk`](https://github.com/hypolia/sdk), cloné dans `../sdk` et figé par `sdk.ref`, et de rspigot, attendu dans `/opt/minecraft/dev/rspigot` et figé par `rspigot.ref`.

## Lancer en local

Serveur rspigot (`:25567`, gRPC `:25581`) :

```bash
unzip -o server/world.zip -d server
/opt/minecraft/dev/rspigot/target/release/rspigot --world-dir ./server
```

Plugin :

```bash
RSPIGOT_URL=http://127.0.0.1:25581 RSPIGOT_PLUGIN_NAME=hypolia-sheepwars cargo run --release -p hypolia-sheepwars
```

Le proxy Velocity se lance depuis [`hypolia/platform`](https://github.com/hypolia/platform).

## Construire les images

```bash
docker buildx bake
```

Optionnel : `ORCHESTRATOR_URL=http://127.0.0.1:8080` et `SERVER_ID=sheepwars-1` si l'orchestrateur local tourne. Sinon le plugin enchaîne les manches sur place.

En jeu : `/sheepwars join|leave|hub`, et pour les admins `/sheepwars forcestart|stop`.

Contrat du sidecar et variables d'environnement : [`docs/PLUGIN_CONTRACT.md`](./docs/PLUGIN_CONTRACT.md).
