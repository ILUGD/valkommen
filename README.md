# valkommen

'Välkommen' is an automated attendance and feedback retrieval system.

## Tech Stack
1. BASH
2. Docker
3. Python 3
4. PostgreSQL
5. Django REST Framework

## Working

Välkommen works by automatically sending the RSVP mail to all prospective attendees once the event is finalized.

Also, after the event, the organizer can send the link to an anonymous feedback form of the particular day of the event OR (conclusively) of the whole event to only the attendees who were able to actually attend the event. This can be done through mail, rather than having a full-fledged application for attendees.

## Specifications

### PHASE I : RSVP MAILS

1. The organizer presses SEND in Valkommen module page on the web app. 
2. The organizer reviews the list of prospective attendees and presses CONFIRM to send the RSVP invite to the prospective attendees.
3. The prospective attendees recieve the mail and either press "Yes I'll be there" or "No, can't make it." (defaults to "No")
4. After the deadline for RSVPs is over, the prospective attendees recieve the confirmation email with a QR Code containing a special code unique to their personal invitation. This QR code is generated as follows:-

```
    Special Code = hash(email + timestamp at which the RSVP was done)
```

This timestamp will be taken from the Valkommen DB when the RSVP was actually responded to. The QR Code will be generated on the server, put in the mail and sent to the prospective attendee.

### PHASE - II : ATTENDANCE

For the on-site attendance, we need to be sure that the attendees actually show up at the event. For this, we will make use of the QR Code sent earlier with the confirmation mail.

The organizers and/or volunteers will make use of an onlie QR Code scanner that will scan the QR Code of the attendees, confirming their presence on the event in the Valkommen DB. If there are any attendees, they can be enrolled then and there with just their email IDs and full legal name.

### PHASE - III : FEEDBACK

- We have to look out for the anonymity of the user filling the form
- We also have to ensure the feedback is only filled by the actual attendees of the event.
- We also have to ensure the feedback form is only filled once by every actual attendee.

1. Feedback forms are ready to be deployed 5 hours prior to the event time. 
2. Organizer needs to press the button to deploy the feedback form mails to actual attendees.(defaults to "send feedback mail 1 hour after the event ends")
3. Attendees fill the form and Valkommen recieves anonymised input from the attendees.

### ANONYMITY

>The main advantage of using the timestamp is, this timestamp will be known to the database managing the RSVPs, and not accessible to the Feedback system. This allows us to ensure anonymity of the users filling the feedback form.

1. The feedback form will contain the timestamp retrieved from the Valkommen DB, and will be later used by the front end to recreate the hash with email ID entered by user in the feedback form. 

>The email ID entering ensures the form is filled by an actual attendee, and filled only once by any one attendee.

```
FEEDBACK FORM

front-end:

    given : timestamp of RSVP confirmation
                (hidden)

    inputs : 1) email ID of the actual attendee
                (required)
             2) How would you rate the event? 
                (0.0 - 100.0) (required)
             3) Would you like to share some views about 
                the event? 
                (can be blank)
```

2. The feedback will be sent to the Valkommen module with the recreated hash, and accepted IFF the hash matches any one hash out of the actual attendees. The feedback submodule only asks for the hash, and nothing else.

## Tasks
### Docker Image
1. Set up a basic docker image to set up working environment.
### Feedback
1. social media post -> feedback form
2. mail -> feedback form
3. create the feedback form (using APIs)
4. CLI for form creation

### RSVP
1. QR Scanner - web page
2. maintain a DB for attendance.
3. API endpoint for QR Scanner

### Attendance
1. Meetup page - get list of RSVP'd (prospective) attendees
2. Mail RSVP -- QR Code

## Deliverables
1. Automatic RSVP handling submodule.
2. Attendance confirmation submodule.
2. Automatic feedback form submodule.
