# Help PDQ.com with an exciting new product!

Here at PDQ.com we pride ourselves on being at the **very** cutting edge of technology. When we determined that the best way to keep our customers happy was to read their minds, we dove right in. Here we are a year later and the progress we've made is incredible! That said, between continuously improving PDQ Deploy, PDQ Inventory, and working tirelessly on the *Cabalistic Necromancer* (good name eh?) our engineers are stretched extremely thin. That's where you come in! Help us get the Cabalistic Necromancer (CN) to an alpha stage we can be proud of and demo to executives!

In a nutshell, CN reads minds! If that wasn't fun enough, it's currently calibrated to read the minds of PDQ.com employees ([1](##Disclaimers)). The way it is [currently implemented](##Links:)  the CN exposes a simple rest endpoint at https://pdqweb.azurewebsites.net/api/brain. This endpoint will return a **Thought** object (in JSON) that looks like this:
 
```json
{
    "name": "Matt",
    "currentBeer": "Guinness",
    "currentThought": "I wonder why this works?",
    "daydream": "https://media.giphy.com/media/5nj4KLBy2mhkH1pUWT/giphy.gif"
}
```

We, the engineering team, are very proud of this system, but we think it needs a bit more before we go show it to the executives. Namely, it needs a UI.

Unfortuantely our current system, which is very much still in *Alpha* stage has an issue where if multiple requests are sent to the `https://pdqweb.azurewebsites.net/api/brain` endpoint simultaneously, and the CN happens to pick the same employee's mind to read for any 2 of those requests... Well, let's just say the **Thought** it returns will likely be that employee's last... What is there to say, science is dangerous sometimes 🤷. To avoid this unfortunate outcome we need you to actually make a small backend as well as a small frontend.

The backend should host a simple endpoint (REST, websockets, grpc, whatever) that *your* frontend clients can use to invoke a call to `https://pdqweb.azurewebsites.net/api/brain` and then return the result to *all connected clients*. Furthermore, the backend needs to ensure that only 1 request is ever going to `https://pdqweb.azurewebsites.net/api/brain`! This is **vitally** important, please dont hurt any ~~more~~ employees!

The frontend should have a button that will invoke *your* API and present the information returned from the call *as well as* a photo of the employee (these photos can be retreived from https://www.pdq.com/about-us/ and their names should match the `name` field on the **Thought** object). You can get the employee photo on the backend or the frontend, we don't care, it just needs to be shown on the frontend to impress the executives 😅.

Since only 1 request can be made to the CN, but there will likely be many executives that all want to see this at once from multiple clients/locations, we need all connected clients to show some kind of 'loading' indicator if a request to the CN is already being made.

# Diagrams/Notes:

## Thoughts:
* The CN is, as you can tell, fairly unstable and will occasionally return `status: 500` errors. You will need to handle this, either on the frontend or the backend so that we don't look bad in front of the executives!
* You can create your application in whatever language you want, however understand that our preference and what we use is generally C#/TypeScript/JavaScript with .Net Core, Node, and React.
* We consider it a bonus if you containerize this application. If we can just run `docker-compose up` we'll literally cry with joy 😂

## Disclaimers:
1. All PDQ.com employees have signed waivers ensuring that they understand the risk involved with mind reading technology and all research involving the Cabalistic Necromancer, the Talismanic Formula, and [scp-2663](http://www.scp-wiki.net/scp-2663).

## Warning:
### Some of the following links contain trade secrets and should not be discussed outside of the scope of this project!

## Links:
* [Cabalistic Necromancer System Diagram](./Cabalistic_Necromancer.png)
