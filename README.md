# Problem Statement:

Develop rest end-point to generate dynamic email content (body) as html string which can be send as email to Emirates customer.

# Solution Detailing:

- System should maintain pre-defined HTML templates (embedded file in resource folder) for each type of emails.
- System should expose rest end-point which will accept “Email Type” and Dynamic-Data payload.
- For given “Email Type” and Dynamic Data, system should do the following to generate output html.
    - Pick proper templated based on given “Email Type”
    - Replace placeholder in template with attribute values of DynamicData object and return the string.

# Samples:

HTML template:-

Email Type = **Booking Email (BOOKING)**

Email Template = 

```
<html>
<head></head>

<body> 

Dear $dynamicData.customer,

Thank you for choosing Emirates. Your booking reference number is $dynamicData.PNR, Flight No $dynamicData.fltNo.

<b>Flight details</b>


<table><tr><th>Passenger Name</th><th>Seat</th></tr> 

            #foreach( $passenger in $passengers) 

            <tr><td>$ passenger.getName()</td><td>$ passenger.getSeat()</td></tr> 

            #end 

</table> 


Have a great flight..

Emirates 
```


# Request Payload:

{"emailType":"BOOKING","dynamicData":{"customer":"Adam","PNR":"ABCDE","fltNo":"EK 543","passengers":[{"name":"Adam","seat":"21G"},{"name":"Maria","seat":"21F"}]}}

# Response:

<html><head></head> 

<body> 

Dear Adam,

Thank you for choosing Emirates. Your booking reference number is ABCDE, Flight No EK 543..



**Flight details**



| Passenger Name | Seat 
|----------------|-----
|Adam | 21G
|Maria | 21F



Have a great flight.

Emirates 
