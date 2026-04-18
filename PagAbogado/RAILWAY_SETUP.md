# 🚀 Instrucciones para Desplegar en Railway

## Variables de Entorno Necesarias

Configura estas variables en el panel de Railway (Settings → Variables):

```
SECRET_KEY=n6^zpn-%dce+rd0b^a=*vm_ym^x5^rey%fj4f@s)y*e_()4m3*
DEBUG=False
ALLOWED_HOSTS=tudominio.railway.app,localhost
DATABASE_URL=<Generado automáticamente por Railway>
CSRF_TRUSTED_ORIGINS=https://tudominio.railway.app
```

### Pasos:

1. **Crea un nuevo Proyecto en Railway**
   - Accede a https://railway.app
   - Click en "New Project"
   - Conecta tu repositorio GitHub

2. **Agrega Base de Datos PostgreSQL**
   - En Railway: "+ Add Service" → PostgreSQL
   - Esto genera automáticamente `DATABASE_URL`

3. **Configura Variables de Entorno**
   - Copia cada variable del archivo `.env.example`
   - Reemplaza los valores según tu dominio
   - **Usa el SECRET_KEY proporcionado arriba**

4. **Configura el Build Command (Opcional)**
   - Railway automáticamente detecta Django
   - Si es necesario: `python manage.py collectstatic --noinput`

5. **Configura el Start Command**
   - Railway usa el `Procfile` automáticamente:
     ```
     web: gunicorn prueba.wsgi
     release: python manage.py migrate
     ```

6. **Deploy**
   - Haz push a GitHub desde tu rama principal
   - Railway automáticamente hace deploy

### Variables Importantes Explicadas:

| Variable | Valor Ejemplo | Descripción |
|----------|---------------|-------------|
| `SECRET_KEY` | `n6^zpn-%dce+rd0b^a=*vm_ym^x5^rey%fj4f@s)y*e_()4m3*` | Clave de seguridad de Django (ya generada) |
| `DEBUG` | `False` | **NUNCA** usar `True` en producción |
| `ALLOWED_HOSTS` | `miapp.railway.app,localhost` | Reemplaza con tu dominio real |
| `DATABASE_URL` | Generado por Railway | PostgreSQL automático |
| `CSRF_TRUSTED_ORIGINS` | `https://miapp.railway.app` | HTTPS de tu dominio |

### Verificar que Funciona:

Una vez deployado, verifica:
```bash
curl https://tudominio.railway.app
```

Deberías ver tu página de inicio.

### Troubleshooting:

Si ves errores 500:
1. Revisa los logs en Railway → "View Logs"
2. Verifica que `DATABASE_URL` esté configurada correctamente
3. Ejecuta `python manage.py migrate` (lo hace automáticamente el release task)

Si ves errores de CSRF:
- Actualiza `CSRF_TRUSTED_ORIGINS` con tu dominio real

Si ves "DisallowedHost":
- Actualiza `ALLOWED_HOSTS` con tu dominio real

---

**Archivo actualizado:** 18 de abril de 2026
