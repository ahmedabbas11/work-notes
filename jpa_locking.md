#jpa and locking how to increment a counter without concurrency issues
hibernate locking
what you need here is a pessimistic locking 
https://docs.jboss.org/hibernate/orm/4.0/devguide/en-US/html/ch05.html

but it's vendor specific , so you need hibernate 
#locking with spring database

interface ParentRepository extends CrudRepository<Parent, Long> {
  @Lock(LockModeType.PESSIMISTIC_WRITE)
  Parent findOne(Long id);
}

https://stackoverflow.com/questions/35786815/write-lock-entity-in-spring-from-database

#increment a counter without concurrency issues

simply move the concurrency to the database level and for java it's atomic operation

UPDATE Tag t set t.count = t.count + 1 WHERE t.id = :id;

https://stackoverflow.com/questions/30143594/spring-jpa-and-hibernate-how-to-increment-a-counter-without-concurrency-issu