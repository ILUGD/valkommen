# valkommen

'Välkommen' is an automated attendance and feedback retrieval system.

## Tech Stack (stack)
1. BASH
2. Docker
3. Python 3
4. PostgreSQL

## Working

Välkommen works by automatically sending the RSVP mail to all prospective attendees once the event is finalized.

Also, after the event, the organizer can send the link to an anonymous feedback form of the particular day of the event OR (conclusively) of the whole event to only the attendees who were able to actually attend the event. This can be done through mail, rather than having a full-fledged application for attendees.

## Specifications

### PHASE I : RSVP MAILS

1. Valkommen finds out the email ID and full name of attendees that hit RSVP on the Meetup.org page.
2. After the deadline for RSVPs is over, the prospective attendees receive the confirmation email with a QR Code containing a hash of their email ID, hence unique to their personal invitation. This QR code is generated as follows:-

### PHASE - II : ATTENDANCE

The organizers and/or volunteers will make use of an online QR Code scanner that will scan the QR Code of the attendees, confirming their presence on the event. The API will register their presence in the Valkommen DB on the server side. If there are any new attendees, they can be enrolled then and there with just their email IDs and full legal name. This also needs to be implemented on the web app.

### PHASE - III : FEEDBACK

FEEDBACK FORM will be completely customizable according to the event.

Main Concerns-
- look out for the anonymity of the user filling the form
- ensure the feedback form is
   - only filled by the actual attendees of the event.
   - only filled once by every actual attendee.
- ensure the organizer have complete control over **when** to send the Feedback forms to the attendees.

1. Feedback forms should be available to be deployed 5 hours prior to the event time.
2. Organizer presses a button on the dashboard to deploy the feedback form mails to actual attendees. (defaults to "send feedback mail 1 hour after the event ends")
3. Attendees fill the form and Valkommen receives anonymised input from the attendees.

### ANONYMITY

The feedback will be sent to the Valkommen module, and accepted IFF-
   - the email ID entered in the form, matches any one email IDs out of the actual attendees
   - the email ID entered in the form did not fill the form already once

   > The feedback submodule retrieves all the hashed email IDs and maintains a separate list of feedbacks.

## Tasks
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
2. QR Code mailing system

## Deliverables
1. Automatic RSVP handling submodule.
2. Attendance confirmation submodule.
2. Automatic feedback form submodule.
