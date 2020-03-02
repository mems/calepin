Write all, make reports, about choice has been mades

API references, guides, tutorials, and blog posts

- don't use words like “easy,” “simple,” “trivial,” and “not hard”
- when communicating on a project, use clear and accessible language for people who didn’t grow up speaking English, or read less-than-fluently.
- avoid accidental racism by using “denylist” and “allowlist,” instead of “blacklist” and “whitelist”

> After you do something dozens of times, it is understandable that something is “easy” to you. However, what about someone who’s never seen the UI or feature before?
> [...]
> Encourage people who are newer to the project to contribute to or address documentation that doesn’t make sense to them

- [Bus factor — Wikipedia](https://en.wikipedia.org/wiki/Bus_factor)
- [Code comments](../Development/Development.md#comments)
- [Technical writing — Wikipedia](https://en.wikipedia.org/wiki/Technical_writing)
- [Writing Documentation When You Aren't A Technical Writer — Part One | Stoplight API Intersection](https://stoplight.io/blog/writing-documentation-when-you-arent-a-technical-writer-part-one-ef08a09870d1)
- [Writing Documentation When You Aren't A Technical Writer — Part Two | Stoplight API Intersection](https://stoplight.io/blog/writing-documentation-when-you-arent-a-technical-writer-part-two-59997587cc2a/)
- [Why You Shouldn't Ignore Internal API Documentation | Stoplight API Intersection](https://stoplight.io/blog/internal-api-documentation/)
- [Where the Wild Docs Are | Stoplight API Intersection](https://stoplight.io/blog/open-source-documentation/)

## Specification

> Never use "SHOULD" in official guidance. Do the hard work to make it simple: "MUST" when people must do it, "MAY" when there's a choice.
— [Caroline Jarrett](https://twitter.com/cjforms/status/808333086563897345)

> "must" when people must do it, "may" when there's a choice.

> must = duty, may = power

- [w3ctag.github.io/explainers.md at master · w3ctag/w3ctag.github.io](https://github.com/w3ctag/w3ctag.github.io/blob/master/explainers.md) - explainer as living document that describes a (proposed) feature (for web platform)

## Checklist

- [The Simple Genius of Checklists, from B-17 to the Apollo Missions | Inside Nuclino](https://blog.nuclino.com/the-simple-genius-of-checklists-from-b-17-to-the-apollo-missions)

## Release note

- [As a Designer I want better Release Notes](https://uxdesign.cc/design-better-release-notes-3e8c8c785231)

## API

- [API](../Conception/Conception.md#api)
- [REST API Documentation Templates | Stoplight API Intersection](https://stoplight.io/blog/rest-api-documentation-templates/)

## Error messages

> Error messages as a form of documentation:
> 
> - Humble: "An unknown error occured (-50)" -> "Sorry, we could not reach the Netflix service. Please check Network Settings to connect to an available network and use Netflix (15001)"
> - Human: "Exception has been thrown by the target of an invocation" -> "There was a problem: Your password is incorrect"; "Your AccountSid or AuthToken was incorrect. [More info](https://www.twilio.com/docs/errors/20003)"
> - Helpful: "404. That's an error. The requested URL |url| was not found on this server. That's all we know" -> "That's very nice photo, but it's a bit too big. Try one that's smaller than 4000px tall by 4000px wide. Cancel - Try a different image"
> - Humor: "|illustration of beasts eating computers| We'll be back shortly. We may have forgotten to feed the wild Tumbeasts that roam our datacenter, resulting in gnawing and/or mutiny. Animal control has been alerted.", "Something went and got goofed. Retry"
> 
> — [Error Messages: Being Humble, Human, and Helpful will make users Happy — Write the Docs](https://www.writethedocs.org/videos/na/2017/error-messages-being-humble-human-and-helpful-will-make-users-happy-kate-voss/)

> Just like any other form of documentation, put the relevant information first. This can be done by having the object first and the action second. The user is looking for the result, not how to get there. This is helpful when users quickly scan your error messages.
> "Press the back button to return to the previous page." -> "To return to the previous page, use the back button."

Errors in docs, allows you to expand on the error message without increasing it in length, while still trying to help the user understand why they are getting the error.
For one error (ex: 401 status code error "Permission Denied"), there are a lot of possible causes which they clearly lay out in Error and Warning Directory.

- [Writing Documentation When You Aren't A Technical Writer — Part Two | Stoplight API Corner](https://stoplight.io/blog/writing-documentation-when-you-arent-a-technical-writer-part-two-59997587cc2a/)
