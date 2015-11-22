App Engine application for the Udacity training course.

## Student Responses
### Add Sessions to a Conference
I mostly followed the pattern establish in the create conference methods to add sessions, only I set the conference as the parent for the session rather than the user. However, only the conference creator can add sessions to the conference.

For the featured speaker, I created a static method **cacheFeaturedSpeaker()** that checks to see if the speaker has more than one session at the conference. If so, the method udates memcache with the speaker name and sessions. I then created a request handler called **SetFeaturedSpeakerHandler** that calls the static method. Finally, I created a task in my **createSession()** method to set the featured speaker.

### Create 2 additional queries
1. **getPopularSessions** This querries looks for sessions in which more that have been added to more than five wishlists. I recognize that five is low threshold, but I figured it was fine for testing purposes

2. **getSessionByStartTime** This querries filters by Session.date and Session.startTime to return sessions begining at a specific time. It would be useful for an attendee looking to fill a whole in his or her schedule.

### Query Related Problem Solution
Currently Data store does not allow more than one inequality filter at a time, so attemping something like `.filter(ndb.AND(Session.typeOfSession != 'workshop', session.startTime < 1900))` would return an exception. In order to perform this querry, I first peformed a query that returned all sessions starting before 7. Then I iterated over the results of the query, and pushed all non-workshop querries to a list called filtered_session.  You can see my implementation under the endpoint **getEarlyNonWorkshops()**



## Products
- [App Engine][1]

## Language
- [Python][2]

## APIs
- [Google Cloud Endpoints][3]

## Setup Instructions
1. Update the value of `application` in `app.yaml` to the app ID you
   have registered in the App Engine admin console and would like to use to host
   your instance of this sample.
1. Update the values at the top of `settings.py` to
   reflect the respective client IDs you have registered in the
   [Developer Console][4].
1. Update the value of CLIENT_ID in `static/js/app.js` to the Web client ID
1. (Optional) Mark the configuration files as unchanged as follows:
   `$ git update-index --assume-unchanged app.yaml settings.py static/js/app.js`
1. Run the app with the devserver using `dev_appserver.py DIR`, and ensure it's running by visiting your local server's address (by default [localhost:8080][5].)
1. (Optional) Generate your client library(ies) with [the endpoints tool][6].
1. Deploy your application.


[1]: https://developers.google.com/appengine
[2]: http://python.org
[3]: https://developers.google.com/appengine/docs/python/endpoints/
[4]: https://console.developers.google.com/
[5]: https://localhost:8080/
[6]: https://developers.google.com/appengine/docs/python/endpoints/endpoints_tool
