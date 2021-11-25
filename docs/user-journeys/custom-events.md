## User Journey Custom Events

In user journeys, you have the option to set the result as 'pass event' with text that you can enter.

Whenever triggers are met for this user journey, this event data is passed to you via an event on the document. You can handle this event by creating an event listener on the document for the event name 'csc-journey'

e.g.

```
document.addEventListener('csc-journey', (e) => console.log(e.detail));
```

Here, e.detail will contain the string value of the text you entered on the dashboard.
You can perform any action you want when this event is bubbled to you - in the example, we only logged the event data to the console.
