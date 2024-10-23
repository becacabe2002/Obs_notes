## Chap 1: overview
Sample process to calculate Top picks:
1. A request is created
2. Server calls the rcm-sys, which consists of a pipeline of methods. 

- Rating prediction is only a part of a recommendation system.

- Taxonomy:
    + **Domain**: type of recommended content
    + **Purpose**: for the end user and for the provider
    + **Context**: environment of recommendation receiver
    + **Personalization level**: Most popular, Semi-personalized, Personalized
    + **Privacy and trustworthiness**: how much does user trust recommendations
    + **Interface**: input, output
    
### Design of MovieGeeks
* **MovieGEEKs** - main part of the site (serve client logic), responsible for retrieving movie data.
* **Analytics** - (Chap 4)
* **Collector** - tracks user behavior and stores in the evidence db. (log) (Chap 2)
* **Recs** - deliver the recommendations. (Chap 5)
* **Recommendation builder** - pre-cal recommendation (Chap 7)

Process of building a rcm-sys:
1. Idea
2. Log Data
3. Choose recommender algo
4. Create a model
5. Test offline
6. Test online

## Chap 2: ways to collect data from users
- Evidence is collected to reveal user's tastes.

- There are two main types of data produced by system's users.
    + **Explicit**: rating, likes
    * **Implicit**: log recorded by system monitor

- Collecting data on users only works if there is a way to identify customers.
    + Using cookie, when user logged in, information will be transfered to user profile.

- Getting visitor data from other sources (social media sites)

* Implicit ratings are extracted from the events triggered by the user.
* Explicit ratings aren't always reliable because they can be biased due to social influences. (Implicit is usually more reliable, but only if we understand the meaning of each event)
### Building collector for MovieGEEKs
* Place it in a parallel structure to a more scalability

* Have two logical parts:
    + Server side: save log from client side
    + client side: with MovieGeeks, it is just a function that post evidence to collector in the server side
    
* Log database contains each evidence as a single row:
    `date, user_id, content_id, event, session_id`
    
```js
// static/js/collector.js
function add_impression(user_id, event_type, content_id, session_id, csrf_token) {
	$.ajax({
		 type: 'POST', // post method since it add data to db
		 url: '/collect/log/',
		 data: {
				"csrfmiddlewaretoken": csrf_token, // csrf middleware token
				"event_type": event_type,
				"user_id": user_id,
				"content_id": content_id,
				"session_id": session_id // unique
				},
		 fail: function(){
			console.log('log failed(' + event_type + ')')
		}
})};
```
	
```python
@ensure_csrf_cookie
def log(request):

    if request.method == 'POST':
        date = request.GET.get('date', datetime.datetime.now())

        user_id = request.POST['user_id']
        content_id = request.POST['content_id']
        event = request.POST['event_type']
        session_id = request.POST['session_id']

        l = Log(
            created=date,
            user_id=user_id,
            content_id=str(content_id),
            event=event,
            session_id=str(session_id))
        l.save()
    else:
        HttpResponse('log only works with POST')

    return HttpResponse('ok')
```

## Chap 3: Monitoring the system

```text
[Evidence] --> [Website Usage] --> [User taste] --> [Rcms] 
```

### User personas
> Fictive people who represent different stereotypes groups of user.

* Analytics part

## Chap 4: behavioral data transform into ratings
* Transform user's behavior to a format that can be used as input for recommender algorithm.

* 

Chap5: non-personalized recommendations
Chap6: Prob of new users and simple sol

Chap7: formulas to calculate similarity between users or content items
Chap8: CF
Chap9: metrics for offline evaluation rcmers and ways to make rcm online
Chap10: CBF using Latent Dirichlet Allocation, TF-IDF
Chap11: CF but using dimensional reduction method
Chap12: way to mix types of rcmers
Chap13: ranking algorithms and learning methods to rank rcm
Chap14:
