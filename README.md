# Tests-for-Words-API
Automated tests Postman collection and documents for Words API

Comments on the Words API tests checklists and Postman collection

GET a Word tests

The priority of each test case was evaluated according to my user experience, based on how often the specific input seems to be used. The highest ones are the test cases, which have inputs, which seem to be used more often. The high priority was also assigned to NoAuth user negative check, as Word API is a paid service with number of requests per day restrictions depending on pricing plan, so restrictions for NoAuth users seem to be important.

As the full number of test cases I derived did not exceed the task restrictions of how many requests could be in a Postman collection, I added all of them to the collection, including the low priority ones, as their numbers aren’t high.

The design of test sets for each request was based on following principles:
1.	For every request the proper HTTP response status code and time of response (under 1000 ms) were checked. For negative tests proper error messages were checked. 
2.	For every positive test it was checked whether the correct word was found according to the input.
3.	In positive tests besides checking that the correct word was retrieved, the full number or response keys was checked. I did not focus on the values of the keys, as it seems more of a database relations testing problem, so here I checked whether any other information was retrieved for the word except the word itself, as it is implied in API docs. The approach was to check that the number of keys retrieved in response is above 1, as the specific keys set could differ for every word depending on how much information there is in the database on the specific word. The exception is TC1.34 (Word, that could be different parts of speech), the number of ‘partOfSpeech’ details retrieved in ‘results’ key of the response was checked additionally, as there should be at least 2 of them.
4.	Additional check was added to every positive test, checking that ‘rhymes’ details were not returned by the request, as it is specifically mentioned in Word API docs that ‘rhymes’ details should not be returned by normal request, but after some tests executions some requests got ‘rhymes’ in responses (for further details please see Issues).

GET Word details tests

As there are 24 possible GET Word details request variants depending on which details are requested, the full number of tests, including negative ones, seemed to be excessive. The only negative checks I added to the collection are NoAuth tests.

The highest priopity was assigned to test cases. The high priority was also assigned to NoAuth user negative checks, as Word API is a paid service with number of requests per day restrictions depending on pricing plan, so restrictions for NoAuth users seem to be important. For the same reason it seemed logical to double-check each request variant individually to see, that there are no exceptions for NoAuth users among requests.

The design of test sets for each request was based on following principles:
1.	For every request the proper HTTP response status code and time of response (under 1000 ms) were checked. For negative tests proper error messages were checked. 
2.	For every positive test it was checked whether the correct word and correct detail type was found according to the input.
3.	Besides that, the full number or response keys was checked, that should equal 2 for every request, as only one key except “word” should be retrieved in the response.
4.	For ‘definitions’ details request additional tests were made to check that there is at least one definition found and that number of ‘partOfSpeech’ details equals the number of retrieved definitions.
