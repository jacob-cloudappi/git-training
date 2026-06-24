# Ejercicio 2 — Deshacer y recuperar con reflog

> **Duración:** 4-5 min  
> **Cuándo:** justo después del bloque 02 Comandos esenciales

---

## Objetivo

El más impactante de la sesión: hacer un `reset --hard` que "destruye" commits y recuperarlos con `git reflog`. Verás que Git casi nunca borra nada de verdad.

---

## Pasos

### 1. Crea varios commits

```bash
echo "version 1" > ver.txt && git add . && git commit -m "v1"
echo "version 2" > ver.txt && git add . && git commit -m "v2"
echo "version 3" > ver.txt && git add . && git commit -m "v3"
git log --oneline
```

Deberías ver los tres commits: `v1`, `v2`, `v3`.

### 2. Simula el desastre

```bash
git reset --hard HEAD~2
git log --oneline
```

Solo ves `v1`. Los commits `v2` y `v3` han "desaparecido".

### 3. Busca en el reflog

```bash
git reflog
```

Verás algo así:

```
abc123 HEAD@{0}: reset: moving to HEAD~2
def456 HEAD@{1}: commit: v3
ghi789 HEAD@{2}: commit: v2
...
```

### 4. Recupera

```bash
git reset --hard HEAD@{1}
git log --oneline
```

`v2` y `v3` están de vuelta. 🎉

---

## ¿Qué ha pasado realmente?

`reset --hard` **no borra el commit**. Solo mueve el puntero HEAD hacia atrás. El objeto sigue existiendo en `.git/objects` hasta que `git gc` lo limpie, lo que no ocurre hasta ~90-104 días después.

Por eso el reflog puede encontrarlo: sabe a dónde apuntaba HEAD antes del reset.

---

## Otras formas de recuperar un commit "perdido"

```bash
# Crear una rama nueva desde ese commit (sin mover HEAD)
git branch rescate <SHA>

# Traer solo ese commit a la rama actual
git cherry-pick <SHA>
```

---

## Para reflexionar

| Situación | Comando adecuado |
|-----------|-----------------|
| Quiero deshacer el commit pero guardar los cambios para reeditarlos | `git reset --soft HEAD~1` |
| Quiero deshacer el commit y dejar los cambios sin stage | `git reset --mixed HEAD~1` |
| Quiero empezar desde cero, no me importan los cambios | `git reset --hard HEAD~1` |

---

## Comandos de referencia

```bash
git reflog                      # historial completo de movimientos de HEAD
git reflog --since="2 hours ago"  # filtrar por tiempo
git reset --hard HEAD@{N}      # volver a esa posición del reflog
git reset --hard <SHA>          # volver a un commit concreto
git branch rescate <SHA>        # crear rama sin mover HEAD
```
