
# Andean Agrotech - Demo

Sistema de demostración para la gestión inteligente de recursos agrícolas andinos.

## 📋 Requisitos Previos

Para ejecutar esta demo necesitas:

- **PHP 7.4 o superior** (recomendado PHP 8.0+)
- **MySQL 5.7 o superior** (o MariaDB 10.3+)
- **Servidor web** (Apache o Nginx) o PHP Built-in Server
- **Composer** (opcional, para gestionar dependencias si las hay)

## 🚀 Instalación Rápida

### Paso 1: Clonar/Descargar el proyecto

Si tienes el proyecto en un repositorio:
```bash
git clone [URL_DEL_REPOSITORIO]
cd Innova
```

### Paso 2: Configurar la base de datos

1. Crea una base de datos MySQL:
```sql
CREATE DATABASE andean_agrotech;
```

2. Crea un usuario (opcional, puedes usar root para la demo):
```sql
CREATE USER 'agrotech_user'@'localhost' IDENTIFIED BY 'tu_password';
GRANT ALL PRIVILEGES ON andean_agrotech.* TO 'agrotech_user'@'localhost';
FLUSH PRIVILEGES;
```

3. Importa el esquema de la base de datos (si tienes un archivo SQL):
```bash
mysql -u agrotech_user -p andean_agrotech < database/schema.sql
```

### Paso 3: Configurar la conexión a la base de datos

Crea o edita el archivo de configuración `config/database.php`:

```php
<?php
return [
    'host' => 'localhost',
    'database' => 'andean_agrotech',
    'username' => 'agrotech_user',
    'password' => 'tu_password',
    'charset' => 'utf8mb4'
];
```

### Paso 4: Iniciar el servidor

**Opción A: Servidor PHP integrado (más fácil para demo)**

```bash
cd Andean_AgroTech_Web
php -S localhost:8000
```

Luego abre tu navegador en: `http://localhost:8000`

**Opción B: Apache/Nginx**

Configura tu servidor web para apuntar a la carpeta `Andean_AgroTech_Web`

## 📁 Estructura del Proyecto

```
Innova/
├── README.md
├── Andean_AgroTech_Web/
│   ├── index.html
│   ├── presentacion.html
│   ├── logo.png
│   └── (archivos PHP y otros)
├── config/
│   └── database.php (configuración de BD)
├── database/
│   └── schema.sql (esquema de base de datos)
└── (otros archivos del proyecto)
```

## 🛠️ Desarrollo

### Crear una conexión a la base de datos

Crea un archivo `Andean_AgroTech_Web/includes/db.php`:

```php
<?php
$config = require_once __DIR__ . '/../config/database.php';

try {
    $pdo = new PDO(
        "mysql:host={$config['host']};dbname={$config['database']};charset={$config['charset']}",
        $config['username'],
        $config['password'],
        [
            PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
            PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
        ]
    );
} catch (PDOException $e) {
    die("Error de conexión: " . $e->getMessage());
}
```

### Usar la conexión en tus archivos PHP

```php
<?php
require_once 'includes/db.php';

// Ejemplo de consulta
$stmt = $pdo->query("SELECT * FROM cultivos");
$cultivos = $stmt->fetchAll();
?>
```

## 📝 Notas para la Demo

- Este es un proyecto de demostración académica
- La configuración es básica y pensada para desarrollo local
- Para producción, considera implementar medidas de seguridad adicionales
- Los datos son de ejemplo para mostrar funcionalidades

## 🐛 Solución de Problemas

### Error de conexión a MySQL

- Verifica que MySQL esté corriendo: `sudo systemctl status mysql`
- Confirma que las credenciales en `config/database.php` sean correctas
- Asegúrate de que la base de datos existe

### Error 404 en el navegador

- Verifica que estés en el directorio correcto
- Confirma que el servidor esté corriendo en el puerto correcto
- Revisa la ruta en la barra de direcciones del navegador

### Permisos de archivos

Si tienes problemas con permisos:
```bash
chmod -R 755 Andean_AgroTech_Web
```

## 📚 Recursos

- [Documentación PHP](https://www.php.net/docs.php)
- [Documentación MySQL](https://dev.mysql.com/doc/)
- [Documentación PDO](https://www.php.net/manual/es/book.pdo.php)

---

**Nota:** Este README es para una configuración básica de demostración. Para un entorno de producción se requieren configuraciones adicionales de seguridad.

