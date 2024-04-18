# continuous-deployment-azure

En primer lugar, nos logueamos en el cliente de Azure (el login se realizará con ayuda del navegador) 
```
az login
```

Creamos un grupo de recursos `ais-group`
```
az group create --name ais-group --location westeurope
```

Creamos nuestra aplicación lanzando un contenedor a partir de la imagen `maes95/anuncios:v1`. Le pondremos a la aplicación el nombre `ais-anuncios`

```
az container create \
    --resource-group ais-group \
    --name ais-anuncios \
    --image maes95/anuncios:v1 \
    --dns-name-label ais-anuncios \
    --ports 8080
```

La URL dónde podremos acceder a la aplicación será: anuncios.westeurope.azurecontainer.io:8080

Podemos ver el estado de nuestra aplicación con el siguiente comando
```
az container show  \
    --resource-group ais-group \
    --name ais-anuncios \
    --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" \
    --out table
```

