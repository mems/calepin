Aka documentation style guide, write documentation

Write all, make reports, about choice has been mades

API references, guides, tutorials, and blog posts

- when communicating on a project, use clear and accessible language for people who didn’t grow up speaking English, or read less-than-fluently.
- [avoid accidental racism by using “denylist” and “allowlist,” instead of “blacklist” and “whitelist”](../Development/Development.md#inclusive-terminology)

- [Bus factor — Wikipedia](https://en.wikipedia.org/wiki/Bus_factor)
- [Code comments](../Development/Development.md#comments)
- [Technical writing — Wikipedia](https://en.wikipedia.org/wiki/Technical_writing)
- [Technical Writing  |  Google Developers](https://developers.google.com/tech-writing)
- [Writing Documentation When You Aren't A Technical Writer — Part One | Stoplight API Intersection](https://stoplight.io/blog/writing-documentation-when-you-arent-a-technical-writer-part-one-ef08a09870d1)
- [Writing Documentation When You Aren't A Technical Writer — Part Two | Stoplight API Intersection](https://stoplight.io/blog/writing-documentation-when-you-arent-a-technical-writer-part-two-59997587cc2a/)
- [Why You Shouldn't Ignore Internal API Documentation | Stoplight API Intersection](https://stoplight.io/blog/internal-api-documentation/)
- [Where the Wild Docs Are | Stoplight API Intersection](https://stoplight.io/blog/open-source-documentation/)
- [Google developer documentation style guide  |  Google Developers](https://developers.google.com/style)
- [PharkMillups/beautiful-docs: Pointers to useful, well-written, and otherwise beautiful documentation.](https://github.com/PharkMillups/beautiful-docs)

## Specification

> Never use "SHOULD" in official guidance. Do the hard work to make it simple: "MUST" when people must do it, "MAY" when there's a choice.
— [Caroline Jarrett](https://twitter.com/cjforms/status/808333086563897345)

> "must" when people must do it, "may" when there's a choice.

> must = duty, may = power

- [RFC 2119: Key words for use in RFCs to Indicate Requirement Levels](https://www.rfc-editor.org/rfc/rfc2119) and [RFC 8174: Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words](https://www.rfc-editor.org/rfc/rfc8174.html)
- [w3ctag.github.io/explainers.md at master · w3ctag/w3ctag.github.io](https://github.com/w3ctag/w3ctag.github.io/blob/master/explainers.md) - explainer as living document that describes a (proposed) feature (for web platform)

## It's not easy for everyone

Aka "It's not simple for everyone"

Don't use words like "easy", "simple", "trivial", and "not hard".

> After you do something dozens of times, it is understandable that something is “easy” to you. However, what about someone who’s never seen the UI or feature before?
> [...]
> Encourage people who are newer to the project to contribute to or address documentation that doesn’t make sense to them
>
> — [Writing Documentation When You Aren't A Technical Writer — Part Two | Stoplight API Intersection](https://stoplight.io/blog/writing-documentation-when-you-arent-a-technical-writer-part-two-59997587cc2a/#oversimplification)

- [Don’t tell me it’s easy – BI Polar](https://ssbipolar.com/2020/05/01/dont-tell-me-its-easy/)

## Checklist

- [The Simple Genius of Checklists, from B-17 to the Apollo Missions | Inside Nuclino](https://blog.nuclino.com/the-simple-genius-of-checklists-from-b-17-to-the-apollo-missions)

## Release note

- [As a Designer I want better Release Notes](https://uxdesign.cc/design-better-release-notes-3e8c8c785231)

## API

- [API](../Development/Development.md#api)
- [REST API Documentation Templates | Stoplight API Intersection](https://stoplight.io/blog/rest-api-documentation-templates/)

## CLI

- [Command line documentation](../Development/Development.md#command-line-documentation)
- [man page - Wikipedia](https://en.wikipedia.org/wiki/Man_page)
- [Command manual page](../Operating%20Systems/Command%20line/Command%20line%20%28Unix%29.md#Command%20manual%20page)
- [Command manual page](../Operating%20Systems/Command%20line/Command%20line%20%28Unix%29.md#Colors%20and%20control%20sequences)

## Error messages

> Error messages as a form of documentation:
>
> - Humble: "An unknown error occured (-50)" -> "Sorry, we could not reach the Netflix service. Please check Network Settings to connect to an available network and use Netflix (15001)"
> - Human: "Exception has been thrown by the target of an invocation" -> "There was a problem: Your password is incorrect"; "Your AccountSid or AuthToken was incorrect. [More info](https://www.twilio.com/docs/errors/20003)"
> - Helpful: "404. That's an error. The requested URL |url| was not found on this server. That's all we know" -> "That's very nice photo, but it's a bit too big. Try one that's smaller than 4000px tall by 4000px wide. Cancel - Try a different image"
> - Humor: "|illustration of beasts eating computers| We'll be back shortly. We may have forgotten to feed the wild Tumbeasts that roam our datacenter, resulting in gnawing and/or mutiny. Animal control has been alerted.", "Something went and got goofed. Retry"
>
> — [Error Messages: Being Humble, Human, and Helpful will make users Happy — Write the Docs](https://www.writethedocs.org/videos/na/2017/error-messages-being-humble-human-and-helpful-will-make-users-happy-kate-voss/)

> Apex crash - Out of memory
>
> Apex crashed because it ran out of memory.
>
> The most common causes of this are:
>
> * "Texture Streaming Budget" is too high in your video settings. Lowering this can help.
> * All other programs plus Apex combine to use too much memory. Quitting other programs can help.
> * Your Windows page file is set too small. Increasing the page file size can help. (The page file lets Windows move less important memory to disk until it's needed again.)
>
> TECHNICAL INFORMATION:
>
> * Apex was using 2.3 GB of physical memory.
> * Apex was using 7.3 GB of virtual memory.
> * Apex failed to allocate 1.0 MB of memory.
>
> * Your PC has 32.0 GB of memory physically installed.
> * Your PC has 128.0 TB of virtual memory (with the page file).
> * After Apex exited, your PC memory load is about 84%.
>
> Ctrl+C in this window will copy this message so you can paste it as text.
>
> — [ralph waldo cybersyn on Twitter: "this is the most helpful crash message i've ever seen https://t.co/JCy4iDPrFt" / Twitter](https://twitter.com/atomicthumbs/status/1250265618500091906?s=12)

> Just like any other form of documentation, put the relevant information first. This can be done by having the object first and the action second. The user is looking for the result, not how to get there. This is helpful when users quickly scan your error messages.
> "Press the back button to return to the previous page." -> "To return to the previous page, use the back button."

Errors in docs, allows you to expand on the error message without increasing it in length, while still trying to help the user understand why they are getting the error.
For one error (ex: 401 status code error "Permission Denied"), there are a lot of possible causes which they clearly lay out in Error and Warning Directory.

- [Writing Documentation When You Aren't A Technical Writer — Part Two | Stoplight API Corner](https://stoplight.io/blog/writing-documentation-when-you-arent-a-technical-writer-part-two-59997587cc2a/)

## Personal pronoun

> In my writing, I’ve almost completely switched from “you” to “we”—I find it more engaging.
>
> Example:
> - Before: “If a property can be omitted, you put a question mark after its name.”
> - After: “If a property can be omitted, we put a question mark after its name.”
>
> — [Axel Rauschmayer on Twitter: "In my writing, I’ve almost completely switched from “you” to “we”—I find it more engaging. Example: – Before: “If a property can be omitted, you put a question mark after its name.” – After: “If a property can be omitted, we put a question mark after its name.”" / Twitter](https://twitter.com/rauschma/status/1235980161939619840)

> 'they' often helps avoid the 'he/she' issue in written English.
> — [Johnny D on Twitter: "@rauschma This is good. Also 'they' often helps avoid the 'he/she' issue in written English." / Twitter](https://twitter.com/JD_Rodger/status/1236376868410011648)

- [Personal pronoun - Wikipedia](https://en.wikipedia.org/wiki/Personal_pronoun)
- [T–V distinction](../Text/Text.md#t–v-distinction)
- [Second person and first person](https://developers.google.com/style/person)

## Naming

See also [../Development/Development.md](#naming)
