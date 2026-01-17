# Game Server Template Collection

A collection of validated Docker-based game server templates for easy deployment.

## Quickstart

1. Browse templates in [templates/](templates/)
2. Use your deployment platform with the YAML config
3. Fill variables (version, memory, etc.)

**Example**: Minecraft Fabric

```
templates/minecraft/fabric.yaml
```


## Available Templates

| Game      | Templates               | Docker Image          |
| :-------- | :---------------------- | :-------------------- |
| Minecraft | fabric.yaml | itzg/minecraft-server |

<!-- Auto-generate this table or add manually as templates grow -->

## Template Format

Every template follows this structure:

```yaml
name: Minecraft Fabric
description: Minecraft Fabric Server with default fabric installation
variables:
  - name: Minecraft Version
    type: string
    regex: \d\.\d+\.\d
    placeholder: version
game_id: '[steam_grid_db_game_id]' # This id comes from the https://www.steamgriddb.com/
docker_image_name: itzg/minecraft-server
docker_image_tag: latest
# ... port_mapping, environment_variables, etc.
```

**Full schema**: [schema/template.schema.json](schema/template.schema.json)

## Why www.steamgriddb.com? 

Cosy is relying on the SteamGridDb API to resolve game information as this was the best and easiest to access API.

## Contributing

- Add new templates: [CONTRIBUTING.md](CONTRIBUTING.md)
- Request games: [New template issue](https://github.com/%7Byour-org%7D/%7Brepo%7D/issues/new?template=template-request.yaml)
- Report bugs: [Bug report issue](https://github.com/%7Byour-org%7D/%7Brepo%7D/issues/new?template=bug-report.yaml)


## Validation

All templates pass CI validation:

- YAML syntax
- Schema compliance
- Port ranges
- Docker image format

CI runs on every PR: `.github/workflows/validate-templates.yml`

## Deployment Platforms

These templates work with:

## License

MIT - see [LICENSE](LICENSE)

***

⭐ Found a bug? [[Report it →]](https://github.com/magenta-mause/cosy-templates/issues/new?template=bug-report.yaml)
🚀 Want a new game? [[Request it →]](https://github.com/magenta-mause/cosy-templates/issues/new?template=template-request.yaml)

***


