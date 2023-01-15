Spring cloud Bus Refresh Event in spring cloud config server client :

 First we need to install kafka server in system with the help of below link:

 	https://kafka.apache.org/quickstart

 Setup spring cloud server and client with below wiki

 	https://soshace.com/spring-cloud-config-refresh-strategies/
 	https://soshace.com/centralize-the-configuration-of-services-with-spring-cloud-config/

 Create github repository for maintaining the application profiles at center place.


  repository structure:
  			reponame:
  				<applicaiton>-<profile>.properties

Spring cloud server:
	
	Whenever updating any value in profiles we can update the properties in each client without restarting the client applications, below are the 3 ways we can do

		1) Calling /actuator/refresh event at each client application
		2) By calling the /actuator/bus-refresh endpoint exposed on the config client integrated with Spring Cloud Bus.
		3) By calling the /monitor endpoint exposed on the config server integrated with Spring Cloud Bus

Working structure:

	whenever we are updating using second point, below are the events will generated in the follwing order.
	1) RefreshRemoteApplicationEvent - RefreshRemoteApplicationEvent is catched before refreshment of environment. So here the old value of property is printed.
	2) EnvironmentChangeEvent - If you use the local varible you will get the old value and if you fetch from the env type of Environment class, you will get the new value
	3) RefreshScopeRefreshedEvent - This event will be like finally in refresh bus concept.


Spring cloud Server code github repo: 

	curl --location --request POST 'http://localhost:9090/actuator/busrefresh'
	curl --location --request POST 'http://localhost:9090/actuator/refresh'

		
Client Repositories:

	https://github.com/NithishReddy/springclienttwo
	https://github.com/NithishReddy/springclientone

SpringProfiles:

	https://github.com/NithishReddy/springprofiles





