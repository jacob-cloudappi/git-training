# Ejercicio 1 — Setup y modelo de objetos

> **Duración:** 3-4 min  
> **Cuándo:** justo después del bloque 01 Fundamentos

---

## Objetivo

Ver con tus propios ojos que Git es una base de datos de contenido: commits, trees y blobs con sus SHAs. Y comprobar que dos archivos con el mismo contenido comparten el mismo objeto.

---

## Pasos

### 1. Asegúrate de estar en tu rama

```bash
git checkout practica/tu-nombre
git status   # debe decir "nothing to commit"
```

### 2. Explora el último commit

```bash
git cat-file -p HEAD
```

Verás algo así:

```
tree abc123...
parent def456...
author Tu Nombre <tu@email.com> 1234567890 +0100
committer Tu Nombre <tu@email.com> 1234567890 +0100

Setup: rama de práctica lista
```

### 3. Mira dentro del tree

Copia el SHA del `tree` que aparece arriba y ejecuta:

```bash
git cat-file -p <SHA-del-tree>
```

Verás la lista de archivos con sus blobs. Para ver el contenido de un blob:

```bash
git cat-file -p <SHA-del-blob>
```

### 4. Prueba la deduplicación

```bash
echo "hola" > a.txt
echo "hola" > b.txt
git add a.txt b.txt
git commit -m "Dos archivos, mismo contenido"
git cat-file -p HEAD^{tree}
```

Fíjate: `a.txt` y `b.txt` tienen **el mismo SHA de blob**. Git solo almacenó el contenido una vez.

---

## ¿Qué observar?

- El commit tiene: `tree`, `parent`, `author`, `committer` y mensaje
- El tree lista archivos con sus hashes
- Mismo contenido → mismo SHA → un solo objeto almacenado
- El SHA cambia si cambias cualquier cosa, incluso el timestamp

---

## Comandos de referencia

```bash
git cat-file -p HEAD          # ver el commit actual
git cat-file -p HEAD^{tree}   # ver el tree del commit actual
git cat-file -p <SHA>         # ver cualquier objeto por su SHA
git cat-file -t <SHA>         # ver el tipo (blob, tree, commit)
git cat-file -s <SHA>         # ver el tamaño en bytes
```
