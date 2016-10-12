We arrived in Paris on the Friday via the Eurostar from London and spent a
couple of days doing the usual tourist things (art galleries, Churches etc.)
before turning up to the Theatre De Paris for our second Dotgo conference on
the Monday morning.

The doors opened a few minutes late (time spent usefully chatting with others
in the queue) but the whole registration process was quick and I had a stylish
black Parisian gopher t-shirt at the end of it. The venue as a plush chic theatre of
red decor was more uplifting than many tech venues and we feasted on chocolate
pastries and coffee.  I was lucky enough to recognise the go-vim author Fatih
Arslan and spoke with him about some of his future plans since I was quite keen
for delve debugger support (hoped for next year after vim 8 support had settled
down). I also snarfed a couple of his rare go-vim stickers. I felt guilty
taking two since they were in short supply but I had the legitimate excuse
that Sue my partner (and fellow programmer) would want one. 

We took a box at on the first floor which overlooked the stage and settled
down.  The Master of Celebrities introduced himself on stage and presented "Le
Gopher" -- a mysterious cloaked figure -- who spoke with a booming voice and
was unveiled to reveal a massive (well over average human size) gopher stuffed
giant.

Dave Cheney spoke first about "First-class functions" and credited as
inspiration a Rob Pike Blog:

https://commandcenter.blogspot.co.uk/2014/01/self-referential-functions-and-design.html

Basically passing functions to functions is something more usual in dynamic
languages such as javascript than more static, compiled languages like Go. But
it was still possible in Go.

Dave gave a number of examples:

https://github.com/davecheney/presentations/tree/master/do-not-fear-first-class-functions

But the one which really stuck in my head was that of a calculator.  The
initial version had a dispatch type function containing a large ugly case
statement which listed each arithmetic operation (eg. addition etc.) but by
passing each operation as parameters to this function it could be refactored to
look nicer and allow new operations to be more easily added. He also wisely
encouraged restraint in the use of first class functions.

Damian Gryski then spoke about memory allocations, caches and performance:

https://github.com/dgryski/talks/tree/master/dotgo-2016

He gave some suggestions for trying to fit data in caches but concluded
by saying in most cases just using simpler algorithms was better.

Then followed Dmitri Shuralyov speaking about GopherJS -- a compiler which
converted Go to Javascript -- which I found quite exciting. As a server-side
programmer I liked the idea of being able to avoid javascript and write Go to
run as Javascript and being able to access the DOM etc. He quoted the examples
of the frontend and backend being able to share the same business logic code
and validation code as an obvious advantage.  He also showed an ugly example of
call-back hell Javascript to do HTTP streaming which refactored into much
cleaner Go.

He also showed us an amazing "Hover Demo" running both on desktop and inside
browser:

https://dmitri.shuralyov.com/projects/Hover-Demo/

(takes a little time to load!)

Péter Szilágyi spoke about Ethereum -- a blockchain (like Bitcoin) based system
where you could run programs.  They had Denial of Service (DoS) issues last month
based on caching bugs but he was able to fix this with immutability in Go. Go
didn't have direct support for immutability but strings (and not slices) were
immutable.  Also he was able to make structs immutability indirectly.

https://ethereum.karalabe.com/talks/2016-dotgo.html

This was one of my favourite talks and I resolved to try the Ethereum system
out.

The buffet food at lunch was absolutely superb, much better than the average
tech conference food (London Go Conference I'm thinking of you!)  although
oddly there were no paper plates so one had to balance mini-pizza on tissue
paper.  Sadly Sue got quite angry about the toilet facilities for women and I
learnt that in the entire building only one toilet cubical downstairs was
available for women (and shared with disabled!). But over all I thought the
conference organisation was well above average (and I've been to many tech
conferences).  Many of us, including myself, had our photos taken with "Le
Gopher" up on stage during this break.

We then had four lightning talks. Simone Carletti told us that using
Go to develop a cross-platform API had led to better API design for the other
languages:

https://dnsimple.com/dotgo

Lucas Clemente talked about Google's fast QUIC (HTTP/2.0 over UDP) and his
implementation::

https://github.com/lucas-clemente/quic-go

Janaa Burcu Dogan gave an excellent description of useful flags to pass to the
Go build chain tools.

http://go-talks.appspot.com/github.com/rakyll/talks/gcinspect/talk.slide#1

Elias Naur spoke about Gomobile and told us it was now possible to directly
call Android Java and IOS Objective C from within Go.

One of the conference highlights was probably Kelsey Hightower talking about
"Self-deploying Go apps". A lot of speakers had shown kubernetes in use but he had
taken this one step further to create his Kargo library which allowed this
functionality to be embedded within a Go app itself. 

https://github.com/kelseyhightower/kargo

Kelsey was a particularly polished and amusing speaker and did some scary live
deployment demos to "rock the temple" of the Demo Gods (who didn't seem to mind
too much) and show now the world of many computers could be treated as just one
computer.

Some more lightning talks followed. Javier Provecho Fernández told us how to
produce smaller Go binaries by stripping the binaries.  Using the UNIX strip
was wrong (which explained to me why OpenBSD's strip on Go binaries had
actually produced *larger* binaries when I tried it!) but rather you should 
pass "-ldflags" options to "go build" in order to strip. Also he mentioned UPX to
compress binaries with the warning it tended to trigger Anti Virus warnings.

I needed caffeination at this point and my note taking on my mobile was less
zealous than before but I remember a lightning talk about:

https://github.com/sbinet/pygo

and Rhys Hiltner from Twich spoke on using 

https://golang.org/pkg/runtime/trace/

to debug a production issue and also spoke of finding a Garbage Collection bug
in Go itself (which would be explained in a future Twich video!).

Katrina Owen gave a nice example of code refactoring a zombie game (example
cunningly rewritten to hide the guilty!) using the Flocking Rule and, sorry it
has to be said, some quite ugly slide fonts!

Brad Rydzewski talked about how to use plugins (again something more associated
with dynamic languages than static). He had a nice way of wrapping calls to
external binaries using "net/rpc" for both os/exec and "docker run" and hosting
external plugins on github as a convenient registry and showed us his Drone CI
system as an example:

https://github.com/drone/drone

Matthew Holt, the author of caddyserver, talked about using Go with ACME (which
is Let's Encrypt API to automatically provision SSL certs).  The talk was a
good one, practical, useful and certainly was effective in showing how much
easier things had become than manual provision. He also gave reviews of
Go libraries to use ACME.

But, and I admit to straying into crypto politics here,  I did think it was a
little uncritical of the existing SSL infrastructure using trusted 3rd parties
(like issues with some of the root CAs!). Self signed can work with a web 
of trust.

The last talk was Robert Griesemer, one of the original Go authors, who gave a
superb talk on "Prototype your design!" using the example of how he was
prototyping a new feature (multi-dimensional slices useful for matrices) with
minimal modification of the existing Go compiler.  He certainly explained
things very clearly given the complexity of the subject. 

https://github.com/griesemer/dotGo2016

Basically he hacked the part of the system where the Abstract Syntax Tree (AST)
was written into order to cleverly shoehorn some new additional syntax in.
This meant, with relatively minimal effort, he could actually try out the new
syntax to see how well it worked with a view to adding something similar in
properly in future. He explained step by step, illustrating with node and link
type diagrams, as if you were watching the process of his work each change of
the AST to add an addition operation.

Once this was done he had enough of an implementation to experiment with the syntax
in order to review the design. He pointed out that "prototyping raises design
questions we didn't even know we should be asking".

He had the feature, of that subset of the clever who are able to teach, of
explaining things so well, by pitching at a high level, that for a few minutes
I thought I understood it all very clearly. Then I thought a bit more and
realised this was just the tip of the iceberg and how much more there was to it.

Anyway a great insight into how Go is developed and extended (and a example of
how other software should be extended) and a great finish to the day.
