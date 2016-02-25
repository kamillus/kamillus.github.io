---
layout: post
title:  "Domain Driven Design with the Spring Framework"
date:   2016-02-25 18:44:30
categories: software design development DDD
---

With the advent of ORMs in modern programming tools, developers have been able to create relationships between objects rapidly, however, at a cost. The cost of ORM is the creation of [anemic models](http://www.martinfowler.com/bliki/AnemicDomainModel.html). Using Hibernate often, I have encounted the issue of anemic models and decided to outline how to mitigate this scourge before the domain expands!


If you are not yet familiar with Domain Driven Design, I encourage you to obtain the
[Domain Driven Design book](https://domainlanguage.com/ddd/) by Eric Evans. If you are in a hurry, there is some good material to be absorbed on Martin Fowler's web site as well. To summarize, the book outlines how to create rich domains by utilizing POJOs (or Objects in any other language). For myself, the experience of introducing DDD to the business was very pleasant. Between the business user and developer there was no magic; everyone was on the same page with the ability to contribute to the model thanks to the [ubiquitous language](http://martinfowler.com/bliki/UbiquitousLanguage.html). But alas, this blog entry is about the technical aspects!

My solution to Anemic Models was partly inspired by the (official?) [DDD Sample repository on github](http://dddsample.sourceforge.net/). In the code listed, the author separates domain models, specifications, value and other domain objects from the Hibernate repository. The author achieves full separation of domain from the ORM.

In my case, due to limited time, I have decided to leak some database creational logic into the domain by annotating my models with JPA/Hibernate keywords. While that may not be ideal, it aids with the clarity of the physical and the logical aspects of the domain. Similarly to the author, I use service and repository objects to persist content. Unfortunately, I end up mixing the service layer with the data persistence layer, which is obviously not ideal but nonetheless practical. What that looks like in the code is:

	//OrderServiceImpl.java

	@Autowired
	OrderRepository orderRepository;

	...
	@Override
	public void addCustomerToOrder(Order order, Customer customer)
	{
		order = orderRepository.findOne(order.getId());
		order.addCustomer(customer);
		orderRepository.save(order);
	}

	//Order.java
	@OneToMany(cascade=CascadeType.ALL, fetch=FetchType.EAGER)
	private List<Customer> customers = new ArrayList<Customer>();

	...
	public void addCustomer(customer)
	{
		customers.add(customer);
	}

A few things are happening there. First of all, I'm using spring IoC to autowire dependencies. Second of all, I'm using the orderRepository to save my changes (similarly to github DDD sample). Thirdly, I'm using a OneToMany relationship between my customer and order entities. For this to work, you will need to fetch the data for processing and that's where EAGER fetches come in handy. Additionally, we need to cascade all changes down when we save the entity.


Going forward, I'd like to further refactor my domain to make it indepenent of the surrounding technology i.e. get rid of JPA/Hibernate annotations. Additionally, there is improvement to be made in the services to represent the model more clearly. Domain Driven Design is a really nice way to create rich models while expressing business and software design. While it may not be the new shiny technology, it is still a solid concept to keep in your toolset.