PARA REALIZAR ESTE TP:
Debemos descargar Minikube y el driver Docker
Link: https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download
Debemos descargar Kubectl que es la herramienta que nos permite comunicarnos con Kubernetes mediante lineas de código Link: https://kubernetes.io/docs/tasks/tools/
Ademas de descargar GIT para poder descargar los repos Link: https://git-scm.com/downloads

Luego de haber descargado todo lo que debemos hacer es crear una carpeta dentro de nuestra maquina y desde la terminal movernos con cd hacia ella.

Ya dentro de esta debemos realizar:
git init
git clone https://github.com/IgnacioSaAn/manifiestosTD5.git
git clone https://github.com/IgnacioSaAn/static-website2.git

////////////////////////////////////////////////////////////////////////////////////////////////

Luego de clonar los repos dentro del directorio nuevo lo que debemos hace es levantar lo que vendria siendo minikube, nos volvemos al directorio principal y realizamos el siguiente script

minikube start --mount --mount-string="/home/inachi/TD5D/static-website:/mnt/web"
#El primer directorio debe ser el directorio en el que se encuentre tu carpeta con el HTML

Luego de levantar la maquina lo unico que nos queda es aplicar nuestros manifiestos por lo que deberemos hacer cd hasta la carpeta donde se encuentran los mismo.

Ya dentro de la misma debemos poner: "kubectl apply -f ." 

Despues de eso nuestro pod ya debería estar levantandose, podemos ver el estado del mismo haciendo kubectl get pods: el nombre será: static-site-XXX-XXX.El estado de este será pending, ContainerCreating y por último Running.

Cuando este mismo ya este en running podremos levantar el servicio con nuestro html haciendo el siguiente script:

minikube service static-site-service
#Se nos abrirá una ventana en el navegador con nuestra página

¡¡FELICIDADES LEVANTASTE TU PRIMER SERVICIO CON KUBERNETES!!

SI QUERES SUMARLE UN PLUS DE AGREGARLE FUNCIONALIDAD AL ARCHIVO INGRESS HACE ESTO:

minikube addons enable ingress (es normal que tarde)

Ya habilito el addon, nos sigue conseguir la ip de minikube: "minikube ip"

luego nos queda decirle a la maquina que no solo se va a poder acceder desde el puesto, sino tambien por un url propio:
echo "$(resultado de minikube ip) local.service" | sudo tee -a /etc/hosts
Si no te funciona este comando podes probar sacandole el signo $ y los parentesis
echo "resultado de minikube ip local.service" | sudo tee -a /etc/hosts

si queres probar si funciona pone en el buscador lo siguiente: http://local.service/

¡¡FELICIDADES LEVANTASTE TU PRIMER SERVICIO CON KUBERNETES Y UN INGRESS!!
