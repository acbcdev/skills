# TODO

## Skills por agregar

### 1. Skill: `readme-writer`
Crear una skill para generar READMEs profesionales, inspirada en el estilo de Tania Rascia y los "100 consejos para devs".

- [ ] Definir frontmatter (name, description, model, allowed-tools)
- [ ] Incorporar reglas de estilo: claridad, ejemplos, badges, estructura progresiva
- [ ] Emular tono directo y pedagógico al estilo Tania Rascia
- [ ] Incluir secciones comunes: install, usage, API, contributing, license
- [ ] Publicar en `skills/readme-writer/SKILL.md`

### 2. `autommit`: Hacerlo más atómico

El skill actual tiene 3 estrategias (`file`, `features`, `domain`). Hacerlo más atómico implica:

- [ ] Dividir la estrategia `file` por chunk lógico en vez de archivo completo
- [ ] Revisar si el strategy `file` debe ser el default o si conviene `hunk` (cambio atómico)
- [ ] Evaluar si la granularidad actual genera commits grandes y cómo partirla
- [ ] Posible nueva estrategia: `hunk` — un commit por cambio atómico (diff hunk)
- [ ] Tests/validación de que los commits sean realmente atómicos (un solo propósito)
