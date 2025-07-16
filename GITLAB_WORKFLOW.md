# GitLab Workflow - Branch Strategy

Este repositorio utiliza el workflow de GitLab (GitFlow) con las siguientes ramas:

## Estructura de Ramas

### 🔥 main
- **Propósito**: Rama de producción
- **Estabilidad**: Completamente estable
- **Despliegues**: Solo código listo para producción
- **Protección**: Protegida contra pushes directos

### 🚀 develop
- **Propósito**: Rama de desarrollo principal
- **Estabilidad**: Desarrollo activo
- **Integración**: Donde se integran todas las features
- **Base para**: Nuevas features y releases

### 🧪 testing
- **Propósito**: Rama de pruebas
- **Estabilidad**: Para testing y QA
- **Flujo**: develop → testing → staging → main
- **Pruebas**: Pruebas de integración y funcionales

### 🎭 staging
- **Propósito**: Preproducción
- **Estabilidad**: Ambiente similar a producción
- **Validación**: Pruebas finales antes del release
- **Despliegue**: Staging environment

## Flujo de Trabajo

### 1. Desarrollo de Features
```bash
# Crear feature branch desde develop
git checkout develop
git checkout -b feature/nueva-funcionalidad

# Trabajar en la feature
git add .
git commit -m "feat: nueva funcionalidad"

# Push y crear PR hacia develop
git push origin feature/nueva-funcionalidad
```

### 2. Proceso de Testing
```bash
# Merge develop → testing
git checkout testing
git merge develop

# Ejecutar pruebas
npm test
# o los comandos de testing específicos
```

### 3. Staging y Preproducción
```bash
# Merge testing → staging (después de pruebas exitosas)
git checkout staging
git merge testing

# Validación final en staging environment
```

### 4. Release a Producción
```bash
# Merge staging → main (después de validación)
git checkout main
git merge staging

# Tag del release
git tag -a v1.0.0 -m "Release v1.0.0"
git push origin v1.0.0
```

## Tipos de Ramas

### Feature Branches
- **Nomenclatura**: `feature/nombre-feature`
- **Base**: `develop`
- **Destino**: `develop`
- **Ejemplo**: `feature/github-integration`

### Hotfix Branches
- **Nomenclatura**: `hotfix/descripcion-fix`
- **Base**: `main`
- **Destino**: `main` y `develop`
- **Ejemplo**: `hotfix/security-patch`

### Release Branches
- **Nomenclatura**: `release/version`
- **Base**: `develop`
- **Destino**: `main` y `develop`
- **Ejemplo**: `release/v1.2.0`

## Reglas de Merge

### Pull Request Requirements
1. **Code Review**: Al menos 1 revisor
2. **Tests**: Todas las pruebas deben pasar
3. **Documentation**: Documentación actualizada
4. **Conflicts**: Sin conflictos de merge

### Branch Protection
- `main`: Solo merge via PR, require reviews
- `develop`: Merge directo permitido para maintainers
- `testing`: Merge desde develop solamente
- `staging`: Merge desde testing solamente

## Comandos Útiles

### Sincronización de Ramas
```bash
# Actualizar todas las ramas
git fetch origin
git checkout main && git pull origin main
git checkout develop && git pull origin develop
git checkout testing && git pull origin testing
git checkout staging && git pull origin staging
```

### Cleanup de Ramas
```bash
# Eliminar ramas locales merged
git branch --merged develop | grep -v "main\|develop\|testing\|staging" | xargs -n 1 git branch -d

# Eliminar ramas remotas
git remote prune origin
```

## Convenciones de Commits

Usamos [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` Nueva funcionalidad
- `fix:` Corrección de bug
- `docs:` Documentación
- `style:` Cambios de formato
- `refactor:` Refactorización
- `test:` Pruebas
- `chore:` Mantenimiento

## Ambientes

| Rama | Ambiente | URL | Propósito |
|------|----------|-----|-----------|
| main | Production | https://prod.example.com | Producción |
| staging | Staging | https://staging.example.com | Preproducción |
| testing | Testing | https://testing.example.com | QA/Testing |
| develop | Development | https://dev.example.com | Desarrollo |

## Checklist de Release

### Pre-release
- [ ] Todas las features merged en develop
- [ ] Testing completo en rama testing
- [ ] Staging validation exitosa
- [ ] Documentación actualizada
- [ ] CHANGELOG.md actualizado

### Release
- [ ] Merge a main
- [ ] Tag de versión creado
- [ ] Release notes publicadas
- [ ] Deployment a producción
- [ ] Notificación al equipo

### Post-release
- [ ] Merge back a develop
- [ ] Cleanup de ramas obsoletas
- [ ] Monitoreo de producción
- [ ] Actualización de issues cerrados
