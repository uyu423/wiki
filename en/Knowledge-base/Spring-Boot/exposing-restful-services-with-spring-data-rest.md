---
title: Exposing RESTful Services with Spring Data REST
description: 
published: true
date: 2023-02-17T18:02:24.149Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:16:41.494Z
---

- [Spring 데이터 REST로 RESTful 서비스 노출***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/exposing-restful-services-with-spring-data-rest)
{.links-list}


REST is an architectural style for building web services that are scalable, maintainable, and fast. Web services that conform to the REST architectural style, or RESTful web services, provide a consistent interface for clients and servers that is easy to use and understand.

One of the benefits of using the REST architectural style is that it makes it easy to expose data and functionality from web services as resources that can be accessed and used by clients. This makes it possible for clients to access and use data and functionality from web services without having to know how the services are implemented.

Spring Data REST is a library that makes it easy to expose RESTful interfaces for data repositories that are created with the Spring Data library. Spring Data REST takes the features of Spring Data and adds a default implementation of a RESTful interface that can be used to access data stored in a Spring Data repository.

In this post, we'll take a look at how to use Spring Data REST to expose RESTful interfaces for data repositories. We'll also look at how to use Spring Data REST to add custom functionality to RESTful interfaces.

Data repositories that are created with Spring Data can be easily exposed as RESTful resources using Spring Data REST. All that is required is to add the @RepositoryRestResource annotation to the repository interface.

The @RepositoryRestResource annotation is used to indicate that a repository should be exposed as a REST resource. The annotation can be used on both the interface and the implementation class of a repository.

When the annotation is used on the interface, it will cause the interface to be exposed as a REST resource. When the annotation is used on the implementation class, it will cause both the interface and the implementation class to be exposed as REST resources.

The @RepositoryRestResource annotation has several attributes that can be used to configure how the repository will be exposed as a REST resource.

The path attribute is used to specify the path of the REST resource. The default value is the uncapitalized, pluralized name of the entity.

The CollectionResourceRel attribute is used to specify the relationship of the collection resource to the parent resource. The default value is CollectionResourceRel.ITEM.

The Exported attribute is used to specify whether the repository should be exported as a REST resource. The default value is true.

The maxPageSize attribute is used to specify the maximum number of items that can be returned in a single page of results. The default value is Integer.MAX_VALUE.

The pageSize attribute is used to specify the default number of items that should be returned in a single page of results. The default value is 20.

The PagedResourcesAssembler attribute is used to specify the paged resources assembler that should be used to assemble the results of the findAll() method into a paged resources object.

The Projection attribute is used to specify the projection that should be used to expose the data from the repository. The default value is null.

The Rel attribute is used to specify the rel of the resource. The default value is self.

The ResourceDescription attribute is used to specify the description of the resource. The default value is null.

The ResourceRelation attribute is used to specify the resource relation of the resource. The default value is ResourceRelation.SELF.

The Sort attribute is used to specify the sort that should be used to order the results of the findAll() method. The default value is null.

@RepositoryRestResource(path = "people", collectionResourceRel = "people", exported = true, maxPageSize = 50, pageSize = 20)
public interface PersonRepository extends CrudRepository<Person, Long> {

}
In the example above, the PersonRepository will be exposed as a REST resource at the path /people. The collection resource will be named people and will be exported. The maximum number of items that can be returned in a single page of results is 50. The default number of items that should be returned in a single page of results is 20.

Spring Data REST also makes it possible to add custom functionality to RESTful interfaces. This is done by creating custom controllers and adding them to the application context.

 @RestController
 @RequestMapping("/people")
 public class PersonController {

     @Autowired
     private PersonRepository repository;

     @RequestMapping(method = RequestMethod.GET)
     public List<Person> findAll() {
         return repository.findAll();
     }

     @RequestMapping(method = RequestMethod.POST)
     public Person add(@RequestBody Person person) {
         return repository.save(person);
     }

     @RequestMapping(method = RequestMethod.PUT)
     public Person update(@RequestBody Person person) {
         return repository.save(person);
     }

     @RequestMapping(value = "/{id}", method = RequestMethod.DELETE)
     public void delete(@PathVariable Long id) {
         repository.delete(id);
     }
 }
In the example above, a custom controller is created that provides methods for finding all people, adding a person, updating a person, and deleting a person. These methods can be invoked by clients that make HTTP GET, POST, PUT, and DELETE requests to the /people path.

It's also possible to add custom methods to repositories that are exposed as REST resources. These methods can be invoked by clients that make HTTP GET requests to the path of the resource.

@RepositoryRestResource
public interface PersonRepository extends CrudRepository<Person, Long> {

    @RestResource(path = "findByName")
    public List<Person> findByName(@Param("name") String name);
}
In the example above, a custom method is added to the PersonRepository that can be used to find people by name. This method can be invoked by clients that make an HTTP GET request to the /people/findByName?name=<name> path.

 Spring Data REST is a library that makes it easy to expose data repositories as REST resources. Spring Data REST makes it possible to add custom functionality to REST interfaces. In this post, we've looked at how to use Spring Data REST to expose data repositories as REST resources.