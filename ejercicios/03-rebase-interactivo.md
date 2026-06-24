# Ejercicio 3 — Rebase interactivo

> **Duración:** 5 min  
> **Cuándo:** justo después del bloque 03 Integración

---

## Objetivo

Convertir una historia sucia de 4 commits de desarrollo (WIPs, fixes, typos) en 1 commit limpio y atómico, listo para un MR. Esto es lo que harás antes de cada PR en el mundo real.

---

## Pasos

### 1. Crea una rama con historia sucia

```bash
git checkout -b feature/mi-feature
echo "v1" > feat.js  && git add . && git commit -m "WIP"
echo "v2" >> feat.js && git add . && git commit -m "fix typo"
echo "v3" >> feat.js && git add . && git commit -m "almost done"
echo "v4" >> feat.js && git add . && git commit -m "Add feature"
git log --oneline
```

Verás 4 commits: exactamente el tipo de historia que no querrías que nadie vea en un MR.

### 2. Lanza el rebase interactivo

```bash
git rebase -i HEAD~4
```

Se abrirá tu editor con algo así:

```
pick abc123 WIP
pick def456 fix typo
pick ghi789 almost done
pick jkl012 Add feature
```

> ⚠️ El commit más **antiguo** va arriba — al revés que `git log`.

### 3. Edita el plan

Cambia el archivo para que quede así:

```
pick jkl012 Add feature
fixup ghi789 almost done
fixup def456 fix typo
drop abc123 WIP
```

Guarda y cierra el editor (`Esc` → `:wq` en vim, o cierra la pestaña en VS Code).

### 4. Comprueba el resultado

```bash
git log --oneline
```

Un solo commit limpio: `Add feature`. 🎉

---

## Opciones del editor

| Opción | Qué hace |
|--------|----------|
| `pick` | Mantiene el commit tal cual |
| `reword` | Mantiene el commit pero abre el editor para cambiar el mensaje |
| `squash` | Junta con el commit anterior y abre el editor para editar el mensaje combinado |
| `fixup` | Junta con el anterior y descarta el mensaje (el más cómodo para limpiar) |
| `drop` | Elimina el commit completamente |
| `exec` | Ejecuta un comando de shell entre commits |

---

## Reglas importantes

**El orden importa:** lo que escribes en el editor es el orden de aplicación de los commits, de arriba hacia abajo. El commit de arriba es el más antiguo.

**Solo en trabajo local:** el rebase cambia los SHAs de los commits. Si ya hiciste push de esa rama, necesitarías un `push --force-with-lease`, lo que puede causar problemas a quien haya trabajado sobre ella. La regla de oro: **rebasea antes de hacer push**.

---

## Bonus: si abres el editor y te arrepientes

```bash
git rebase --abort
```

Vuelves exactamente al estado anterior, como si no hubieras ejecutado nada.

---

## Comandos de referencia

```bash
git rebase -i HEAD~N            # rebase interactivo de los últimos N commits
git rebase -i main              # rebase interactivo de todo lo que va por delante de main
git rebase --continue           # continuar después de resolver un conflicto
git rebase --abort              # cancelar y volver al estado anterior
git push --force-with-lease     # push seguro después de rebase (comprueba que nadie más ha pusheado)
```
