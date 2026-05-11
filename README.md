# Análisis de Mercado y Selección:

La propuesta será del CRM Zoho One, a continuación las razones:
<img width="500" height="200" alt="image" src="https://github.com/user-attachments/assets/9ddd35c9-80b2-4b0a-abd9-114668992fb3" />

1. (25 empleados, presupuesto ajustado, necesidad de personalización en el etiquetado).  
     
   \-Ideal para empresas pequeñas y medianas al ser simple, claro y eficiente trabajando con las cuentas aunque hay empresas grandes como Netflix que la usan  
   \-Permite centralizar todas las herramientas necesarias para el negocio y ofrece 50 aplicaciones diferentes sin coste extra.  
   \-Tanto la inversión inicial es baja comparado con otros CRM y como a largo plazo ya que   
   \-Usa una interfaz alojada en la nube fácil de acceder.  
   \-En caso de crecer la empresa ofrece una gran escalabilidad.  
   \-Para la solicitud de etiquetas personalizadas, Zoho One cuenta con esta funcionalidad.   
   \- Su rango de precios es de 0€/mes, 14/mes, 40/mes y 60/mes. En este caso se recomienda el plan de medio de 37/mes ya que ofrece todo lo necesario(50+ aplicaciones, automatizacion, analiticas, soporte estandar).  
   \-Además es fácil de empezar para principiantes y tiene aplicación móvil,  
   \-No es necesario tener un equipo de IT pendiente para su uso.  
2. Cálculo de TCO:  
   \-Coste de suscripción es de 40/mes  
   \-El coste de implementación sería de una implementación inicial de 140h a 50€/h para la migración de datos y formación inicial.  
   \-No hace falta contratar un servicio de cloud al usar el propio de Zoho.  
   

# Diseño de Seguridad RBAC 

Hicimos la division de permiso en una sola tabla dividida en roles/sectores, manteniendo el Principio de Mínimo Privilegio para garantizar la seguridad al usuario. 
| Permisos | Clientes | Presupuesto | Stock | Albaranes entrada/salida | Factura | Administración |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| Administración | Permiso total | Permiso total | Permiso total | Permiso total | Permiso total | Permiso total |
| Comercial | Solo lectura  | Solo lectura | Sin acceso | Sin acceso | Lectura | Sin acceso |
| Operario de Almacén  | Sin acceso | Sin acceso | Lectura y modificar | Lectura | Sin acceso | Sin acceso |
| Contable | Lectura | Lectura | Solo lectura | Lectura | Lectura y puede modificarlo | Sin acceso |

# 

# Documentación de Explotación

Teniendo en cuenta la norma ISO/IEC 26514, y usando Zoho One \+ PostgreSQL.

```
 services:  
	postgres:  
		image: postgres: 16-alpine  
		container \_name: aljarafe\_db  
		restart:  unless-stopped
		depends on:  
			POSTGRES\_DB: aljarafe  
			  POSTGRES\_USER: aljarafe\_admin  
			  POSTGRES\_PASSWORD: ${DB\_PASSWORD}

			volumes:  
      \- pg\_data:/var/lib/postgresql/data  
      \- ./backups:/backups  
    ports:  
      \- "5432:5432"

volumes:  
  pg\_data:
```

Por qué lo elegí: con un solo archivo y un solo comando (docker compose up -d), cualquier técnico levanta el sistema idéntico en cualquier máquina. Si el servidor cae, recuperarlo son 30 segundos.

**comando para realizar un backup de la base de datos PostgreSQL.**
```
docker exec \-t aljarafe\_db pg\_dump \-U aljarafe\_admin \-d aljarafe \-F c \-f /backups/aljarafe\_$(date \+%Y%m%d).dump
```
## 

## Referencias 

\[1\] “Plantilla de matriz de permisos RBAC para gestión documental en pymes: [https://www.mafosan.com/blog/plantilla-de-matriz-de-permisos-rbac-para-gestion-documental-en-pymes-disena-accesos-por-rol-sin-frenar-la-colaboracion/](https://www.mafosan.com/blog/plantilla-de-matriz-de-permisos-rbac-para-gestion-documental-en-pymes-disena-accesos-por-rol-sin-frenar-la-colaboracion/)  
 (accessed May 11, 2026).

\[2\] “Zoho vs Odoo: ¿qué ERP elegir?”[https://www.appvizer.com/magazine/operations/erp/zoho-vs-odoo](https://www.appvizer.com/magazine/operations/erp/zoho-vs-odoo) (accessed May 11, 2026).

\[3\] “Etiquetas.” [https://help.zoho.com/portal/es/kb/projects/settings-in-zoho-projects/portal-configuration/articles/etiquetas\#Enable\_Tags](https://help.zoho.com/portal/es/kb/projects/settings-in-zoho-projects/portal-configuration/articles/etiquetas#Enable_Tags)  (accessed May 11, 2026).

