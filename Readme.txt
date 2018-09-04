#Assignment:
#You may write in whichever language you want.

#You are provided with hotels database in CSV (Comma Separated Values) format.
#We need you to implement HTTP service, according to the API requirements described below. You may use any language or platform that you like: #C#/Java/Scala/etc.
#1.	RateLimit: API calls need to be rate limited (request per 10 seconds) based on API Key provided in each http call.
#1.	 On exceeding the limit, api key must be suspended for next 5 minutes. 
#2.	Api key can have different rate limit set, in this case from configuration, and if not present there must be a global rate limit applied.
#2.	Search hotels by CityId
#3.	Provide optional sorting of the result by Price (both ASC and DESC order).

#Note: Please don’t use any external library or key-value store for RateLimit. You need to create a InMemory Implementation for RateLimit

Assumption: 
I have used SpringBoot to develop the application. I'm attaching the executable springboot jar also with application source code. This executable jar can be run from any system where JAVA is present with command >>java -jar <JAR_NAME>
I have made few assumption:
1. There will be two type of the user "free" and "registered"
2. I have hard coded the registered users in a list(it suppose to come from database)eg. user1, user2, user3 
3. Client/API key will be set in the request header as "Client-key". If client key is not set in the request header, I'm considering that as a free user
4. Free user has 5 request/10sec to the API and Registered user has 100 request/10sec. It can be modified in the rate-limit.properties file in class path
5. designed URIs are:
	1. http://<HOST>:PORT/hotelbookingsystem/<CITY_NAME>  			==> List all the hotel in the city
	2. http://<HOST>:PORT/hotelbookingsystem/<CITY_NAME>?sort=asc  	==> List all the hotel in the city sorting of the result by Price in ASC
	3. http://<HOST>:PORT/hotelbookingsystem/<CITY_NAME>?sort=desc  ==> List all the hotel in the city sorting of the result by Price in DESC
6. It will generate the JSON output
	
Test: 1. If a free user sends more that 5 request/10Sec, He will be blocked for 5 Min. After 5 min, he can again send 5 request/10Sec
	  2. Registered user can send 100 request/10Sec. If we want to give unlimited access, I have made it configurable in "rate-limit.properties"
	  3. If we use the above mentioned URI 2 and 3, result will be shown in ASE or DESC respectively.
	  
Note: If I have missed anything or diverted from requirement, Please let me know.