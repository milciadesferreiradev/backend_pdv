0# Backend PDV (Punto de Venta)

## Descripción

Este proyecto es un backend para un sistema de Punto de Venta (PDV) desarrollado con Spring Boot. Proporciona una API RESTful para gestionar categorías, productos, clientes, proveedores, ventas, compras, usuarios y roles. Incluye autenticación JWT, generación de reportes con JasperReports y soporte para impresión de tickets y códigos de barras.

## Características

- **Autenticación y Autorización**: Sistema de login con JWT y roles de usuario.
- **Gestión de Inventario**: CRUD para productos, categorías, proveedores y clientes.
- **Ventas y Compras**: Registro de transacciones de venta y compra con ítems detallados.
- **Reportes**: Generación de reportes en PDF usando JasperReports (productos, ventas, compras, tickets).
- **Auditoría**: Logs de operaciones para seguimiento.
- **API RESTful**: Endpoints documentados con Swagger.
- **Base de Datos**: PostgreSQL con JPA/Hibernate.
- **Contenedorización**: Dockerfile para despliegue en contenedores.

## Tecnologías Utilizadas

- **Java 17**
- **Spring Boot 3.3.2**
- **Spring Data JPA**
- **Spring Security**
- **JWT (JJWT)**
- **PostgreSQL**
- **JasperReports 6.20.0**
- **Lombok**
- **Maven**
- **Docker**

## Prerrequisitos

- Java 17 o superior
- Maven 3.6+
- PostgreSQL 12+
- Docker (opcional, para contenedorización)

## Instalación

1. Clona el repositorio:
   ```bash
   git clone https://github.com/milciadesferreiradev/backend_pdv.git
   cd backend_pdv
   ```

2. Instala las dependencias con Maven:
   ```bash
   mvn clean install
   ```

## Configuración

1. **Base de Datos**:
   - Crea una base de datos PostgreSQL llamada `postgres` (o configura en `application.properties`).
   - Ejecuta el script `database.sql` para inicializar la base de datos si es necesario.

2. **Archivo de Configuración**:
   Edita `src/main/resources/application.properties`:
   ```properties
   spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
   spring.datasource.username=tu_usuario
   spring.datasource.password=tu_contraseña
   application.security.jwt.secret=tu_secreto_jwt
   app.allowed.origins=http://localhost:3000
   app.printer.name=POS-58
   ```

   - `spring.datasource.*`: Configuración de la base de datos.
   - `application.security.jwt.secret`: Secreto para firmar tokens JWT (genera uno seguro).
   - `app.allowed.origins`: Orígenes permitidos para CORS.
   - `app.printer.name`: Nombre de la impresora para tickets.

## Ejecución

### Ejecutar Localmente

1. Asegúrate de que PostgreSQL esté corriendo.
2. Ejecuta la aplicación:
   ```bash
   mvn spring-boot:run
   ```
   La aplicación estará disponible en `http://localhost:8080`.

### Ejecutar con Docker

1. Construye la imagen:
   ```bash
   docker build -t backend-pdv .
   ```

2. Ejecuta el contenedor:
   ```bash
   docker run -p 8080:8080 backend-pdv
   ```

## API Endpoints

La API está organizada en controladores. Aquí un resumen de los principales endpoints:

### Autenticación
- `POST /auth/login`: Iniciar sesión y obtener token JWT.

### Usuarios
- `GET /users`: Listar usuarios.
- `POST /users`: Crear usuario.
- `PUT /users/{id}`: Actualizar usuario.
- `DELETE /users/{id}`: Eliminar usuario.

### Roles y Permisos
- `GET /roles`: Listar roles.
- `POST /roles`: Crear rol.
- `PUT /roles/{id}`: Actualizar rol.
- `DELETE /roles/{id}`: Eliminar rol.

### Categorías
- `GET /categories`: Listar categorías.
- `POST /categories`: Crear categoría.
- `PUT /categories/{id}`: Actualizar categoría.
- `DELETE /categories/{id}`: Eliminar categoría.

### Productos
- `GET /products`: Listar productos.
- `POST /products`: Crear producto.
- `PUT /products/{id}`: Actualizar producto.
- `DELETE /products/{id}`: Eliminar producto.

### Clientes
- `GET /clients`: Listar clientes.
- `POST /clients`: Crear cliente.
- `PUT /clients/{id}`: Actualizar cliente.
- `DELETE /clients/{id}`: Eliminar cliente.

### Proveedores
- `GET /suppliers`: Listar proveedores.
- `POST /suppliers`: Crear proveedor.
- `PUT /suppliers/{id}`: Actualizar proveedor.
- `DELETE /suppliers/{id}`: Eliminar proveedor.

### Ventas
- `GET /sales`: Listar ventas.
- `POST /sales`: Crear venta.
- `GET /sales/{id}`: Obtener venta por ID.
- `GET /sales/report`: Generar reporte de ventas (PDF).

### Compras
- `GET /purchases`: Listar compras.
- `POST /purchases`: Crear compra.
- `GET /purchases/{id}`: Obtener compra por ID.
- `GET /purchases/report`: Generar reporte de compras (PDF).

### Reportes
- `GET /products/report`: Reporte de productos.
- `GET /sales/ticket/{id}`: Generar ticket de venta.

Todos los endpoints requieren autenticación con token JWT en el header `Authorization: Bearer <token>`.

## Base de Datos

El esquema de la base de datos se define en `src/main/resources/schema.sql`. Las entidades principales incluyen:

- `User`: Usuarios del sistema.
- `Role`: Roles con permisos.
- `Permission`: Permisos asignados a roles.
- `Category`: Categorías de productos.
- `Product`: Productos en inventario.
- `Client`: Clientes.
- `Supplier`: Proveedores.
- `ProductSale` / `ProductSaleItem`: Ventas y sus ítems.
- `ProductPurchase` / `ProductPurchaseItem`: Compras y sus ítems.
- `Log`: Registros de auditoría.

## Reportes

Los reportes se generan con JasperReports. Los archivos `.jrxml` están en `src/main/resources/reports/`. Incluyen:

- `products.jrxml`: Reporte de productos.
- `sales.jrxml`: Reporte de ventas.
- `purchases.jrxml`: Reporte de compras.
- `ticket.jrxml`: Ticket de venta.
- `barcode.jrxml`: Código de barras.

## Pruebas

Ejecuta las pruebas con Maven:
```bash
mvn test
```

## Contribución

1. Haz un fork del proyecto.
2. Crea una rama para tu feature (`git checkout -b feature/nueva-funcionalidad`).
3. Commit tus cambios (`git commit -am 'Agrega nueva funcionalidad'`).
4. Push a la rama (`git push origin feature/nueva-funcionalidad`).
5. Abre un Pull Request.

## Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo `LICENSE` para más detalles.

## Contacto

Para preguntas o soporte, contacta al desarrollador: [milciadesferreiradev](https://github.com/milciadesferreiradev).</content>
<parameter name="filePath">/workspaces/backend_pdv/README.md