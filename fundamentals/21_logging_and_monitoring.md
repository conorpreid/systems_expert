# Logging and Monitoring

### Terms before beginning
- logging
	- the act of collecting and storing logs, useful info about the system
	- typically programs will output log messages to its STDOUT and STDERR pipes
	- these automatically get aggregated into a centralised logging solution
- monitoring
	- the process of having visibility into a systems key metrics 
	- implemented by collecting important events in a system and agg-ing them in human-readable charts
- alerting
	- the process through which system administrators get notified when critical system issues occur
	- can be set up by defining specfic thresholds on monitoring charts
	- past these thresholds, alerts are sent via various communication channels 


### Getting into it
think of edge case issues - you need to be able to debug when weird stuff happens \
you log stuff to tell you what the code is doing and what is happening during execution \
you also need to collect these logs and store them in a db, so that we can agg them later and visualise \
formats can be JSON, you have some service that reads those \
monitoring is what makes this process easier \
gives vis into health of the system \
you need metrics and a way to measure and report on those metrics \
think about algoexpert
	- are users running into latency when running code? 
	- are users able to access various pages quickly?
	- is the payment system working properly
	- how many sales per day 
	- authentication (google vs github vs facebook) etc
all about monitoring important metrics

often a time series database is used here \
purpose built to handle events over time \
query + graph those values in the db 

alerting then handles the comms on certain events beyond certain thresholds 

