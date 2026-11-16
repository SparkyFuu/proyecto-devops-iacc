# Proyecto DevOps - Reserva de horas médicas

Proyecto académico para ejecutar una página web estática de reserva de horas médicas con Nginx y Docker Compose. No utiliza base de datos, API ni servicios externos.

## Requisitos

- Git
- Docker Desktop con Docker Compose
- Navegador web

## Estructura

```text
proyecto-devops/
├── src/
│   ├── index.html
│   └── styles.css
├── .github/workflows/devops-automation.yml
├── .env.example
├── .gitignore
├── Dockerfile
├── docker-compose.yml
└── README.md
```

## Ejecución local

1. Copiar el archivo de ejemplo de variables:

```bash
cp .env.example .env
```

En Windows PowerShell se puede usar:

```powershell
Copy-Item .env.example .env
```

2. Construir e iniciar el servicio:

```bash
docker compose up -d --build
```

3. Revisar el estado:

```bash
docker compose ps
```

4. Abrir en el navegador:

```text
http://localhost:8080
```

5. Revisar logs y uso básico de recursos:

```bash
docker compose logs web
docker stats --no-stream reserva_medica_web
```

6. Detener y eliminar el contenedor:

```bash
docker compose down
```

## Seguridad aplicada

- `.env` está excluido mediante `.gitignore`.
- `.env.example` solo contiene valores de ejemplo y no secretos.
- La página avisa que no deben ingresarse datos personales reales.
- No existen claves, tokens ni credenciales dentro del repositorio.
- El servicio es estático y no persiste los datos del formulario.

## Estrategia Git propuesta

- `main`: versión estable.
- `feature/formulario-reserva`: cambios del sitio y configuración del contenedor.
- Commits pequeños y descriptivos.
- Pull request hacia `main` antes de fusionar.
- Revisión de archivos modificados y ejecución de validaciones antes del merge.

Ejemplos de commits:

```text
chore: iniciar estructura del proyecto
feat: agregar formulario de reserva medica
build: agregar nginx y docker compose
ci: agregar validacion basica con github actions
docs: completar instrucciones de ejecucion
```

## Automatización complementaria

El workflow `.github/workflows/devops-automation.yml` comprueba archivos obligatorios, construye la imagen, inicia un contenedor temporal y valida el servicio con `curl`. Es una ayuda para detectar problemas antes de integrar cambios, pero no reemplaza la verificación local solicitada con Docker Desktop.
