# Delivery Backend

Este es un backend desarrollado en Django REST Framework para un sistema de delivery de restaurantes. Incluye autenticación de usuarios, gestión de menú, carrito de compras, pedidos, pagos y notificaciones, con protección de autenticación mediante tokens JWT.

## Estructura del Proyecto

El proyecto está dividido en las siguientes aplicaciones:

- **users**: Gestión de autenticación y perfil de usuario.
- **menu**: Gestión de los platillos disponibles en el restaurante.
- **cart**: Manejo del carrito de compras.
- **orders**: Creación y gestión de pedidos.
- **payment**: Procesamiento de pagos.
- **notifications**: Notificaciones relacionadas con el estado de los pedidos.

## Requisitos

- Python 3.x
- Django 3.x o superior
- Django REST Framework
- PostgreSQL

## Instalación

1. Clona el repositorio y navega al directorio del proyecto:

    ```bash
    git clone https://yummiesdelivery@dev.azure.com/yummiesdelivery/Backend/_git/Backend
    cd delivery_backend
    ```

2. Instala las dependencias necesarias:

    ```bash
    pip install -r requirements.txt
    ```

3. Configura la base de datos PostgreSQL en el archivo `settings.py`:

    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': 'delivery',
            'USER': 'postgres',
            'PASSWORD': '123456',
            'HOST': '127.0.0.1',
            'PORT': '5432',
        }
    }
    ```

4. Ejecuta las migraciones para crear las tablas en la base de datos:

    ```bash
    python manage.py makemigrations
    python manage.py migrate
    ```

5. Crea un superusuario para acceder al panel de administración:

    ```bash
    python manage.py createsuperuser
    ```

6. Inicia el servidor de desarrollo:

    ```bash
    python manage.py runserver
    ```

## Uso

### Endpoints Principales

Los endpoints están agrupados en varias aplicaciones:

1. **Autenticación (`/api/users/`)**
    - `POST /signup`: Crear una nueva cuenta de usuario.
    - `POST /login`: Iniciar sesión y obtener un token de acceso.
    - `GET /profile`: Obtener el perfil del usuario autenticado.
    - `POST /logout`: Cerrar sesión.

2. **Menú (`/api/menu/`)**
    - `GET /menu`: Obtener la lista de platillos.
    - `GET /menu/popular`: Obtener platillos populares.
    - `GET /menu/favorites`: Obtener favoritos del usuario.
    - `POST /menu/favorites`: Añadir un platillo a favoritos.
    - `GET /menu/search`: Buscar platillos por nombre o categoría.

3. **Carrito (`/api/cart/`)**
    - `POST /cart`: Añadir un platillo al carrito.
    - `GET /cart`: Ver el contenido del carrito.
    - `DELETE /cart/{item_id}`: Eliminar un platillo del carrito.
    - `PUT /cart/{item_id}`: Actualizar la cantidad de un platillo en el carrito.

4. **Pedidos (`/api/orders/`)**
    - `POST /order`: Crear un nuevo pedido.
    - `GET /order/{order_id}`: Ver detalles de un pedido específico.
    - `GET /orders`: Listar todos los pedidos del usuario.

5. **Pagos (`/api/payment/`)**
    - `POST /payment`: Procesar el pago de un pedido.
    - `GET /payment/status`: Verificar el estado del pago.

6. **Notificaciones (`/api/notifications/`)**
    - `GET /order/{order_id}/status`: Obtener el estado actual de un pedido.
    - `POST /order/{order_id}/issue`: Reportar un problema con un pedido.

### Autenticación

Este proyecto utiliza JWT (JSON Web Token) para la autenticación de usuarios. Asegúrate de incluir el token en los encabezados de las solicitudes a endpoints protegidos:

