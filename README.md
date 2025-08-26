# 🔐 Ejercicio Práctico 1 – Pipeline CI/CD Vulnerable

Este repositorio contiene un **pipeline intencionalmente vulnerable**, desarrollado como parte del portafolio de ciberseguridad.  
El objetivo es **identificar debilidades en un flujo CI/CD** y posteriormente proponer una versión **segura y endurecida**, siguiendo buenas prácticas de **DevSecOps**.

---

## 🚨 Importante
Este pipeline está diseñado **solo para fines educativos y demostrativos**.  
⚠️ **No debe usarse en producción**, ya que contiene malas prácticas de seguridad.

---

## 📂 Contenido
- `.github/workflows/insecure-pipeline.yml` → Workflow con vulnerabilidades.
- `.github/workflows/secure-pipeline.yml` → Versión mejorada (endurecida) como referencia.
- Documentación del informe asociado.

---

## 🧩 Vulnerabilidades presentes en el pipeline
El archivo `insecure-pipeline.yml` contiene, entre otras, las siguientes debilidades:

1. **Despliegue directo a producción** en cada `push` a `main`.
2. **Uso de `pull_request_target` con secrets expuestos**.
3. **Permisos excesivos** (`permissions: write-all`).
4. **Dependencias instaladas sin lockfile** (`npm install`).
5. **Pruebas que no bloquean el pipeline** (`continue-on-error: true`).
6. **Secrets escritos en disco** (`~/.ssh/key.pem`).
7. **Acciones no fijadas por versión** (`@master` en lugar de pin por SHA).
8. **`git pull` en servidor de producción** → despliegue no inmutable.
9. **Servicio levantado con `screen` y `flask run` en puerto 80 sin TLS**.

---

## ✅ Versión segura propuesta
En `secure-pipeline.yml` se incluyen medidas correctivas como:
- Integración de **SAST (CodeQL)** y **SCA (OWASP Dependency-Check/Snyk)**.
- Escaneo de **contenedores/IaC (Trivy, Checkov)**.
- **SBOM (Syft)** y firma de artefactos (**Cosign**).
- Despliegue **inmutable** (artefacto desde GHCR/S3).
- Uso de **OIDC** para autenticación sin claves estáticas.
- **Aprobación manual** antes de desplegar a producción.
- Servicio gestionado con **systemd** + **Nginx con TLS**.

---

## 📊 Objetivo del informe
El informe que acompaña este ejercicio muestra:
- Tabla de **debilidades vs. mitigaciones**.
- **Diagrama de flujo** del pipeline seguro.
- **Beneficios** de aplicar DevSecOps:
  - Reducción de riesgo.
  - Mejor trazabilidad.
  - Cumplimiento normativo.
  - Velocidad de entrega sostenible.

---

## 👩🏻‍💻 Autora
- **Alicia Vento**  
Portafolio de Ciberseguridad – 2025  
