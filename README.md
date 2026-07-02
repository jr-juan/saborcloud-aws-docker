# SaborCloud — Entorno Local con Docker Compose

Entorno de base de datos local para la empresa **SaborCloud S.A.S**, 
replicando la infraestructura desplegada en AWS EC2. Incluye PostgreSQL 18 
como motor de base de datos y pgAdmin 4 como herramienta de administración 
gráfica, orquestados con Docker Compose.

---

## Tecnologías usadas

- Docker Desktop
- Docker Compose
- PostgreSQL 18
- pgAdmin 4

---

##  Estructura del proyecto

```
pg-stack/
├── pgdata/              # Volumen de datos (ignorado en git)
├── docker-compose.yml   # Orquestación de servicios
├── comando.md           # Comandos útiles
└── saborcloud.sql       # Script de la base de datos
```

---

##  Cómo levantar el entorno

**1. Clonar el repositorio**
```bash
git clone https://github.com/jr-juan/saborcloud-aws-docker.git
cd saborcloud-aws-docker/pg-stack
```

**2. Levantar los servicios**
```bash
docker compose up -d
```

**3. Verificar que estén corriendo**
```bash
docker compose ps
```

**4. Restaurar la base de datos**
```bash
docker exec -i postgres-saborcloud psql -U postgres -d saborcloud < saborcloud.sql
```

---

##  Acceso a pgAdmin

Abre en el navegador: `http://localhost:8080`

Las credenciales de acceso se configuran en las variables de entorno
del archivo `docker-compose.yml`.

---

##  Conexión al servidor en pgAdmin

Al registrar el servidor usa:

| Campo    | Valor      |
|----------|------------|
| Host     | `postgres` |
| Port     | `5432`     |
| Database | `postgres` |

Las credenciales se definen en las variables `POSTGRES_USER` y
`POSTGRES_PASSWORD` del `docker-compose.yml`.

---

##  Base de datos

La base de datos `saborcloud` contiene el modelo relacional completo
para la gestión de pedidos del restaurante:

| Tabla          | Registros |
|----------------|-----------|
| roles          | 1000      |
| empleados      | 1000      |
| clientes       | 1000      |
| mesas          | 1000      |
| categorias     | 1000      |
| productos      | 1000      |
| pedidos        | 1000      |
| detalle_pedido | 1000      |
| pagos          | 1000      |

---

##  Detener el entorno

```bash
docker compose down
```

---

##  Autor

**Juan Roman Cuero Ordoñez**  
Ingeniería de Sistemas — Universidad del Pacífico  
Electiva Profesional III — 2026