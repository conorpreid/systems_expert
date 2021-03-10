# Availability

### Terms before beginning
- Availability
  - The chances of a server or service being up and running at a given time
  - Measured in %'s
- High Availability
  - Systems with particularly high levels of availability
- Nines
  - Refers to percentages of uptime
  - 5 nines == 99.999% uptime (which is 5.3mins)
- Redundancy
  - The process of replicating parts of the system
  - this makes it more reliable
- SLA
  - service level agreement
  - collection of guarantees from service provider
  - about availability or other things
- SLO
  - service level objective
  - constitues an SLA, SLA's are made of SLO's.

### Getting into it
most systems have an implied guarantee of availability \
when you pay a subscription to a service, there is an implied aggreement that you will be able to access the site \
the importance of availability is application-specfic. airplane software? very important. some random webpage? not really \
its tough to get high availability, might mean you have to have low throughput or high latency etc \
diff parts of a system can have diff levels, depending on how important it is \
to improve - bring in redundancy. you don't want single points of failure \
its about duplicating etc portions of the system. if one server dies, the other takes over \
load balancer sits inbetween those servers, but now load balancer is a single point of failure. Bring in more load balancers then! \
this is passive redundancy - there is also active redundancy \
the latter is when only one server is ever handling traffic, if it dies the other *knows* and takes over \
in passive, the others just take over and nothing really happens \
leader election comes in here, will handle later  
