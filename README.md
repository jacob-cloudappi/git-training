# 🧪 Formación Git — Repo de práctica

Bienvenido/a al repo de la formación de verano 2026.

Aquí harás los ejercicios en vivo durante la sesión. Antes de que empiece necesitas completar los tres pasos de abajo — no te llevará más de 10 minutos y nos ahorrarás ese tiempo al grupo el día de la formación.

---

## Antes de la sesión: prepárate en 3 pasos

### Paso 1 — Comprueba que tienes Git instalado

Abre una terminal y ejecuta:

```bash
git --version
```

Necesitas la versión **2.23 o superior**. Si el comando no existe o la versión es antigua:

- **macOS** → `brew install git`
- **Windows** → descarga el instalador desde [git-scm.com/download/win](https://git-scm.com/download/win)
- **Ubuntu/Debian** → `sudo apt install git`

---

### Paso 2 — Configura tu identidad

Esto es lo primero que Git necesita para poder hacer commits. Ejecuta los cuatro comandos:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
git config --global pull.rebase true
git config --global rerere.enabled true
```

Sustituye `"Tu Nombre"` y `"tu@email.com"` por los tuyos. El email debe ser el mismo que usas en GitHub.

---

### Paso 3 — Clona el repo y crea tu rama

```bash
git clone https://github.com/jacob-cloudappi/git-training
cd git-training
git checkout -b practica/tu-nombre
```

Sustituye `tu-nombre` por tu nombre real en minúsculas y sin espacios, por ejemplo `practica/pablo` o `practica/ana-garcia`.

Haz un primer commit para verificar que todo funciona:

```bash
echo "# Práctica de $(git config user.name)" > mi-practica.md
git add mi-practica.md
git commit -m "Setup: rama de práctica lista"
git push -u origin practica/tu-nombre
```

Si el push funciona sin errores, **estás listo/a**. 🎉

---

## Verificación rápida

Ejecuta esto y comprueba que el output tiene sentido:

```bash
git log --oneline
git status
```

Deberías ver tu commit en el log y el directorio limpio en el status.

---

## Estructura del repo

```
git-training/
├── README.md          ← este archivo
├── ejercicios/
│   ├── 01-fundamentos.md
│   ├── 02-deshacer-y-reflog.md
│   └── 03-rebase-interactivo.md
└── mi-practica.md     ← lo creas tú en el paso 3
```

Los enunciados detallados de cada ejercicio están en la carpeta `ejercicios/`. Los iremos abriendo durante la sesión — no hace falta que los leas antes.

---

## Si te quedas atascado/a

**GitHub te pide usuario y contraseña en cada push:**

Lo más cómodo es usar SSH. Genera una clave y añádela a tu cuenta siguiendo [esta guía de GitHub](https://docs.github.com/es/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent). Si prefieres HTTPS, crea un token de acceso personal en **GitHub → Settings → Developer settings → Personal access tokens** (scope: `repo`) y úsalo como contraseña.

**El push falla con "Permission denied" o "remote: Permission to ... denied":**

Comprueba que estás logueado con la cuenta correcta y que tienes acceso al proyecto. Si no, escríbeme.

**No tienes permisos para instalar nada en tu máquina:**

Avísanos antes de la sesión para buscarte una solución.

---

## El día de la formación

- Llega con el repo clonado y tu rama creada
- Tendrás la terminal abierta y lista para escribir
- Usaremos el repo compartido en el ejercicio de merge/PR del bloque de integración — el resto lo harás en local sobre tu propia rama

---

*Cualquier problema antes de la sesión, escríbeme: jacob@cloudappi.net*
