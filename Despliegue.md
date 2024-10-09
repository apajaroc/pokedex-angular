


> Written with [StackEdit](https://stackedit.io/).
## Explicación del Despliegue
El despliegue se hace por medio de Azure y Github, permitiendonos actualizar la aplicación automáticamente cada vez que se envía código al repositorio de Github en la rama **main**.

Para ello se hace uno de uno de los servicios de Azure llamado Aplicación Web Estática siguiendo los pasos del tutorial mostrado [aquí](https://learn.microsoft.com/es-es/azure/static-web-apps/deploy-angular?pivots=github).
Es muy sencillo, es cuestión de: 

 - Seleccionar el servicio de aplicación web estática.
 - Darle nombre a la aplicación
 - Seleccionar si deseamos que sea gratuita o estándar (**Para mayor velocidad de despliegue seleccionaremos estándard**)
 - Conectar la cuenta de Github si es la primera vez, escoger el repositorio y la rama.

>Claramente los pasos anteriores requieren que el repositorio ya esté listo con el código. En este caso no se utilizó comandos de Git, sino la funcionalidad del editor de código Visual Studio Code para usar Git facilmente.

Habiendo completado los anteriores pasos, la aplicación ya estaría en la nube y accesible desde un link público, sin embargo no aparecen las imágenes de los pokemons, y la calificación de los encabezados de seguridad son bajos.

- Para corregir los encabezados, se agrega el archivo **staticwebapp.config.json** en el directorio raiz de la aplicación:

    {
    
    	"routes": [
    
			{
    
			    "route": "/*",
    
				    "headers": {
    
						    "strict-transport-security": "max-age=31536000; includeSubDomains; preload",
    
						    "referrer-policy": "no-referrer",
    
						    "x-content-type-options": "nosniff",
    
						    "x-frame-options": "DENY",
    
							"permissions-policy": "geolocation=(), microphone=(), camera=()"
    
			    }
    
		    }
    
	    ]
    
    }


- Para corregir las imágenes de los pokemons en la pantalla principal, se debe corregir la ruta de las imagenes en el archivo **src\environments\environment.prod.ts** de **pokedex-angular/assets/images** a **/assets/images**.

Listo!
    

