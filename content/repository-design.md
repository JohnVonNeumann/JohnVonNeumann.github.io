Title: Repository Design
Date: 2019-08-04
Modified: 2019-08-04
Category: Automation
Tags: sysadmin, automation, devops, engineering
Slug: repository-design
Authors: JohnVonNeumann
Summary: Changing the way we think about repository UX.

## Changing the way we think about repository UX.

Since I started working in software, and more specifically, "DevOps", I have had to work with a smorgasbord of irregular repositories. They have varied in every way you can imagine, much of the time with relative impunity.

No one likes working with repositories like this. They are dirty and downright depressing in some instances, to move from a "clean" repository with good quality CI/CD, automation and quality control, into an old and crusty repository, without these things, feels wrong. I will make the generalisation that when people work in one of these "forsaken" repositories, they tend to work to a much lower level of quality than they might usually, because the state of the repository, does not inspire the need to work to a high level of quality. This is a problem.

### Broken Windows Theory

`The broken windows theory is a criminological theory that states that visible signs of crime, anti-social behaviour, and civil disorder create an urban environment that encourages further crime and disorder, including serious crimes. The theory suggests that policing methods that target minor crimes such as vandalism, public drinking, and fare evasion help to create an atmosphere of order and lawfulness, thereby preventing more serious crimes.`

I believe that the broken windows theory exists within software. I believe that human operators; software engineers, will instinctively checkout of good quality work if the environment they are working in has "visible signs of crime, anti-social behaviour, and civil disorder". It's a fairly understandable reaction.

The reasons for such "lawlessness" are enumerate, timelines, resources, laziness and general bad work, lack of knowledge/ignorance to better ways of doing work, lack of good quality tooling, etc. There are a host of bogeyman that can be used to blame this situation on.

### Programming has had a definition of "good" for a while now

There is so much content out there surrounding general software engineering and what constitutes good quality code that in many ways, we have developed a natural sense for what can be considered good quality. We "walk" into a codebase, and can see the hallmarks of greatness, and conversely, the hallmarks of a dumpster fire. This is endemic, it occurs without us considering it, we look at a codebase and say "this is garbage", we have developed a keen sense for garbagism and what its ugly little offspring look like. This is good.

Programming actually has a number of frameworks to support good quality code creation, and these frameworks are the logical backing that provides us our quick reflex "garbage identification". Extreme Programming, 12 Factor Application Design, Clean Code. All great examples of the work that has been put into creating good quality, well backed theory, to support the creation of good quality software engineering output.

### So where is ours?

Despite programmers (I mean this in the traditional Operations-Development sense) having had this structure and overall definition of "good work" for a relatively large amount of time, the DevOps space in many ways seems to struggle with the idea of taking some of this and relaying it into our own space.

We still struggle to (from my experience) standardise what a "good repository" should look like, with deltas in implementation occurring across organisations everywhere. This problem is only amplified with the shift to SaaS based git hosting, where new repositories cost nothing to create and more organisations move to multi-repository set-ups.

Personally, I am tired of having to enter a repository and add a gitignore with the basic ignores, add a CI file that'll largely look the same within the same language ecosystem, and I'm definitely tired of having to keep either a mental check-list of repository actions or consult a README file, then copy pasta the directives across, hoping they work.

### Enter "Repository Design"

My thoughts around how to fix this issue have started to fall under my own mental banner of "Repository Design", which I use as a way of thinking about what the best practice for a repository should be and how we as developers can go about designing good quality repositories.

I personally believe that the repository should be viewed in many ways as a product, a shippable that is self contained and can be quantified in terms of its quality. As we encounter a heavier push towards automation/infrastructure as code, it is important to highlight the delivery mechanism for this code, and having a publicly understood "API" for a repository, should help push us towards better automation. I also believe that repository automation is an area ripe for improvement, with massive gains to be achieved through simple adjustments in repository work flows.

An important distinction of Repository Design is the focus on the overall User Experience of a repository.

### How easily can a repository be used?
In many cases where large scale automation is done well, many people shy away from using the end product to its fullest potential what can be extremely complicated automation if they feel they either don't understand it or do not possess the skills to fix fuck ups if they occur. In many ways, a defining feature of good quality automation is that it is typically low maintenance once it is in place. You've already automated the task, so in many cases, the automation may sit chugging along for months, sometimes years, untouched, before human eyes gaze over it again. In my experience, the easiest way to detract value and usage from your otherwise perfect automation solutions is to not pay close enough attention to the very real human operators that will be using it.

As a simple example of the type of high level goals of Repository Design consider your local development environment:

It is most likely a 16GB+ machine, with plenty of free compute and zero network latency (to yourself), yet we consistently push all menial linting tasks off your local environment and onto a remote CI/CD server. How much time is lost in the process of creating the commits, sending them to your git hosting provider, having the build picked up, initialisation of a build agent, then it fails because you used a tab instead of a space.

Repository Design does not seek to remove CI/CD or anything of the kind, it simply seeks to allow developers to use the resources they have, properly, to enable better workflows for everyone involved. We wish to keep all the tasks that can be done locally, within the current CI/CD process, but also bring what we can internal, to quicken the feedback loops of development.

### No need for new tooling

The best thing about this situation is that in a large amount of situations, we have no real need for newer tooling.

* Repository Action/API Automation - Makefiles
* Automated Code Edit Automation - Githooks
* Stable, repeatable linting - Docker with Linters

This list is to continue being fleshed out, but for the time being I'll leave this where it is.

Older tooling, re-purposed with additional wrapping can provide great solutions to existing, boring problems, that for the most part are theoretically solved, but not in an automated fashion.

In some cases, it's not even that you need complicated automation, but a tool that generated simple basic default gitignore files would be a godsend, how many times have you gone into a repository littered with garbage like `.DS_Store` files, that a coworker hasn't put in the `.gitignore` but have now been committed into the repository? I know I've fixed this numerous times. And the main issue with this?

It's fucking boring.

No one likes doing stuff like this, but if you are an engineer with high standards, eventually, with enough time spent in one repository, these bugs will get under your skin and you'll want to fix them.

So you do fix it. And the world is good. Then you go to another repository...

### Conclusion

I'll be putting together some ideas/tooling around this in the months to come, I think these issues have bounced around inside my head long enough now that I've finally decided to automate these garbage tasks so I can focus on personally higher value work, this is what automation is about, moving humans towards higher value work.

I've been building a simple tool I'm calling `pstart`, and will have a simple "beta" release available soon when I have around 3 of the core features delivered. It's a simple tool that will allow for contextual repository management, regardless of the stage of life the repository currently exists in. I hope for it to be a way for automation folks (and everyone else) to take back some of their jobs, and usher in a more sensible way of thinking about repositories. As usual, it'll be opinionated, but it will also be Open Source. So feel free to make a pull. It's unit tested and all that, so I intend for it to be a good quality production.

Keep an eye on my Github at: https://github.com/JohnVonNeumann

Cheers for reading.
