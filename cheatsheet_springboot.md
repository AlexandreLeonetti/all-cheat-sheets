# Spring Boot Cheat sheet.

rest api structure ?

* Controller
* Service
* Repository

package manager ?
 * maven

health check ?
 * Actuator

database ?
* Spring Data JPA ( Java Persistance API)
* H2 ( in memory db )

top commands ?
* ./mvnw spring-boot:run

main decorators ?

* @Entity
* @Table( name = "users")
* @Id
* @GeneratedValue(strategy = GenerationType.IDENTITY)
* @Service
* @RestController
* @RequestMapping("/users")
* @GetMapping
* @PostMapping


