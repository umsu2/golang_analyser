# golang_analyse

playing with rabbitmq in golang. sentence analyser, takes a sentence, process it using different processors, then collect result and publish to db, redis, email.

1. entry point, go-kit microservice takes http request 
2. request send to exchange 
3. exchange binds to multiple queues, queue might be , word counter, vow counter, lengh counter, longest word etc.
4. microservices workers handles all these queues, once job is complete, the microservice that handled the task must send the flag to another exchange (for task completion, indicating which sentence of which task is completed)
5. another, maybe just single one microservice then listens to that exchange/queue and once all task is completed for that sentence. send another msg to another exchange so multiple other microservice can handle report generation.
6. finally report is send to db, reddis and email. or even back to the response if making the request handling blocking. 

not sure how to avoid bottleneck on 5? could do pulling. but... it is terrible.
