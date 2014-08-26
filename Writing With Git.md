Writing With Git


An idea for a next-generation word processor.

For anyone unfamiliar with these terms, here’s a simple description of Git and a simple description of GitHub.

My younger brother is a senior at UC Berkeley, soon to finish with a social science major, but with a budding interest in web development. Last night I was trying to impress upon him the importance of Git, and how great GitHub is for novice coders — if you know where to look. Besides being able to look at production-quality code, there are also repos that are styleguides, programming books, or lists of links. For a true beginner, these can be much more valuable than, say, being able to poke around the internal workings of jQuery.

During our chat I said “if I were writing papers for college now I would consider writing them in a code editor in Markdown.” I hadn’t thought this through before I said it, but I kept thinking about it after we finished talking. What would a Git-powered word processor, using Markdown and designed for non-coders, look like?

#### The Problem
Like my brother I also majored in social sciences, specifically Political Science and Economics. I wrote a lot of papers. But much of the time that I spent “writing” was actually spent wrangling formatting, mucking around with footnotes, trying in vain to recover lost changes, or wishing I could revert to earlier versions. Anybody who has used “track changes” in Word (or analogous features in Google Docs or Pages) knows what a nightmare it can be. Each change, regardless of its triviality, is accorded the same level of visual importance. Track changes clobbers page formatting. I doubt I need to belabor the point, since nearly everyone has wrestled with a cumbersome word processor at some point.

A quick Google search doesn’t turn up much for git word processor. The Git Handbook talks briefly about using Git with Word documents. There’s a Branch discussion about ideal word processor features, although most of the participants seem to be hackers and would thus presumably feel comfortable writing in TextMate or Sublime. There’s a repo called gitpublish which uses Git “metaphors” and seems fairly technical. But that’s about it.

Update: I came across github-bookeditor which implements much, though certainly not all, of what I imagined GWP would do.

Update 2: Draft is the closest thing I’ve seen yet. It has most of the features described here. More on this below.

#### Git Word Processor

So what are the important features? I’ll call this hypothetical app “GWP” from here on out.

It would use Git as its core, and offer GitHub integration.
It would have a familiar word processor interface, and tools for debugging repos that avoid the command line.
Content would be written in Markdown.
It would offer document and text formatting tools.
It would be able to easily publish content to a variety of web platforms, as well as produce beautifully formatted PDFs.
Let’s look at these in a little more detail.

#### Git
Using Git is the whole idea here. Integrating a GWP desktop app with GitHub should be encouraged but not required. When “saving” a document, the user would be creating a commit. This is the fundamental core of the concept, but I’m a Git novice so I’m not sure what it would look like beyond that. GWP would work as a web app using the FileSystem API. Prose.io is an example of what’s possible with GitHub’s awesome API, and actually already does part of what the GWP would ideally do. Unfortunately it doesn’t look like that project has moved forward appreciably in months.

#### Interface
The GitHub desktop app does a great job of presenting an interface that isn’t intimidating for Git virgins, so GWP features involving Git directly could take massive inspiration from that. GWP would be designed for users who have never seen the command line, and who get cold sweats even looking at code. An essential feature would be easy ways to debug a repo that has gotten messed up somehow, without resorting to the command line. GitHub’s desktop app will sometimes give you an error message that says “Failed to sync this branch. You might have to open a shell to debug the state of this rep0.” GWP would seek to avoid this at all costs, perhaps by simplifying the type of Git commands that are enabled by default. Power users who are comfortable debugging their own repos would be free to enable these features. A PowerPoint-style interface for developing presentations would be a terrific feature as well.

Markdown
Markdown is awesome. In fact, I don’t think it’s a stretch to say that a significant portion of the success that iA Writer has enjoyed is due to the heavily Markdown-inspired formatting syntax it uses. For people who spend way too much time wrestling with formatting in Word, Markdown is an absolute revelation.

StackEdit is an open source web app that accomplishes much of what I’d envision GWP would do with Markdown. However, the key difference I imagine is that you would type in Markdown but only see your formatted content. This might be jarring — frankly I have no idea. But I feel like users would get used to it. You would certainly be able to toggle between raw Markdown (in a monospaced font) and your formatted content. Perhaps when the editor detects you might be entering Markdown syntax (i.e. typing hash signs) it displays those characters differently until well-formed Markdown, then formats the text visually. So, when entering a second level header, you’d type “##” which would be highlighted and set in a monospace font, but once you hit space and start typing the heading’s text, the “##” would disappear and you’d automagically be typing in your heading level two style.

The two-pane model used by StackEdit can be distracting. It also works much better for content that will be displayed fluidly on the web than for documents intended for printing. I imagine the interface for GWP to be more like a classic word processor. It would be paginated, with the kinds of page margins, headers, and footers, you’d expect to see in Word or Google Docs. Users could opt to enter a fluid mode that would more accurately represent how the content would appear on the web.

#### Formatting
Word and its ilk offer ways to set the global styles for different levels of headers, but I rarely used them, and I think that’s fairly common. It’s cumbersome to write a section title, outline it, then select which header level it is from a dropdown. Usually I would find myself manually formatting each header, which is absurd. Markdown has the perfect antidote for this in that you can easily set different header levels with preceding hash marks. Encouraging users to use a proper information hierarchy within a document allows for easy styling of different headers levels. I would imagine GWP would have formatting tools similar to those found in Word, although dramatically stripped down to just those that are commonly used. While use of Markup syntax would be encouraged, keyboard shortcuts for italic and bold would remain, and shortcuts for other styles would be available, as they are in the Medium editor. Under the hood, formatting would be done with CSS. This would allow those who are willing and able to have virtually unlimited control over document presentation.

GWP would also provide all the pagination features present in Word, like having a title page, page numbering, as well as headers and footers. Some kind of automated footnoting would be a great feature as well.

#### Publishing
Though originally conceived as a replacement for Word, Pages, or Google Docs, GWP would do more than merely produce nicely formatted documents suitable for printing. Like prose.io, it would be able to act as an content editor for GitHub Pages. Perhaps if you open Markdown documents from a local file location that indicates it is part of a Jekyll site, GWP could load up the appropriate stylesheets and display content close to how it will ultimately be displayed on the web. GWP should be able to publish posts to WordPress and other CMS, as well as Tumblr and similar platforms. If Medium ever provides an API, it would be great to have that as an option.

But one of the critical features would be for exported PDFs to look very similar to documents created in Word. College professors expect papers to look a certain way, after all. They also expect them to be a certain length, which is nearly always measured by pages. A student writing a 25-page term paper will damn sure want to know how much progress she’s made towards that relative to that length at any given moment.

Miscellaneous
It would be absolutely crucial for GWP to run fully without a network connection. Whether this means native app, offline-first web app, or a web app downloaded and run locally, or all of the above, I’m not sure. Part of this depends on the FileSystem API, for which support is currently very limited. In any case, limiting dependencies is important. Developers take for granted having Node, NPM, Ruby, Rails, etc. installed for a locally run app, but these would be a hurdle for most hypothetical GWP users. In an ideal world the app would be 100% client-side JavaScript, but I’m not sure how feasible this is.

GWP should encourage hackers to use it for non-coding projects. What this would look like, I’m not entirely sure. First, it should be easy to switch to a non-paginated mode that is more comfortable for people who create content primarily for the web. I mentioned above that users should be able to delve in to the underlying CSS if they so choose. Syntax highlighting for code blocks would be essential. Integration with Gists would be cool. A more ambitious feature would be literate programming for any language, although that might be beyond the scope of the project.

#### Bringing It All Together
As I’ve mentioned throughout, there are apps out there right now that implement various parts of what GWP would do. iA’s Writer showed that people will readily adopt the write-to-format syntax that Markdown provides. StackEdit shows what’s possible in a Markdown editor web app, and its open source codebase could provide a great starting point. Prose.io shows what can be accomplished through the browser with the GitHub API. GitHub’s own desktop app shows that Git can be made (mostly) user-friendly. Google Docs presents a familiar word processor interface in the browser, complete with page breaks and margins, that is be necessary for any tool seeking to supplant an entrenched incumbent like Word. Draft comes very close to a comprehensive solution, and indeed exceeds the GWP concept with a number of innovative features. However, it’s not clear if Draft uses Git under the hood, and it doesn’t seem to integrate with GitHub at this point.

#### Git On Campus
In September 2013, Wired put out an article on GitHub and co-founder and President Tom Preston-Werner titled “From Collaborative Coding to Wedding Invitations: GitHub Is Going Mainstream.” The article’s focus was that, while it’s has cornered the hacker market, GitHub is poised to expand beyond the software development industry.

But he [GitHub founder Tom Preston-Werner] thinks the GitHub way could work just about any place where text needs to be stored, edited, and discussed: law firms, hospitals, banks, design shops.
Likewise, in an interview with opensource.com, GitHub co-founder and CIO Scott Chacon was more explicit about GitHub’s goal of bringing Git to the masses.

The collaborative nature of open source development is something that we’ve tried to simplify, and we’re trying to simplify to the point where you don’t have to be a coder in order… to collaborate on structured documents of almost any kind. People are using it to write books, people are using it to write research papers… We use it internally for legal documents that we’re working on.
He goes on to specifically mention a coming shift “to simpler writing formats like markdown and away from proprietary binary formats like Word.”

But neither Preston-Werner nor Chacon mentioned what I believe could be one of the biggest markets for their product — universities. The volume of text produced at universities is staggering, as is the amount of time these institutions’ employees and students spend fighting with their word processors.

Undergraduates up all night working on term papers only to somehow lose them to the whims of Word. Professors and teaching assistants unable to keep syllabus, assignment, and exam versions straight from semester to semester. The organizational clusterfuck that every group project turns into. The difficulty students have collaborating on a study guide. University administrations trying to write and receive feedback on campus policies. The list goes on and on. Academia—at all levels—is dying for Git and only the Computer Science majors know about it.

(GitHub has a portal showcasing their product in education, but it’s focused on CS students and professors.)

Universities have another thing going for them: a high turnover rate, at least among the student body. Trying to convice an entire law firm, think tank, or corporation to leave the crushing embrace of Word would be difficult. But each fall change is in the air as millions of freshmen enter universities across the country. Undergrads, I believe, would be the most receptive audience for GWP. And once they graduate, they’ll bring Git with them into every industry that can make use of it.

#### Moving Forward
I’d like to take a stab at coding up a prototype web app, but have never built anything on this scale before. Any feedback on GWP is very welcome, and please let me know if you’d be interested in volunteering time or ideas. I’m on Twitter and (of course) GitHub. Update: created a GitHub organization and page and forked a couple of interesting repos.

Thanks for reading.
