# Playbook de instalación y configuración de Redmine

Este playbook de Ansible automatiza la instalación y configuración de Redmine desde código fuente. Utiliza `rbenv` para gestionar Ruby y configura Redmine con MySQL como base de datos.

## Requisitos


- Acceso a usuario con privilegios de `sudo`.
- Sistema operativo destino: **Ubuntu 22.04 (Jammy Jellyfish)** o **Ubuntu 24.04**.
- Conexión a internet para descargar Redmine y dependencias.

## Variables

- `redmine_version`: Define la versión de Redmine a instalar. Por ejemplo:

  ```yaml
  redmine_version: 6.0.5


## Funcionalidades del playbook

1. Instala dependencias necesarias para Ruby.
2. Instala y configura `rbenv` para el manejo de Ruby.
3. Descarga y descomprime el código fuente de Redmine.
4. Copia los templates de configuración:

   * `Gemfile.j2`
   * `database.yml.j2`
5. Instala las gemas del `Gemfile`.
6. Ejecuta las tareas de inicialización:

   * Generación del token secreto.
   * Migraciones de base de datos.
   * Carga de datos por defecto.
7. Inicia el servidor Redmine en segundo plano usando Puma.


## Estructura esperada

* `templates/database.yml.j2`: Template del archivo de configuración de la base de datos.
* `templates/Gemfile.j2`: Template del archivo `Gemfile` para instalar las gemas.
* `templates/redmine.service.j2`: Template del archivo `redmine.service` para configurar redmine como servicio.

## Consideraciones

* El PATH de `rbenv` se exporta e inicializa en cada tarea que lo requiere, para asegurar que esté disponible incluso cuando `.bashrc` no se evalúa (como es el caso en tareas no interactivas de Ansible).
* El script se diseñó para usarse en entornos nuevos y controlados, donde no existe Ruby instalado previamente.
