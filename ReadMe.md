Camel Spring Boot Project simple-test
===========================

To build this project use

    mvn install

To run this project with Maven use

    mvn spring-boot:run

For more help see the Apache Camel documentation

    http://camel.apache.org/


For testing

    curl http://localhost:8090/camel/api-docs
    curl http://localhost:8090/camel/ping

Acces Swagger UI with definition

    http://localhost:8090/webjars/swagger-ui/2.1.0/index.html?url=/camel/api-docs

    curl http://localhost:8090/camel/restsvc/ping


To deploy on Openshift, make sure you are connected to your Openshift instance and project with the oc command.

    mvn -P ocp fabric8:deploy




## Changes requried if import images from registry.redhat.io


Create secret:

		oc create secret generic redhatio-token  --from-file=.dockerconfigjson=$HOME/.docker/config.json --type=kubernetes.io/dockerconfigjson


		oc secrets link builder  redhatio-token
		
		oc secrets link default redhatio-token --for=pull



import images from redhat.io


		oc import-image fuse-test/fuse-java-openshift --from=registry.redhat.io/fuse7/fuse-java-openshift --confirm --loglevel=7


tag if needed:
	

		oc tag  fuse-test/fuse-java-openshift:latest  fuse-test/fuse-java-openshift:1.3


	

deploy with command:


		mvn -P ocp fabric8:deploy -Dfabric8.generator.from=fuse-test/fuse-java-openshift:1.3






