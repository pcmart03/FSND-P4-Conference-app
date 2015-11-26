App Engine application for the Udacity training course.

## Student Responses
### Add Sessions to a Conference
The session model includes the following properties:

* name (required)
* highlights
* speaker 
* duration
* typeOfSession
* date
* startTime
* interestedAttendees (repeated)

Name, highlights, speaker, typeOfSession, and interestedAttendees are string properties. InterestedAttendees is a repeated property to record when more than one attendee is interested in the session. For this project, I just use it to get a count of the interested attendees for the **getPopularSessions** endpoint. However, in a more robust application, it could be used to return create a "See who else is interested" display, kind of like the facebook's "see who else has liked this" function.

I decided to save the startTime as an integer for convenience while developing. Times should be entered in 24 hour format with no colon. For example `0700 = 7:00 AM` and `1930 = 7:30 PM` This was easy to remember and hard to mess up while I was running tests. 

I chose to make speaker an ordinary text field, rather than having it auto populate from Google plus because I limited session creation to the session organizer, who I imagine would not be the speaker of every session. 


### Create 2 additional queries
1. **getPopularSessions** This querries looks for sessions in which more that have been added to more than five wishlists. I recognize that five is low threshold, but I figured it was fine for testing purposes

2. **getSessionByStartTime** This querries filters by Session.date and Session.startTime to return sessions begining at a specific time. It would be useful for an attendee looking to fill a whole in his or her schedule.

### Query Related Problem Solution
Currently Data store does not allow more than one inequality filter at a time unless they are on the same field, so attemping something like `.filter(ndb.AND(Session.typeOfSession != 'workshop', session.startTime < 1900))` would return an exception. In order to perform this querry, I first peformed a query that returned all sessions starting before 7. Then I iterated over the results of the query, and pushed all non-workshop querries to a list called filtered_session.  You can see my implementation under the endpoint **getEarlyNonWorkshops()**



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
