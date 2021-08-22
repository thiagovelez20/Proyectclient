# Proyectclient
Este es el Proyecto realizado con SprinBoot, bases de Datos de PostgreSQL y utilizar el framework de Angular donde se debía crear un Crud para editar. eliminar, modificar y crear
Crear un Diagrama de entidad Realacionar
Localhost:8083 puerto utilizado en Backend en este caso seria Spring Boot
Localhost: 4200 para crear la interfaz Front End
Bases de Datos Postgesql: PhpAdmin4
Este es el Script de la bases de Datos: Table Tarjera Crédito.
-- Table: public.TarjetaDebito

-- DROP TABLE public."TarjetaDebito";

CREATE TABLE IF NOT EXISTS public."TarjetaDebito"
(
    "Id" numeric(2,0) NOT NULL,
    nameclient text COLLATE pg_catalog."default",
    "firstnameClient" text COLLATE pg_catalog."default",
    state "char",
    createdate date,
    CONSTRAINT "TarjetaDebito_pkey" PRIMARY KEY ("Id")
)
WITH (
    OIDS = FALSE
)
TABLESPACE pg_default;

ALTER TABLE public."TarjetaDebito"
    OWNER to postgres;
Este es el Script de la bases de Datos: Table Cliente
-- Table: public.client

-- DROP TABLE public.client;

CREATE TABLE IF NOT EXISTS public.client
(
    "Id" name NOT NULL,
    documentclient numeric(15,0),
    nameclient name,
    firtsname text COLLATE pg_catalog."default",
    ciudad text COLLATE pg_catalog."default",
    direction text COLLATE pg_catalog."default",
    "Age" numeric(2,0),
    cardvalue double precision,
    cardnumber numeric(25,0),
    CONSTRAINT client_pkey PRIMARY KEY ("Id")
)
WITH (
    OIDS = FALSE
)
TABLESPACE pg_default;

ALTER TABLE public.client
    OWNER to postgres;
    
 ---- SCritp de Spring Boot
 server.port=8084
spring.jpa.database=POSTGRESQL
spring.datasource.platform=postgres
spring.datasource.url=jdbc:postgresql://localhost:5432/db_cliente
spring.datasource.username=postgres
spring.datasource.password=Admin10
spring.jpa.show-sql=true
#spring.jpa.generate-ddl=true
#spring.jpa.hibernate.ddl-auto=create-drop
#spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true

Paquete Modelo:
package CarvajalBusiness.com.co.app.model;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;
import javax.xml.crypto.Data;

@Entity
@Table(name= "cardcredit")

public class CardCredit {
	@Id
	@GeneratedValue(strategy = GenerationType.AUTO)
	private Long id;
	
	// Creamos las propiedades que va tener la Base de Datos
	private String nameclient;
	private String  firtsname;
	private Data creadate;
	private String typesofcards;
	
	public CardCredit(Long id, String nameclient, String firtsname, Data creadate) {
		super();
		this.id = id;
		this.nameclient = nameclient;
		this.firtsname = firtsname;
		this.creadate = creadate;
		this.typesofcards= typesofcards;
	}
	public Long getId() {
		return id;
	}
	public void setId(Long id) {
		this.id = id;
	}
	public String getNameclient() {
		return nameclient;
	}
	public void setNameclient(String nameclient) {
		this.nameclient = nameclient;
	}
	public String getFirtsname() {
		return firtsname;
	}
	public void setFirtsname(String firtsname) {
		this.firtsname = firtsname;
	}
	public Data getCreadate() {
		return creadate;
	}
	public void setCreadate(Data creadate) {
		this.creadate = creadate;
	}
	public String getTypesofcards() {
		return typesofcards;
	}
	public void setTypesofcards(String typesofcards) {
		this.typesofcards = typesofcards;
	}
	
	}
--- Paquete Repositorio------

package CarvajalBusiness.com.co.app.model;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;
import javax.xml.crypto.Data;

@Entity
@Table(name= "cardcredit")

public class CardCredit {
	@Id
	@GeneratedValue(strategy = GenerationType.AUTO)
	private Long id;
	
	// Creamos las propiedades que va tener la Base de Datos
	private String nameclient;
	private String  firtsname;
	private Data creadate;
	private String typesofcards;
	
	public CardCredit(Long id, String nameclient, String firtsname, Data creadate) {
		super();
		this.id = id;
		this.nameclient = nameclient;
		this.firtsname = firtsname;
		this.creadate = creadate;
		this.typesofcards= typesofcards;
	}
	public Long getId() {
		return id;
	}
	public void setId(Long id) {
		this.id = id;
	}
	public String getNameclient() {
		return nameclient;
	}
	public void setNameclient(String nameclient) {
		this.nameclient = nameclient;
	}
	public String getFirtsname() {
		return firtsname;
	}
	public void setFirtsname(String firtsname) {
		this.firtsname = firtsname;
	}
	public Data getCreadate() {
		return creadate;
	}
	public void setCreadate(Data creadate) {
		this.creadate = creadate;
	}
	public String getTypesofcards() {
		return typesofcards;
	}
	public void setTypesofcards(String typesofcards) {
		this.typesofcards = typesofcards;
	}
	
}
---  Paquete Services----
package CarvajalBusiness.com.co.app.Repository.Services;

import java.util.List;
import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import CarvajalBusiness.com.co.app.Repository.ClientResopository;
import CarvajalBusiness.com.co.app.model.Client;

@Service
public class ClientServices {
	
	@Autowired
	private ClientResopository clientresopository;
	
	// Creamos los Cuatro Mètodos basicos que va Tener nuestro Crud
	
	// Metodo de Crear
	public Client create(Client client) {
		return clientresopository.save(client);
		
	}
	
	// Método Listar 
	
	public List<Client> getAllClient() {
		return clientresopository.findAll();
		
	}
	
	// Método para Eliminar
	
	public void delete(Client client) {
		 clientresopository.delete(client);
		
	}
	
	// Metodo para Editar
	public Optional<Client> findById(Long id) {
		return clientresopository.findById(id);
		
	}
		
}
 --- paquete Rest-----
package CarvajalBusiness.com.co.app.Rest;

import java.net.URI;
import java.util.List;
import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;



import CarvajalBusiness.com.co.app.Repository.Services.ClientServices;
import CarvajalBusiness.com.co.app.model.Client;

@RestController
@RequestMapping("/api/client/")

public class ClientRest {
	
	@Autowired
	private ClientServices clientservices;
	
	 // Creamos el PostMapping para guardar los Datos del cliente
	@PostMapping
	private ResponseEntity<Client> save (@RequestBody Client client){
		Client temporal = clientservices.create(client);
		
		try {
			
			return ResponseEntity.created(new URI("/api/client/"+temporal.getId())).body(temporal);
		}catch(Exception e) {
			return ResponseEntity.status(HttpStatus.BAD_REQUEST).build(); 
				
			}
		}
		
		// Creamos el GetMapping para Listar todos los clientes
		
		@GetMapping
		private ResponseEntity<List<Client>> listarclients() {
			
				return ResponseEntity.ok(clientservices.getAllClient());
		}
		
		// Creamos DeleteMapping para Eliminiar el cliente por medio de Mapeo 
		
		@DeleteMapping
		private ResponseEntity<Void> DeletClient(@RequestBody Client client){
			clientservices.delete(client);
			return ResponseEntity.ok().build();
			
		}
		
		// Creamos el GetMapping con Optional para Buscar los clientes
		
		@GetMapping (value= "{id}")
		private ResponseEntity<Optional<Client>> ListClientbyId(@PathVariable("id") Long id){
			return ResponseEntity.ok(clientservices.findById(id));
		}
		
	}
  
  --- Script de Angular---
  
<style>
  :host {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
    font-size: 14px;
    color: #333;
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    margin: 8px 0;
  }

  p {
    margin: 0;
  }

  .spacer {
    flex: 1;
  }

  .toolbar {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 60px;
    display: flex;
    align-items: center;
    background-color: #1976d2;
    color: white;
    font-weight: 600;
  }

  .toolbar img {
    margin: 0 16px;
  }

  .toolbar #twitter-logo {
    height: 40px;
    margin: 0 8px;
  }

  .toolbar #youtube-logo {
    height: 40px;
    margin: 0 16px;
  }

  .toolbar #twitter-logo:hover,
  .toolbar #youtube-logo:hover {
    opacity: 0.8;
  }

  .content {
    display: flex;
    margin: 82px auto 32px;
    padding: 0 16px;
    max-width: 960px;
    flex-direction: column;
    align-items: center;
  }

  footer {
    margin-top: 8px;
    display: flex;
    align-items: center;
    line-height: 20px;
  }

  footer a {
    display: flex;
    align-items: center;
  }
   body{
     background-color: rgb(201, 148, 79);
   }

  @media screen and (max-width: 575px) {
    svg#rocket-smoke {
      display: none;
      visibility: hidden;
    }
  }
</style>

<!-- Toolbar -->
<div class="toolbar" role="banner">
  <img
    width="40"
    alt="Angular Logo"
    src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNTAgMjUwIj4KICAgIDxwYXRoIGZpbGw9IiNERDAwMzEiIGQ9Ik0xMjUgMzBMMzEuOSA2My4ybDE0LjIgMTIzLjFMMTI1IDIzMGw3OC45LTQzLjcgMTQuMi0xMjMuMXoiIC8+CiAgICA8cGF0aCBmaWxsPSIjQzMwMDJGIiBkPSJNMTI1IDMwdjIyLjItLjFWMjMwbDc4LjktNDMuNyAxNC4yLTEyMy4xTDEyNSAzMHoiIC8+CiAgICA8cGF0aCAgZmlsbD0iI0ZGRkZGRiIgZD0iTTEyNSA1Mi4xTDY2LjggMTgyLjZoMjEuN2wxMS43LTI5LjJoNDkuNGwxMS43IDI5LjJIMTgzTDEyNSA1Mi4xem0xNyA4My4zaC0zNGwxNy00MC45IDE3IDQwLjl6IiAvPgogIDwvc3ZnPg=="
  />
  <span>Welcome Users</span>
    <div class="spacer"></div>
      
</div>

<br><br><br><br>
  <div class="containerc_lients">

      <h2 style="size: 16px; text-align: center;color: rgb(157, 228, 204);"> User Management System </h2>
      <br><br>
      <hr>
      <form action="">
        <div class="row mb-3">
          <label for="colFormLabelSm" class="col-sm-2 col-form-label col-form-label-sm"> Document Client:</label>
          <div class="col-sm-2">
            <input type="number" class="form-control form-control-sm" id="colFormLabelSm" placeholder="insert document client.">
          </div>
        </div>
        <div class="row mb-3">
          <label for="colFormLabel" class="col-sm-2 col-form-label"> Name client: </label>
          <div class="col-sm-4">
            <input type="text" class="form-control" id="colFormLabel" placeholder="insert name client">
          </div>
        </div>
        <div class="row mb-3">
          <label for="colFormLabelSm" class="col-sm-2 col-form-label col-form-label-sm"> FirstName Client: </label>
          <div class="col-sm-4">
            <input type="text" class="form-control form-control-sm" id="colFormLabelSm" placeholder=" insert firstname client">
          </div>
        </div>
        <div class="row mb-3">
          <label for="colFormLabelSm" class="col-sm-2 col-form-label col-form-label-sm"> Car Numbers : </label>
          <div class="col-sm-2">
            <input type="number" class="form-control form-control-sm" id="colFormLabelSm" placeholder=" insert card number">
          </div>
        </div>
       
        <div class="row mb-3">
          <label for="colFormLabelSm" class="col-sm-2 col-form-label col-form-label-sm"> city: </label>
          <div class="col-sm-4">
            <input type="text" class="form-control form-control-sm" id="colFormLabelSm" placeholder="insert city">
          </div>
        </div>
        <div class="row mb-3">
          <label for="colFormLabelSm" class="col-sm-2 col-form-label col-form-label-sm"> Direction: </label>
          <div class="col-sm-4">
            <input type="text" class="form-control form-control-sm" id="colFormLabelSm" placeholder="insert direction">
          </div>
        </div>
        <div class="row mb-3">
          <label for="colFormLabelSm" class="col-sm-2 col-form-label col-form-label-sm"> Age: </label>
          <div class="col-sm-4">
            <input type="text" class="form-control form-control-sm" id="colFormLabelSm" placeholder="insert age">
          </div>
        </div>
        <div class="row mb-3">
          <label for="colFormLabelSm" class="col-sm-2 col-form-label col-form-label-sm">Value Car</label>
          <div class="col-sm-4">
            <input type="number" class="form-control form-control-sm" id="colFormLabelSm" placeholder="insert value car">
          </div>
          <br><br>
          <div class="col-md-4">
            <label for="inputState" class="form-label">State</label>
            <select id="inputState" class="form-select">
              <option selected>Active </option>
              <option>Locked</option>
            </select>
          </div>
        </div>    
              <button type="submit" class="btn btn-secondary"> Create </button>  
      
      </form>
  </div>
  <hr>
   
  
  <div class="containerc_lients">
    <h2 style="size: 16px; text-align: center;color: rgb(157, 228, 204);"> User Management System </h2>

      <table class="table_client">
        <thead>
            <tr>
              <th scope="col">Id</th>
              <th scope="col">Document Client</th>
              <th scope="col">Name Client</th>
              <th scope="col">firts Name</th>
              <th scope="col">Car Number </th>
              <th scope="col"> City</th>
              <th scope="col"> Direction</th>
              <th scope="col">Age </th>
              <th scope="col"> Value Car </th>
             
            </tr>
        </thead>

        <tbody>
              <tr>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td> </td>
                <td>
                  <button type="button" class="btn btn-secondary me md-2 "> Edit </button>  
                  <button type="button" class="btn btn-secondary md md-2"> Delete </button>  
                </td>
              </tr>
        </tbody>

      </table>

  </div> 







<router-outlet></router-outlet>

