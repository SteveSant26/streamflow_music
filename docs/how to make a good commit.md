# ✅ Buenas prácticas para crear commits

## 1. 🧠 Haz commits pequeños y enfocados

Cada commit debe representar una sola idea o cambio.

**Ej:** "Agregar validación de email", no "cambios varios".

**✔️ Bueno:**

```bash
feat(auth): validate email format before submit
```

**❌ Malo:**

```bash
fix: arreglos varios en login y estilos
```

## 2. ✍️ Usa mensajes de commit claros y consistentes

Utiliza un mensaje claro, en presente y en voz activa. Ejemplo:

**✔️ Bueno:**

```bash
fix(form): prevent empty submission on enter key
```

**❌ Malo:**

```bash
arreglado que se enviaba sin datos
```

## 3. 🎨 Sigue un formato estándar como Conventional Commits

El formato más recomendado hoy en día es Conventional Commits:

```bash
<tipo>(opcional: contexto): descripción clara y concisa
```

**Ejemplos:**

```bash
feat(login): add remember me checkbox
fix(auth): handle token expiration
refactor(api): simplify user fetch logic
docs(readme): add setup instructions
test(api): add unit tests for user service
chore(lint): update eslint config
```

### 📌 Tipos comunes:

- **feat:** nueva funcionalidad
- **fix:** arreglo de bugs
- **docs:** documentación
- **style:** cambios que no afectan lógica (espacios, comas, etc.)
- **refactor:** reestructuración sin cambiar comportamiento
- **test:** pruebas
- **chore:** tareas de mantenimiento (ci, deps, config)

## 4. 📚 Escribe descripciones si el cambio lo necesita

Usa el cuerpo del commit (después del título) para dar contexto adicional:

```bash
feat(auth): support Google OAuth2 login

This adds a new button to initiate OAuth2 flow with Google. The backend
now accepts a Google token and returns a local JWT.
```

## 5. ✅ Commitea código funcional y probado

Evita hacer commit de código que:

- rompe el build
- no pasa los linters
- o no ha sido probado mínimamente

## 6. 🚫 Evita commits innecesarios

No hagas commits de cosas como:

- Archivos generados (`.pyc`, `dist/`, `node_modules/`)
- Mensajes como "Update", "prueba", "otra vez", etc.

Usa `.gitignore` para excluir archivos innecesarios.

## 7. 🧹 Agrupa cambios relacionados

Si trabajas en algo que involucra varios archivos, agrúpalos en un solo commit lógico si tienen relación.

## 8. 🔧 Usa herramientas que te obliguen a seguir estas reglas

- **pre-commit:** para asegurarte de no subir código sucio
- **commitlint:** para validar que los mensajes sigan Conventional Commits
- **husky:** para ejecutar scripts como linters antes del commit
- **cz-cli (commitizen):** para ayudarte a escribir mensajes estándar desde CLI

## 📦 Ejemplo de buen historial de commits

```bash
feat(user): add user registration endpoint
fix(user): validate email format in schema
refactor(user): extract email validator to utils
docs(api): document /register endpoint in README
test(user): add unit tests for registration flow
```
