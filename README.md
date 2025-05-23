package in.ashokit.repo;

import org.springframework.data.jpa.repository.JpaRepository;

import in.ashokit.entity.Passport;

public interface PassportRepo extends JpaRepository<Passport, Integer>{

}
package in.ashokit.repo;

import org.springframework.data.jpa.repository.JpaRepository;

import in.ashokit.entity.Person;

public interface PersonRepo extends JpaRepository<Person, Integer>{

}
package in.ashokit.service;

import java.time.LocalDate;

import org.springframework.beans.factory.annotation.Autowired;

import in.ashokit.entity.Passport;
import in.ashokit.entity.Person;
import in.ashokit.repo.PassportRepo;
import in.ashokit.repo.PersonRepo;

public class PersonService {

	@Autowired
	private PersonRepo personRepo;

	@Autowired
	private PassportRepo passportRepo;

	public void savePersonWithPassport() {

		Passport passport = new Passport();
		passport.setPassportNum("K8HKHK6");
		passport.setIssuedDate(LocalDate.now());
		passport.setExpDate(LocalDate.now().plusYears(10));

		Person person = new Person();
		person.setPersonName("John");
		person.setDob(LocalDate.now().minusYears(20));

		passport.setPerson(person);
		person.setPassport(passport);

		personRepo.save(person);
	}

	public void deletePerson(int id) {
		personRepo.deleteById(id);
	}

	public void getPerson(int id) {
		personRepo.findById(id);
	}

	public void getPassport(int id) {
		passportRepo.findById(id);
	}

	public void deletePassport(int id) {
		passportRepo.deleteById(id);
	}
}
package in.ashokit;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;

import in.ashokit.service.PersonService;

@SpringBootApplication
public class Application {

	public static void main(String[] args) {
		ConfigurableApplicationContext context = SpringApplication.run(Application.class, args);

		PersonService personService = context.getBean(PersonService.class);

		// personService.savePersonWithPassport();
		// personService.getPerson(1);
		// personService.deletePerson(1);

		// personService.getPassport(1);
		// personService.deletePassport(1);

	}
}
spring:
  datasource:
    username: Manoj
    password: Manoj@853
    url: jdbc:mysql://localhost:3306/jrtp22
    driver-class-name: com.mysql.jdbc.Driver
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
