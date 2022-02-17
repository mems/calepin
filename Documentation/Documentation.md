Aka documentation style guide, write documentation

Write all, make reports, about choice has been mades

API references, guides, tutorials, and blog posts

- when communicating on a project, use clear and accessible language for people who didn’t grow up speaking English, or read less-than-fluently.
- [avoid accidental racism by using “denylist” and “allowlist,” instead of “blacklist” and “whitelist”](../Development/Development.md#inclusive-terminology) - or use "blocklist" and "safelist". See [Inclusive terminology](../Development/Development/Development.md#inclusive-terminology)

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
- [Em Dash: What it is and When to use it - Writer](https://web.archive.org/web/20210228192127/https://writer.com/blog/em-dash-what-it-is-and-when-to-use-it/)

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
- [Keep a Changelog](https://keepachangelog.com/)

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

## Version message

Aka Git commit message.

Use verbes:

- Add: Create a capability e.g. feature, test, dependency
- Cut: Remove a capability e.g. feature, test, dependency
- Fix: Fix an issue e.g. bug, typo, accident, misstatement
- Bump: Increase the version of something e.g. dependency
- Make: Change the build process, or tooling, or infra
- Start: Begin doing something; e.g. create a feature flag
- Stop: End doing something; e.g. remove a feature flag
- Refactor: A code change that MUST be just a refactoring
- Reformat: Refactor of formatting, e.g. omit whitespace
- Optimize: Refactor of performance, e.g. speed up code
- Document: Refactor of documentation, e.g. help files

- https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits
- [How to write the perfect pull request - The GitHub Blog](https://github.blog/2015-01-21-how-to-write-the-perfect-pull-request/)
- [How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
- [joelparkerhenderson/git_commit_message: Git commit message: how to write a good git commit message](https://github.com/joelparkerhenderson/git_commit_message)
- [Bug Prediction at Google](https://google-engtools.blogspot.fr/2011/12/bug-prediction-at-google.html) - Use Git version message to predict spot bugs
- [How to Write a Git Commit Message (2014) | Hacker News](https://news.ycombinator.com/item?id=13889155)
- [Karma - Git Commit Msg](http://karma-runner.github.io/1.0/dev/git-commit-msg.html)
- [How to Get More Out of Your Git Commit Message - datree](https://datree.io/blog/git-commit-message-conventions-for-readable-git-log/)
- [commitlint](https://commitlint.js.org/)

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

## Title capitalization

- [Headline Capitalization for UX: Title Case vs. Sentence Case | Herosmyth](https://web.archive.org/web/20211006163719/https://www.herosmyth.com/article/headline-capitalization-ux-title-case-vs-sentence-case)
- [Sentence case: meaning, examples, and checkers - Writer](https://web.archive.org/web/20211028211147/https://writer.com/blog/sentence-case/)
- [A brief guide to capitalization rules - Writer](https://web.archive.org/web/20211028211600/https://writer.com/blog/capitalization-rules/)
- [Title Case Converter – A Smart Title Capitalization Tool](https://titlecaseconverter.com/)
- [Title Capitalization Rules | Title Case Converter](https://web.archive.org/web/20211026044013/https://titlecaseconverter.com/rules/)
- [APA Style 6th Edition Blog: Title Case and Sentence Case Capitalization in APA Style](https://web.archive.org/web/20210814164806/https://blog.apastyle.org/apastyle/2012/03/title-case-and-sentence-case-capitalization-in-apa-style.html)

## Style guide

Aka stylebook

Examples:

- [Voice and tone - Shopify Polaris](https://web.archive.org/web/20210317115928/https://polaris.shopify.com/content/voice-and-tone)
- [Skype brandbook](https://web.archive.org/web/20211002032642/https://download.skype.com/share/blogskin/press/skype_brandbook.pdf)
- [LinkedIn Brand Guidelines | LinkedIn](https://web.archive.org/web/20211023161239/https://brand.linkedin.com/en-us)
- [Voice & tone guidelines - Salesforce](https://web.archive.org/web/20211007141033/https://www.lightningdesignsystem.com/assets/downloads/salesforce-voice-and-tone.pdf)
- [Copywriting — Zendesk Brandland](https://web.archive.org/web/20211027040428/https://brandland.zendesk.com/copywriting#story)

Style guides:

- [Associated Press Stylebook](https://www.apstylebook.com/)
- [The Chicago Manual of Style](https://www.chicagomanualofstyle.org/home.html)
- [MLA Handbook](https://style.mla.org/)
- [APA Style](https://apastyle.apa.org/)
- [APA Style 6th Edition Blog: How-to](https://blog.apastyle.org/apastyle/how-to/)

See also:

- [Style guide — Wikipedia](https://en.wikipedia.org/wiki/Style_guide)
- [AP style of writing: a comprehensive guide | AP styleguide - Writer](https://web.archive.org/web/20211020220157/https://writer.com/blog/a-comprehensive-guide-to-the-ap-style-of-writing/)
- [Welcome - Microsoft Style Guide | Microsoft Docs](https://web.archive.org/web/20210403071232/https://docs.microsoft.com/en-us/style-guide/welcome/)
- [Mailchimp styleguide: the anatomy of a perfect content styleguide - Writer](https://web.archive.org/web/20210228193019/https://writer.com/blog/mailchimp-styleguide-the-anatomy-of-a-perfect-content-styleguide/)
- [Build a content styleguide for your team - Writer](https://web.archive.org/web/20210228200031/https://writer.com/blog/build-a-content-style-guide-for-your-team/)
- [5 decisions to make before you create a styleguide - Writer](https://web.archive.org/web/20210228190834/https://writer.com/blog/5-decisions-to-make-before-you-create-a-style-guide/)
- [How to Create a Writing Styleguide for Your Brand | Writer](https://web.archive.org/web/20210228195002/https://writer.com/blog/create-writing-style-guide/)
- [How to Write Better: 15 Ways to Improve Your Writing Skills | Writer](https://web.archive.org/web/*/https://web.archive.org/web/20210228191734/https://writer.com/blog/how-to-write-better/)
- [How well do you know your writing styleguide? - Writer](https://web.archive.org/web/*/https://writer.com/blog/how-well-do-you-know-your-writing-style-guide/)
- [What is plagiarism? The act of plagiarizing explained - Writer](https://web.archive.org/web/*/https://writer.com/blog/plagiarism/)
- [What is self-plagiarism and how to avoid it - Writer](https://web.archive.org/web/*/https://writer.com/blog/self-plagiarism/)
- [99 most common grammar mistakes and how to avoid them - Writer](https://web.archive.org/web/*/https://writer.com/blog/a-live-grammar-checklist-the-most-common-grammar-mistakes/)
- [How to avoid plagiarism in 5 simple steps - Writer](https://web.archive.org/web/*/https://writer.com/blog/how-to-avoid-plagiarism/)
- [20 of the most common writing errors at work - Writer](https://web.archive.org/web/*/https://writer.com/blog/20-writing-errors-at-work/)
