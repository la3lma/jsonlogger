This is a work in progress. It's a very simple system for receiving
logdata from some arduino sensors I've built.  They sense and log
bluetooth and wifi units around them, and upload that sensor data
using HTTP (unencrypted) to a server.

This server is the server that will receive that data.  It will
receive the incoming data, which is assumed to be JSON.  That json may
or may not be validated, or if it's validated it may or may not be
very strictly validated.  When it's validated (or not), it's written
as bson to postgres.  The postgres schema for the logging a triplet
consisting of a timestamp, a json metadata structure, and a json
payload structure.  The payload will typically start out being the
received logdata, and the timestamp the timestamp the original data
was read by the service.

The data may be inriched with intepretations about what was seen,
how to interpret fields in the data etc.    All of that will be domain
specific and will build on top of the basic architecture sketched out
above.

There will be some layering violation here, since it's a work in
progress :-) If clear layering turns out to be beneficial, I'm sure it
will be added eventually.