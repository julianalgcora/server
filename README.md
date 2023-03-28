# Serviço de Descoberta - Service discovery e registry

Vamos supor que temos diversos serviços espalhados de forma dinâmica na rede, cada um operando em um IP com uma porta 
diferente.
Como fazemos para descobrir onde está cada serviço? Na aplicação front-end não é uma boa prática ter que saber todos 
esses endereços para fazer as requisições para ela. Nem o próprio back-end quando for se comunicar com outro 
microsserviço ter essa complexidade de ficar procurando em qual porta ou IP aquele serviço, ou instância está operando.

Para isso usamos um ponto-chave da arquitetura de microsserviços, o Service Discovery (Serviço de descoberta). 
Ele é um tipo de catálogo que vai conter o endereço de todas as instâncias e microsserviços que estiverem registrados 
nele.

O Eureka da Netflix é uma implementação de um servidor de descoberta e a integração é fornecida pelo Spring Boot. Usando 
o Spring Boot, podemos construir um servidor de descoberta Eureka e registrar nossos microsserviços nele.
Para criarmos o primeiro servidor para fazer o service discovery vamos usar o Eureka Server na versão 3.1.4.

O Eureka Server foi desenvolvido pela Netflix e faz parte do pacote Spring Cloud Netflix. Primeiro a Netflix 
desenvolveu para uso próprio, depois disponibilizou para a comunidade como open source (ou em português, código aberto).

### Para iniciar o serviço de registro e descoberta com Eureka como servidor, seguir os seguintes passos:
1) Adicionar a dependência do Spring Cloud Eureka Server ao seu arquivo pom.xml.
2) Configurar o arquivo `application.properties` com as informações de configuração para o servidor Eureka:
* A porta em que ele será executado. O padrão é subir na porta 8761, mais será alterado para subir na 8081.
`server.port=8081`
* Definir o nome da aplicação
`spring.application.name=server`
* A primeira configuração é utilizada para definir se o cliente Eureka irá se registrar automaticamente no servidor 
Eureka após o início e a segunda configuração é utilizada para definir se o cliente Eureka irá buscar informações do 
registro de serviços do servidor Eureka. Dado que o uso da aplicação vai ser exclusivo como servidor.
`eureka.client.register-with-eureka=false`
`eureka.client.fetch-registry=false`
* Esta configuração é usada para definir a URL do servidor Eureka. O cliente Eureka usará essa URL para se conectar ao 
servidor Eureka e registrar ou descobrir serviços.
eureka.client.serviceUrl.defaultZone=http://localhost:8081/eureka`
3) Anotar a classe principal da sua aplicação com a anotação `@EnableEurekaServer`
4) Acessar a página http://localhost:8081 no navegador para verificar se o servidor Eureka está em execução. 
Você deve ver a interface do usuário do Eureka, que mostra informações sobre os serviços registrados e as instâncias 
5) Configurar e iniciar outros serviços para se registrarem no servidor Eureka. Para que seus serviços possam ser 
descobertos pelo servidor Eureka, eles precisam se registrar no servidor usando o cliente do Eureka. Isso pode ser feito 
configurando as dependências e as informações de configuração apropriadas nos arquivos de configuração da aplicação e 
6) Verificar o registro e a descoberta de serviços. Depois que seus serviços estiverem registrados no servidor Eureka, 
você pode usar a interface do usuário do Eureka para verificar se eles estão listados corretamente. Você também pode usar 
o cliente do Eureka para acessar informações sobre outros serviços registrados, permitindo que seus serviços se 
comuniquem de forma dinâmica.


### Documentação de referência

* [Eureka Server](https://docs.spring.io/spring-cloud-netflix/docs/current/reference/html/#spring-cloud-eureka-server)
* [Service Registration and Discovery with Eureka and Spring Cloud](https://spring.io/guides/gs/service-registration-and-discovery/)

