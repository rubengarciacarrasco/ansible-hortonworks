# Despliegue de cluster HortonWorks con ansible

Este repositorio contiene los ficheros necesarios para desplegar en un entorno Openstack, un cluster de Hortonworks desde cero.

Orden de ejecución:

* infrastructure.yml, que ejecuta:
	* create_infrastructure.yml: Crea las redes, subredes, routers y groups de seguridad
	* create_instances.yml: Crea las instancias del clúster
* platform.yml, que aplica los roles:
	* ambari:
		* Despliega ambari Agents en todos los nodos del cluster
		* Despliega ambari server
		* Configura ambari server
		* Levanta ambari server
	* blueprint:
		* comprueba que los nodos están registrados en ambari server
		* Instala en ambari server el blueprint con la configuración del cluster
		* Verifica el blueprint
		* Despliega el fichero de cluster que se une al fichero de blueprint y despliega los componentes del cluster en todos los nodos
