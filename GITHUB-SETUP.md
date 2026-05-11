# GitHub Setup — QiHealth Marketing Plugin

Guía paso a paso para subir este plugin a GitHub privado y conectarlo a Claude Cowork como marketplace.

**Tiempo total**: ~20 minutos.

---

## Paso 1 — Crear repo en GitHub (5 min)

### Si no tienes organización GitHub

1. Ve a [github.com/organizations/new](https://github.com/organizations/new)
2. Crea organización con nombre `qihealth` (o el que prefieras)
3. Plan: **Free** está bien para repos privados
4. Una vez creada, continúa al siguiente paso

### Crear el repo privado

1. En tu organización (o cuenta personal), ve a "New repository"
2. **Repository name**: `qihealth-marketing-plugin`
3. **Description**: `Sistema de marketing agéntico para QiHealth — Plugin de Claude Cowork`
4. **Visibility**: **Private** (importante — contiene strategy interna)
5. **NO inicializar** con:
   - ❌ README (ya tenemos uno)
   - ❌ .gitignore (ya está en el folder)
   - ❌ License
6. Click **Create repository**

Vas a ver una pantalla con instrucciones para "push an existing repository from command line". Anota la URL (algo como `https://github.com/qihealth/qihealth-marketing-plugin.git`).

---

## Paso 2 — Push del plugin a GitHub (5 min)

Abre Terminal en tu Mac y navega al folder del plugin:

```bash
# Ajusta la ruta según donde descomprimiste el bundle
cd ~/Downloads/qihealth-bundle-macmini

# Verifica que el folder qihealth-marketing-plugin esté aquí
ls qihealth-marketing-plugin/

# Entra al folder del plugin
cd qihealth-marketing-plugin

# Inicializa git
git init

# Configura tu identidad (si no lo has hecho antes en esta Mac)
git config user.email "jat@qihealth.ai"
git config user.name "Jose Torres"

# Add todos los archivos
git add .

# Verifica qué se va a commitear (debería listar todas las skills, memory, scheduled-tasks)
git status

# Primer commit
git commit -m "Initial commit — qihealth-marketing v0.2.0 (51 skills + 5 scheduled tasks)"

# Cambia branch a main (estándar moderno)
git branch -M main

# Conecta con tu repo en GitHub (REEMPLAZA la URL por la tuya)
git remote add origin https://github.com/qihealth/qihealth-marketing-plugin.git

# Push inicial
git push -u origin main
```

GitHub te pedirá autenticación. Opciones:
- **HTTPS con token**: crea un Personal Access Token en github.com/settings/tokens → usa el token como password
- **SSH**: si ya tienes SSH key configurada con GitHub, mejor cambia la URL a `git@github.com:qihealth/qihealth-marketing-plugin.git`
- **GitHub CLI** (`gh`): si tienes `gh` instalado, autentica con `gh auth login` y push funciona

---

## Paso 3 — Conectar el repo a Cowork (5 min)

### En tu laptop

1. Abre **Claude Cowork Desktop**
2. Ve a **Settings** (engrane arriba a la derecha)
3. Selecciona **Plugins** (en sidebar)
4. Click **Add Marketplace** (o "Add from GitHub")
5. URL: `https://github.com/qihealth/qihealth-marketing-plugin`
6. Cowork autenticará con tu cuenta de GitHub (si no estás conectado, sigue el flow OAuth)
7. Cowork detecta el `.claude-plugin/plugin.json` y muestra el plugin disponible
8. Click **Install** sobre `qihealth-marketing`
9. Verifica que aparecen las 51 skills en la lista de skills disponibles

### Verificación inmediata

En cualquier conversación de Cowork, ejecuta:

```
/qihealth-marketing necesito un reel pilar de Legacy TOF
```

Si el sistema responde con el output estructurado (script + hooks + CTAs + quality gates), está instalado correctamente.

---

## Paso 4 — Replicar en Mac mini (cuando llegue)

En la Mac mini:

1. Instala Cowork
2. Login con `jat@qihealth.ai` (misma cuenta)
3. Settings → Plugins → ya verás el marketplace QiHealth listado (porque es a nivel cuenta/org)
4. Install el plugin
5. Reconecta MCPs (OAuth se hace por device)
6. Activa scheduled tasks **SOLO en la Mac mini**

---

## Paso 5 — Updates futuros (cuando agreguemos skills nuevas)

Cuando construyamos skills nuevas o ajustemos memoria (ej: claims aprobados por advisory):

### En Cowork (o en tu editor)

Edita el archivo en local en la Mac mini o laptop. Ejemplo: agregar claim aprobado a `memory/cofepris-claim-library.md`.

### En Terminal

```bash
cd ~/Downloads/qihealth-marketing-plugin  # o donde tengas el repo
git add memory/cofepris-claim-library.md
git commit -m "Add claim aprobado por advisory: [breve descripción]"
git push
```

### En Cowork

Cowork detecta automáticamente la nueva versión del marketplace y te ofrece updateit (en Settings → Plugins, verás un badge de "Update available").

---

## Estructura del repo (referencia)

```
qihealth-marketing-plugin/
├── .claude-plugin/
│   └── plugin.json          # Manifest del plugin
├── .gitignore               # Archivos ignorados
├── README.md                # Documentación principal
├── GITHUB-SETUP.md          # Este archivo
├── skills/                  # 51 skills
│   ├── orchestrator/
│   │   └── SKILL.md
│   ├── persona-no-measurers/
│   │   └── SKILL.md
│   └── ... (49 más)
├── memory/                  # Memoria pre-cargada
│   ├── strategy-v4.3-summary.md
│   ├── brand-voice.md
│   ├── cofepris-rules.md
│   ├── competitors.md
│   ├── kpis-by-segment.md
│   ├── product-catalog.md
│   ├── ad-references.md     # Llenar con referencias de Jose
│   ├── cofepris-claim-library.md
│   └── ad-learnings.md      # Se llena con uso
└── scheduled-tasks/         # 5 scheduled tasks
    ├── morning-brief-7am.yaml
    ├── competitor-watch-6h.yaml
    ├── weekly-prep-friday.yaml
    ├── monthly-perf-report.yaml
    └── seo-rank-tracking.yaml
```

---

## Permisos del repo

### Inicial (solo tú)
- Owner: jat@qihealth.ai (full access)

### Cuando entren los otros (mes 1-2)
- **Christian Frey (advisory)**: read access (para validar claims approving)
- **Performance Manager**: read access (puede sugerir mejoras vía PRs)
- **Community Manager**: read access
- **Luis (commercial)**: read access (solo si vas a darle acceso al sistema)

Settings → Manage Access en GitHub.

---

## Si algo falla

### "Permission denied (publickey)" al hacer push
SSH key no configurada. Usa HTTPS con Personal Access Token, o configura SSH key en github.com/settings/keys.

### Cowork dice "Plugin not detected"
Verifica que:
1. `.claude-plugin/plugin.json` está en el root del repo (NO dentro de una subcarpeta)
2. El JSON es válido (puedes validar en jsonlint.com)
3. El campo `name` es kebab-case correcto

### Cowork no aparece el marketplace nuevo
- Cierra y reabre Cowork
- Verifica que GitHub OAuth está autorizado en Cowork Settings → Integrations
- Confirma que tu cuenta de GitHub tiene acceso al repo privado

### "Refusing to update because remote contains work"
Si GitHub creó automáticamente un commit (README default), pull primero:
```bash
git pull origin main --rebase
git push
```

---

## Checklist de validación post-setup

- [ ] Repo creado en GitHub como `qihealth-marketing-plugin` (private)
- [ ] Push inicial exitoso (51 skills visibles en GitHub UI)
- [ ] Marketplace agregado en Cowork con la URL del repo
- [ ] Plugin instalado en Cowork (laptop)
- [ ] Test exitoso: `/qihealth-marketing` responde
- [ ] Plugin instalado en Mac mini (cuando llegue)
- [ ] Scheduled tasks activados SOLO en Mac mini
- [ ] MCPs reconectados en Mac mini
- [ ] 9 Slack channels creados
- [ ] Médico revisor agregado a `#qihealth-medical-review`
- [ ] Luis agregado a `#qihealth-commercial-handoffs`

---

## Comando rápido — copy-paste

Para acelerar el paso 2, este es el bloque completo (REEMPLAZA URL):

```bash
cd ~/Downloads/qihealth-bundle-macmini/qihealth-marketing-plugin && \
git init && \
git config user.email "jat@qihealth.ai" && \
git config user.name "Jose Torres" && \
git add . && \
git commit -m "Initial commit — qihealth-marketing v0.2.0" && \
git branch -M main && \
git remote add origin https://github.com/qihealth/qihealth-marketing-plugin.git && \
git push -u origin main
```

Ejecutalo de una sola vez. Si pide credenciales, autentica con tu Personal Access Token de GitHub.
