# Contributing to Template Collection

Thanks for your interest in adding game server templates! Follow these steps to make your PR smooth.

## Before starting

1. **Read the template structure**: All templates follow `templates/{game-name}/{template-description}.yaml` with fields defined in [schema/template.schema.json](schema/template.schema.json).
2. **Check for duplicates**: Search the repo for your game first.
3. **Validate locally**: Use a YAML validator against the schema (VS Code works great).

## Adding a new template

1. **Create the file**: `templates/{game-name}/{template-description}.yaml` (lowercase, dashes).

```
templates/minecraft/fabric.yaml
templates/counter-strike-2/competitive.yaml 
```

2. **Fill the required fields**:
- `name`: Human-readable (e.g. "Minecraft Fabric")
- `description`: What it provides
- `game_id`: Get it from https://cosy-game-api.jannekeipert.de/games?query={search-string}
- `docker_image_name` + `docker_image_tag`: Working Docker image
- `port_mapping`: Standard ports for the game
3. **Add variables**: Use `variables[]` for user inputs (version, memory, etc.).
4. **Test the template**: Deploy it on a test server to verify it starts correctly.

## Validation

Templates must pass the schema. Install a validator:

```bash
# npm
npm install -g validate-yaml
validate-yaml --schema=schema/template.schema.json templates/{game-name}/{template-description}.yaml
```

# Or use VS Code with yaml-language-server

CI will also validate all `templates/*/*.yaml` files automatically.

## Opening a pull request

- Use the auto-filled PR template.
- Complete the checklist.
- Include testing steps showing the server starts and works.

## Common issues

| Issue | Solution |
|-------|----------|
| Schema fails on `docker_image_name` | Use lowercase, valid Docker format: `itzg/minecraft-server` |
| `port_mapping` invalid | Use `"25565": 25565` format, ports 1–65535 |
| `file_downloads` URLs | Use `{{version}}` placeholders, test URLs |
| Paths must start with `/` | e.g. `/data/mods`, not `data/mods` |

## Questions?

Open an [issue](https://github.com/magenta-mause/cosy-templates/issues/new?template=template-request.yaml) first if unsure.
