# Subtaller 1: Crear cuenta AWS y usar S3 con la Capa Gratuita

## Objetivo
Crear una cuenta de AWS, activar la capa gratuita (Free Tier) y realizar operaciones básicas con Amazon S3 (Simple Storage Service).

---

## Parte 1: Crear una cuenta de AWS

### Paso 1 — Ir al portal de registro
1. Abre tu navegador y ve a: **https://aws.amazon.com**
2. Haz clic en **"Create an AWS Account"** (esquina superior derecha).

### Paso 2 — Ingresar datos de la cuenta raíz
1. Escribe tu **dirección de correo electrónico** (será el usuario raíz).
2. Elige un **nombre para tu cuenta** (ej: `mi-cuenta-lab`).
3. Haz clic en **"Verify email address"**.
4. Revisa tu correo y copia el **código de verificación** de 6 dígitos.
5. Ingrésalo en la pantalla y haz clic en **"Verify"**.

### Paso 3 — Crear contraseña
1. Escribe una contraseña segura (mínimo 8 caracteres, mezcla mayúsculas, números y símbolos).
2. Confirma la contraseña y haz clic en **"Continue"**.

### Paso 4 — Información de contacto
1. Selecciona **"Personal"** (para uso educativo/personal).
2. Rellena los campos: nombre, número de teléfono, país, dirección, ciudad, estado y código postal.
3. Acepta el **AWS Customer Agreement**.
4. Haz clic en **"Continue"**.

### Paso 5 — Información de pago
> AWS requiere una tarjeta de crédito o débito, pero **no te cobrará** mientras uses solo los servicios del Free Tier.

1. Ingresa los datos de tu tarjeta (número, fecha de vencimiento, CVV).
2. AWS realizará un **cobro temporal de USD $1** para verificar la tarjeta (se revierte en 3-5 días).
3. Haz clic en **"Verify and Continue"**.

### Paso 6 — Verificación de identidad por teléfono
1. Selecciona tu país y escribe tu número de teléfono.
2. Elige verificación por **SMS** o **llamada de voz**.
3. Ingresa el código de 4 dígitos recibido.
4. Haz clic en **"Continue"**.

### Paso 7 — Seleccionar plan de soporte
1. Elige **"Basic support - Free"** (es suficiente para laboratorios).
2. Haz clic en **"Complete sign up"**.

### Paso 8 — Activación de la cuenta
- AWS envía un correo de confirmación.
- La activación puede tardar **hasta 24 horas**, aunque normalmente es inmediata.
- Cuando llegue el correo de bienvenida, tu cuenta está lista.

---

## Parte 2: Primeros pasos — Configurar seguridad básica

### Paso 9 — Habilitar MFA en el usuario raíz
1. Inicia sesión en **https://console.aws.amazon.com** con tu correo y contraseña.
2. Haz clic en tu nombre (esquina superior derecha) > **"Security credentials"**.
3. En la sección **"Multi-factor authentication (MFA)"** > **"Assign MFA device"**.
4. Elige **"Authenticator app"** y sigue el asistente con una app como Google Authenticator o Authy.

### Paso 10 — Crear un usuario IAM para el trabajo diario
> Nunca uses el usuario raíz para actividades cotidianas.

1. Ve a **IAM** (busca "IAM" en la barra de servicios).
2. Haz clic en **"Users"** > **"Create user"**.
3. Nombre de usuario: `lab-user`
4. Marca **"Provide user access to the AWS Management Console"**.
5. Selecciona **"I want to create an IAM user"**.
6. Haz clic en **"Next"**.
7. En permisos, elige **"Attach policies directly"** y busca:
   - `AmazonS3FullAccess`
8. Haz clic en **"Next"** > **"Create user"**.
9. Descarga o copia las **credenciales** (contraseña de consola).

---

## Parte 3: Usar Amazon S3 con la Capa Gratuita

### ¿Qué incluye el Free Tier de S3?
| Recurso | Límite mensual gratuito |
|---|---|
| Almacenamiento | 5 GB |
| Solicitudes GET | 20,000 |
| Solicitudes PUT/COPY/POST | 2,000 |
| Transferencia de datos saliente | 100 GB |

> El Free Tier dura **12 meses** desde la creación de la cuenta.

---

### Paso 11 — Crear un bucket S3
1. Inicia sesión como `lab-user`.
2. En la barra de búsqueda escribe **"S3"** y selecciónalo.
3. Haz clic en **"Create bucket"**.
4. **Nombre del bucket**: debe ser único globalmente. Ejemplo: `mi-bucket-lab-2024-tuapellido`
5. **Región**: selecciona `us-east-1` (N. Virginia) — tiene la cobertura más amplia de servicios gratuitos.
6. En **"Block Public Access"**: deja todas las opciones marcadas (recomendado).
7. Deja las demás opciones por defecto.
8. Haz clic en **"Create bucket"**.

### Paso 12 — Subir un archivo al bucket
1. Haz clic en el nombre de tu bucket recién creado.
2. Haz clic en **"Upload"**.
3. Arrastra un archivo de prueba (ej: un `.txt` o `.csv`).
4. Haz clic en **"Upload"** (parte inferior).
5. Verás el archivo listado en el bucket con su nombre, tamaño y fecha.

### Paso 13 — Organizar con "carpetas" (prefijos)
En S3 no existen carpetas reales, pero se usan prefijos para organizar:

1. Haz clic en **"Create folder"**.
2. Nombre: `raw/`
3. Repite para crear: `processed/` y `output/`
4. Sube archivos dentro de cada "carpeta" usando la misma interfaz de upload.

### Paso 14 — Descargar un archivo desde S3
1. Haz clic en el archivo dentro del bucket.
2. Haz clic en **"Download"** (esquina superior derecha del detalle del objeto).

### Paso 15 — Hacer un objeto públicamente accesible (opcional)
> Solo hazlo con archivos que quieras compartir públicamente.

1. Ve a tu bucket > **"Permissions"** > desactiva **"Block all public access"** (confirma).
2. Selecciona el archivo > **"Actions"** > **"Make public via ACL"**.
3. Copia la URL del objeto para compartirlo.

### Paso 16 — Generar una URL pre-firmada (acceso temporal)
1. Selecciona el archivo.
2. **"Actions"** > **"Share with a presigned URL"**.
3. Define el tiempo de expiración (ej: 1 hora).
4. Copia y comparte la URL — expirará automáticamente.

### Paso 17 — Eliminar objetos y el bucket
> Para evitar costos inesperados, elimina recursos que no uses.

1. Selecciona todos los objetos > **"Delete"** > escribe `permanently delete` > confirma.
2. Regresa a la lista de buckets.
3. Selecciona el bucket > **"Delete"** > escribe el nombre del bucket > confirma.

---

## Parte 4: Acceder a S3 desde la terminal (AWS CLI)

### Paso 18 — Instalar AWS CLI
```bash
# macOS
brew install awscli

# Verificar instalación
aws --version
```

### Paso 19 — Configurar credenciales
1. En IAM, ve a tu usuario `lab-user` > **"Security credentials"** > **"Create access key"**.
2. Selecciona **"Command Line Interface (CLI)"** > acepta la advertencia > **"Next"** > **"Create access key"**.
3. Descarga el `.csv` con **Access Key ID** y **Secret Access Key**.

```bash
aws configure
# AWS Access Key ID: AKIA...
# AWS Secret Access Key: tu_secret_key
# Default region name: us-east-1
# Default output format: json
```

### Paso 20 — Operaciones básicas con AWS CLI
```bash
# Listar buckets
aws s3 ls

# Crear bucket
aws s3 mb s3://mi-bucket-cli-lab

# Subir archivo
aws s3 cp archivo_local.csv s3://mi-bucket-cli-lab/raw/archivo_local.csv

# Listar contenido del bucket
aws s3 ls s3://mi-bucket-cli-lab/

# Descargar archivo
aws s3 cp s3://mi-bucket-cli-lab/raw/archivo_local.csv ./descargado.csv

# Sincronizar carpeta local con S3
aws s3 sync ./datos_locales/ s3://mi-bucket-cli-lab/datos/

# Eliminar objeto
aws s3 rm s3://mi-bucket-cli-lab/raw/archivo_local.csv

# Eliminar bucket (debe estar vacío)
aws s3 rb s3://mi-bucket-cli-lab
```

---

## Parte 5: Monitorear el uso del Free Tier

### Paso 21 — Configurar alertas de facturación
1. Ve a **"Billing and Cost Management"** (busca "Billing" en la barra).
2. Haz clic en **"Budgets"** > **"Create budget"**.
3. Tipo: **"Zero spend budget"** — te avisa si hay cualquier gasto.
4. Ingresa tu correo y crea el presupuesto.

### Paso 22 — Revisar uso del Free Tier
1. Ve a **"Billing"** > **"Free Tier"**.
2. Verás el consumo actual vs. el límite para cada servicio.

---

## Resumen de buenas prácticas
- Nunca compartas tus **Access Keys** en código subido a GitHub.
- Usa **variables de entorno** o **AWS Secrets Manager** para manejar credenciales.
- Elimina recursos no utilizados para evitar cargos inesperados.
- Habilita **S3 Versioning** si necesitas histórico de archivos.
- Usa **S3 Lifecycle Policies** para archivar o eliminar objetos automáticamente.
