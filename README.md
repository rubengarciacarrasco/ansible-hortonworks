# Despliegue de cluster HortonWorks con ansible

Este repositorio contiene los ficheros necesarios para desplegar en un entorno Openstack, un cluster de Hortonworks desde cero.

Orden de ejecución:

* infrastructure.yml, que ejecuta:
	* create_infrastructure.yml: Crea las redes, subredes, routers y grupos de seguridad
	* create_instances.yml: Crea las instancias del clúster
* platform.yml, que aplica los roles:
	* ambari:
		* Despliega ambari Agents en todos los nodos del cluster
		* Despliega ambari server
		* Configura ambari server (configuración por defecto)
		* Levanta ambari server en el puerto 8080
	* blueprint:
		* comprueba que los nodos están registrados en ambari server (a través de la API de ambari)
		* Despliega en ambari server el blueprint con la configuración de los componentes del cluster, calculado en base al número de DATANODES que se han desplegado
		* Verifica que el blueprint se ha subido y validado
		* Despliega el fichero de cluster que indica a qué máquinas se despliegan los componentes definidos en el fichero de blueprint (y su configuración)

La configuración del repositorio permite hacer un despliegue completo, sólo modificar el fichero config.yml.template en un config.yml y en los ficheros create_*.yml para indicar el flavor y los rangos de red que se quieran usar.