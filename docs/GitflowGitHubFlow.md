
---

# 📘 Guía completa para trabajar con Git y branching strategy (Gitflow / GitHub Flow)

---

## ✅ ¿Qué es Git y por qué lo usamos?

**Git** es un sistema de control de versiones. Nos permite:

* Guardar cambios del código a lo largo del tiempo (como guardar versiones de un documento).
* Trabajar varias personas en el mismo proyecto sin pisarse el trabajo.
* Crear ramas (branches) para probar cosas nuevas sin afectar el código final.
* Volver a una versión anterior si algo sale mal.
* Organizar nuestro trabajo de forma profesional y ordenada.

> 💡 Usar Git es como tener un historial de versiones de tu proyecto, poder hacer copias controladas, trabajar en paralelo con tu equipo, y combinar todo de manera segura.

---

## 🛠️ ¿Qué necesito antes de empezar?

1. Tener instalado **Git**:

```bash
sudo apt install git           # En Linux (Debian/Ubuntu)
brew install git               # En MacOS
winget install Git.Git         # En Windows con winget
```

2. Configura tus datos:

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tucorreo@ejemplo.com"
```

3. Tener una cuenta en [GitHub](https://github.com/) o en otro proveedor como GitLab o Bitbucket.

---

## 🧱 ¿Cómo empiezo un proyecto con Git?

### Opción 1: Crear un proyecto nuevo

```bash
mkdir mi-proyecto
cd mi-proyecto
git init
```

> `git init` crea el repositorio Git local.

Crea archivos básicos:

```bash
touch README.md .gitignore
echo "node_modules/" >> .gitignore  # ejemplo
git add .
git commit -m "chore: inicializa proyecto"
```

### Opción 2: Clonar un proyecto existente

```bash
git clone https://github.com/usuario/proyecto.git
cd proyecto
```

---

## 📂 Instalación del proyecto (para proyectos con dependencias)

Si el proyecto usa:

### Node.js:

```bash
npm install
```

### Python:

```bash
pip install -r requirements.txt
```

### Otros entornos:

* Django: `python manage.py migrate && python manage.py runserver`
* React: `npm start`
* Laravel: `composer install && php artisan serve`

> Lee el archivo `README.md`, casi siempre tiene las instrucciones.

---

## 🧠 ¿Qué es una rama (branch) y por qué la usamos?

Las ramas son **caminos paralelos de desarrollo**. Nos permiten trabajar en:

* Nuevas funcionalidades (features)
* Correcciones de errores (bugfixes/hotfixes)
* Versiones de lanzamiento (releases)

> Así mantenemos el código principal (`main` o `develop`) **siempre funcionando**, mientras probamos cosas nuevas sin romperlo.

---

## 🌱 Gitflow explicado (¿cuándo y por qué?)

Gitflow es útil cuando:

* El proyecto tiene varias versiones (v1.0, v1.1…)
* Trabajas en equipo
* Hay pruebas antes de poner en producción

### 🧭 Ramas clave:

| Rama        | Propósito                                           |
| ----------- | --------------------------------------------------- |
| `main`      | Código en producción                                |
| `develop`   | Código que ya pasó pruebas y está listo para lanzar |
| `feature/*` | Nuevas funcionalidades en desarrollo                |
| `release/*` | Preparación de versión antes de lanzar              |
| `hotfix/*`  | Correcciones urgentes directamente en producción    |

---

## 🧪 Flujo de trabajo Gitflow explicado con comandos

### 🔧 A) Crear nueva funcionalidad

```bash
git checkout develop
git checkout -b feature/login-form
```

¿Por qué? Porque no queremos afectar el código que ya funciona (`develop`) mientras hacemos cambios nuevos.

Haz tus cambios:

```bash
git add .
git commit -m "feat: agrega formulario de login"
```

Cuando termines:

```bash
git checkout develop
git merge feature/login-form
git push origin develop
git branch -d feature/login-form
```

---

### 🚨 B) Corregir un error urgente (hotfix)

```bash
git checkout main
git checkout -b hotfix/fix-404-error
```

Corrige y haz commit:

```bash
git commit -am "fix: corrige error 404 en página de contacto"
```

Sube y mergea:

```bash
git checkout main
git merge hotfix/fix-404-error
git push origin main
```

También actualiza develop:

```bash
git checkout develop
git merge hotfix/fix-404-error
git push origin develop
```

---

### 🧪 C) Preparar una release

```bash
git checkout develop
git checkout -b release/1.0.0
```

Haz los ajustes finales (versión, documentación):

```bash
git commit -am "chore: prepara versión 1.0.0"
```

Merge final:

```bash
git checkout main
git merge release/1.0.0
git push origin main

git checkout develop
git merge release/1.0.0
git push origin develop
```

---

## 🌐 GitHub Flow explicado (¿cuándo y por qué?)

GitHub Flow es útil cuando:

* Haces despliegues rápidos y constantes
* Trabajas con integración continua (CI/CD)
* El proyecto no necesita versiones planeadas

---

### 🔄 Flujo de trabajo GitHub Flow

1. Siempre trabajas desde `main`
2. Cada funcionalidad o bug se trabaja en una rama temporal

```bash
git checkout main
git pull origin main
git checkout -b feature/pagina-contacto
```

Haz tus cambios, sube tu rama:

```bash
git add .
git commit -m "feat: agrega página de contacto"
git push origin feature/pagina-contacto
```

Abre un **Pull Request** en GitHub.

Cuando se aprueba, haz merge a `main`.

Luego actualiza tu repositorio:

```bash
git checkout main
git pull origin main
```

---

## 🧼 Cosas importantes que la mayoría olvida

### ❗ Asegúrate de estar actualizado antes de empezar

```bash
git checkout develop  # o main
git pull origin develop
```

### ❗ No trabajes directamente en `main` o `develop`

Siempre crea ramas para tus cambios.

### ❗ Usa nombres descriptivos

| Tipo    | Formato          |
| ------- | ---------------- |
| Feature | `feature/nombre` |
| Fix     | `fix/bug-nombre` |
| Hotfix  | `hotfix/urgente` |
| Release | `release/v1.2.0` |

---

## 🗂️ Estructura del repositorio sugerida

```
📦 proyecto/
├── src/                # Código fuente principal
├── tests/              # Pruebas unitarias
├── .github/workflows/  # Automatizaciones (CI/CD)
├── README.md           # Documentación
├── .gitignore          # Archivos que Git debe ignorar
├── package.json        # Node.js (si aplica)
├── requirements.txt    # Python (si aplica)
```

---

## ✍️ Ejemplos de mensajes de commit

| Tipo     | Ejemplo                                  |
| -------- | ---------------------------------------- |
| feat     | `feat: agrega validación de email`       |
| fix      | `fix: corrige error de login`            |
| chore    | `chore: actualiza dependencias`          |
| docs     | `docs: mejora el README`                 |
| refactor | `refactor: simplifica lógica de filtros` |

> 💡 Usa `git log` para ver tu historial de commits.

---

## ❓¿Qué pasa si...?

### ❓No terminé mi tarea pero me voy

Haz un commit temporal:

```bash
git add .
git commit -m "WIP: trabajando en X"
```

O guarda tu progreso sin hacer commit:

```bash
git stash
```

Luego puedes recuperarlo:

```bash
git stash pop
```

---

## 🔄 Comandos útiles que debes conocer

| Acción                   | Comando                         |
| ------------------------ | ------------------------------- |
| Ver ramas                | `git branch`                    |
| Crear rama               | `git checkout -b rama-nueva`    |
| Cambiar de rama          | `git checkout rama`             |
| Ver estado del proyecto  | `git status`                    |
| Ver historial de commits | `git log --oneline --graph`     |
| Ver diferencias          | `git diff`                      |
| Subir rama               | `git push origin rama`          |
| Eliminar rama local      | `git branch -d rama`            |
| Eliminar rama remota     | `git push origin --delete rama` |

---