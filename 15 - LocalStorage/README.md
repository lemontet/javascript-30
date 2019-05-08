# Local Storage and Event Delegation

There's nothing quite as frustrating as spending 10 minutes filling out a webform, only to accidentally refresh the page and lose all your progress.

To avoid this problem we can use local storage. Local storage lets us store page data in the browsers memory so that state persists even after refresh.

## Overriding default behaviour
When you refresh a webpage you are in fact telling your browser to navigate to the same address as your current page. You can see this behaviour in action on some webpages by preserving your console log; when you refresh the page you might see a statement which says `Navigated to https://yourwebsite.com`.

To take advantage of local storage, we need to override the default behaviour of our form using the `Event` interface method, `Event.preventDefault()`. This method tells the browser to 'override' the default behaviour of the event object. For a form, 'default' behaviour might be to clear or submit the form, neither of which we want.

## How local storage works
You have an object in your browser called 'local storage'. It's a list containing things you've saved to the current domain.


## Event Delegation
How do you add event listeners to elements that don't yet exist on the page?

Add the listener on the parent element. Use Event.target to identify the target element. If it's the kind of element you're after, you can assume it's 