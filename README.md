<p align="center">
    <a href="https://github.com/magenta-mause/cosy">
        <picture>
          <img src="https://raw.githubusercontent.com/Magenta-Mause/Cosy-Templates/refs/heads/main/assets/logo.gif" width="400"  alt="Cosy"/>
        </picture>
    </a>
</p>

# Game Server Template Collection

A collection of validated Docker-based game server templates for easy deployment.

## Quickstart

1. Browse templates in [templates/](templates/)
2. Use template directly inside your [Cosy-Instance](https://github.com/Magenta-Mause/Cosy)
3. Fill variables (version, memory, etc.)

**Example**: Minecraft Fabric

```
templates/minecraft/fabric.yaml
``` 

## Template Format

Every template follows this structure:

```yaml
name: Minecraft Fabric
description: Minecraft Fabric Server with default fabric installation
variables:
  - name: Minecraft Version
    type: string
    regex: \d\.\d+\.\d+
    placeholder: version
    example: '1.21.5'
game_id: minecraft          # slug from games/minecraft.yaml
docker_image_name: itzg/minecraft-server
docker_image_tag: latest
environment_variables:
  VERSION: '{{version}}'
  EULA: 'true'
port_mapping:
  '25565/tcp': 25565
file_mounts:
  - /data                   # cosy-managed persistent volume
resource_limit:
  memory: 4GiB
  cpu: 2
```

**Full schema**: [schema/template.schema.json](schema/template.schema.json)

## Games directory

Every template's `game_id` references a slug — the filename (without `.yaml`) of an entry under [`games/`](games/). Each game file carries the display name and artwork URLs used in the Cosy UI:

```yaml
# games/minecraft.yaml
name: Minecraft
logo_url: https://cdn2.steamgriddb.com/logo/...
hero_url: https://cdn2.steamgriddb.com/hero/...
external_game_id: 38365    # legacy SteamGridDB id; omit for new games
```

When adding a template for a game that isn't listed yet, add a matching `games/{slug}.yaml` in the same PR.

## Advanced fields

Templates may also include:

- **`annotations`** — Docker container labels applied at launch (all users). Values may contain `{{var}}` placeholders.
- **`host_mounts`** — direct host-path bind mounts (`host_path → container_path`, optional `read_only`). Enforced admin-only at runtime.

```yaml
annotations:
  traefik.enable: 'true'
host_mounts:
  - host_path: /var/run/docker.sock
    container_path: /var/run/docker.sock
    read_only: true
```

## Contributing

- Add new templates: [CONTRIBUTING.md](CONTRIBUTING.md)
- Request
  games: [New template issue](https://github.com/Magenta-Mause/Cosy-Templates/issues/new?template=01-template-request.yaml)
- Report
  bugs: [Bug report issue](https://github.com/Magenta-Mause/Cosy-Templates/issues/new?template=02-bug-report.yaml)

## Validation

All templates pass CI validation:

- YAML syntax
- Schema compliance
- Port ranges
- Docker image format

CI runs on every PR: `.github/workflows/validate-templates.yml`

## License

MIT - see [LICENSE](LICENSE)

***

⭐ Found a bug? [[Report it →]](https://github.com/Magenta-Mause/Cosy-Templates/issues/new?template=02-bug-report.yaml)
🚀 Want a new
game? [[Request it →]](https://github.com/Magenta-Mause/Cosy-Templates/issues/new?template=01-template-request.yaml)

***


