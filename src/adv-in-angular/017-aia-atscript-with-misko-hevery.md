---
layout: layouts/post.njk
title: >
      017 AiA AtScript with Miško Hevery
date: 2014-11-20 14:00:00
episode_number: 017
duration: 
audio_url: https://media.devchat.tv/adventures-in-angular/AiA017AtScript.mp3
podcast: adv-in-angular
tags: 
  - adv_in_angular
  - podcast
---

The crew talks about AtScript with Miško Heverly.



### Transcript

**_[Do you wanna have conversations with the Adventures in Angular crew and their guests? Do you wanna support the show? Now you can. Go to adventuresinangular.com/forum and sign up today!]_****CHUCK: **Hey, everybody and welcome to Episode 17 of the Adventures in Angular Podcast. This week on our panel, we have Aaron Frost.** AARON: **Hello.** CHUCK: **Joe Eames.** JOE: **Hey, everybody.** CHUCK: **John Papa.** JOHN: **Hello, from the West Coast somewhere.** CHUCK: **I'm Charles Max Wood from DevChat.tv. And this week we have a special guest, Miško Hevery.** MIŠKO: **Hello.** CHUCK: **We had you on the last episode and people generally know who you are. We brought you on to talk about AtScript. Do you want to kind of give us a brief overview and then we can start rapid fire questions at you?** MIŠKO: **Sure. So AtScript is a… we looked at JavaScript and we said, “Wouldn’t it be great if we had couple of features to make the developers’ jobs even easier? So they can be even more expressive about the code that they want to write.” And for that, we kind of came to the conclusion that it would be really nice to have this concept of annotations. And this is very familiar in like languages like Java. And also, if you have a very large scale projects, I'm talking about 50 people working in a kind of a large scale application, no one person can keep everything in their heads, and so it's useful to have some kind of a type system. But having a type system is actually, and having these annotations at compile time is not sufficient. You actually have to have them at run time. And so you have to have some kind of introspection API. So what AtScript really deals with is this ability to bring all these metadata to runtime, so that frameworks can take advantage of it and give the developers a really awesome experience in building their applications.** JOHN:**So one of the first questions I've got for you is it sounds awesome and I've used TypeScript in the past, I've used CoffeeScript and things like [inaudible] Java and C#, but what does runtime introspection gets you that the design type stuff, things like TypeScript has doesn’t give you?**CHUCK: **Can I stop you real quick? What do you mean by “runtime introspection?” or maybe that's the same question.** MIŠKO: **I think that's the same question. So in TypeScript, we can something as a string and we can verify at compile time that it indeed is a string. Now, there's a limit to what kind of verifications we can do because you have to know for example where you got the value, the function you called received the value whether that one is properly typed. And if it isn't, then you might not be able to verify that it is actually is a string. Now if you can verify that everything is correct, that's nice. But what you really would like to do is use the type information for Dependency Injection to assemble the application. And if you have types, you essentially have all the information to assemble it. For example, if you have a house and the house says, “I need a door.” And the door says, “I need a lock.” Then if you have a Dependency Injection system, you can just say, “Hey, give me a house.” And the DI system will say, “Okay, let’s see. What does a house need?” And it introspects onto the house and says, “Okay, what does the constructor parameters say?” And the constructor says, “Well, I need to take a door.” And it can recurse onto itself and says, “Okay, what does a door need?” It can again introspect the door and says, “Oh, I need a lock.” And so then it knows I have to instantiate a lock. I have to take the lock and put it in the door. Take the door instance, put it in a house. And there you go. I can return to you the house. And if you look at that syntactically, all the information is there but semantically, the information isn't present at runtime in something like TypeScript or CoffeeScript. And because it's not present at runtime, the DI cannot do its magic. So what we're doing is just extending something we all know and love which is types, to a various degree, I mean I'm not saying types are be all, end all. And bringing the information to the runtime, so that we can have frameworks such as DI, help you by assembling the application for you and make your life easier.** JOHN: **So if I heard you correctly, basically this to help the dependency injection with the next version of Angular?** MIŠKO:**It's not just Dependency Injection. Dependency Injection is part of it. The other part of it is for example, currently the way we register formatters or I think they are called “filters” in 1.X, and also the way we register directives is this very convoluted directive registration object. And it would be much better if you just would create a class, say I'm an ng-repeat and then annotate it with something like, “oh, this is a directive.” And then inside of the directive annotation, you place all the necessary information about what these dependencies are, what the bindings are, what kind of bindings it has and so on. And by placing that information in kind of an “annotation style”, it becomes much easier to reason about it, but also much easier to just kind of understand what the code is trying to do. You know, the intent of the code rather than something convoluted like the directive definition object that we have today. So it's not just DI, it's other pieces as well. Let me actually go further. This usefulness is not just for frameworks like Angular but for other frameworks. For example, in NodeJS, Express is very popular framework. And imagine you could just have the next version of, kind of the future version of Express could basically be where you have a bunch of methods and you could just annotate methods, saying that, “This method should be called when a request comes in the following URL.” “This method should be called when it's a POST,” versus “This method should be called when it is a GET.” “Oh, by the way, this method should be an interceptor and it should run in front of all other methods.” So as you can see, it's not just for Angular, but any kind of frameworks out there that we know and love could benefit by having the declarative kind of nature, and specify [inaudible] which would allow user, the developer to specify the intent of the application through these directives in a declarative fashion, rather than through some convoluted “add this to this thing” API kind of a thing.**JOHN: **So if you're building a directive or controller or service or factory or one of the other 20 things you can do in Angular today, we do “angular module.” and then that thing. It's actually a function name. In the new world with AtScript, we'll be able to just create a class, regular TypeScript type or ES6 and then just create an annotation on top of it to say that's a directive, right?** MIŠKO: **That's right. That's a directive. Or this is a filter, known as “formatters” in 2.0. And just by adding that annotation, you're immediately giving information to the system how to register it, add it and so on.** JOHN: **And those annotations are… so the class stuff, that's just ES6, but the annotations, those are AtScript, right?** MIŠKO: **Correct.** JOHN:**Okay. I'm just trying to clarify what is today in ES5. We have ES5. ES6 is coming already here in some cases with people. And then we're talking about TypeScript and AtScript. So there's four levels of things [chuckles] for lack of a better word, to think about.**MIŠKO: **Right. And I think the very important point to be made here is that we are not changing what is out there. We're not subtracting or modifying anything out there. We're purely just adding introspection and annotations. And this is an important point because it means that your existing ES5 code is a valid AtScript code. Your existing ES6 code is a valid AtScript code. So you can kind of have a progressive enhancement to your code base rather than saying, “Oh, by the way. It's a brand new language that changes everything, and we've fixed all the mistakes.” But the side effect of all that is, “Well, it's not really compatible with existing libraries. It doesn’t play with the ecosystem that you all know and love. Your semantics are slightly different, so you can’t just interface with them between the same… on the same webpage you cannot interface within the language as easily and so on.” This isn't the case. We're not trying to fix any mistakes that are existing in Java. We're purely just adding in a progressive enhancements kind of way, new benefits that you can get.** JOE: **So the first questions that comes to mind is if I'm authoring in Angular 2.0 and I want to create a directive, do I have to use the annotation?** MIŠKO:**No. You could do it in the good old-fashioned way in ES5. It wouldn’t be old fashion as in 1.X because that has a slightly, that horrible API with the directive definition object. Which maybe we could kind of bring back for backwards compatibility on migration path or something like that. I mean, we can worry about that in the future. But the annotations if you think about what an annotation is, it is just an extra property on the type factory. So there's a function factory class and you could just place an extra annotation on it. And the property is annotations. And so, when you say, again let’s take an example of “myfilter.” Suppose you have a “myfilter” and you annotate it with @filter name myfilter, it's the same thing as just creating a function type “.myfilter” and below saying myfilter.annotations = [new filter (because a filter is just a class) and in parentheses, you pass in all the parameters. So in other words, the “@” annotation symbol with some class is the same exact thing as replacing the “@” symbol with the new keyword and then taking the resulting object then assigning it to the array called annotations on an object. So we've just simplified a few steps that you don’t have to do the assignment and you can put the annotation in front of the function rather than behind the function. But fundamentally, that is what’s happening. And because it's so simple, it means that you can do this in ES5. And so you can take advantage of these declarative nature of things and these intent. But again, you're not forced to use AtScript. You can happily write ES5 code and get these benefits. It's just going to be slightly more verbose.**JOHN: **Can we switch gears for just a second and think about this? I’d like to make this really clear to people, because I don’t think it's been clear in the last couple of weeks out there, is do you have to use AtScript or not if you use Angular 2.0? What's the vision there?** MIŠKO: **No. You don’t have to use AtScript.** JOHN: **But it's going to give you more features, obviously. The things you were talking about.** MIŠKO:**By using AtScript what you gain is the ability… at the fundamental level, it just means when you have a directive declaration at the bottom of the directive declaration, you will say “.annotations = [new directive blah blah]” and the problem is that the declaration is at the bottom of the function and the function could be very long, and you really want it at the top of the function, right? And so by using AtScript, you essentially get to put it at top of the function. And instead of using the new keyword, you get to place the @ in front of it. That's one thing. The other piece that you gain is that if it's a directive, you also have to do “$inject” on it which is are you familiar with that with Angular 1.X. And that would be populated automatically for you because the type system would provide that information from the types. Again, if you don’t use AtScript, you will just have to do it manually. But there is nothing in there that in any way forces anybody to do this.**AARON: **So I have a question, Miško, who did you work on AtScript with? Who designed it? Was it just you in a box in a vacuum? Who worked with you on it?** MIŠKO:**The whole Angular team worked on this. And it really came from the frustration that we know how these annotations are useful in [unintelligible] server side in languages like Java. And in Java they are actually used all over the place, and they have quite rich ecosystem and many frameworks allow you to take advantage of them. And we kind of realized that there is really nothing equivalent in JavaScript. And all of these crazy hacks we're doing like “$inject =” and the bracket notation, and the parenthesis notation that we have for injection. They are just all kind of hacks. And the real problem with these hacks is that they are Angular-specific hacks. And so the question really came to us was, “Can we some way extend the language of JavaScript (and eventually propose it to ECMAScript committee) in a way that will allow us to have standardized ways of expressing these annotations?” So it wouldn’t be Angular specific like “$inject” but rather a generic mechanism by with others can extend this. And this came essentially in two forms. From the very, very beginning, it was very clear for us that whatever we come up with has to be compatible with ECMAScript 5. In other words, if we choose to do this, it should in no way mean that all of a sudden, you have to [unintelligible] your existing toolset or whatever and you have to move to this new language or whatever you wanna call this. But rather that it should be a progressive enhancement. That if you would like, you can get these benefits. You can have a cleaner syntax but you could still do anything you need to do in ECMAScript 5.**CHUCK: **One rumor that I heard&nbsp; was that AtScript was based upon or is a superset of TypeScript? Is that true? Are they closely related?** MIŠKO: **It's not exactly true today. This is our goal. With are in talks with the TypeScript folks and the TypeScript folks already have a type system that they are proposing for JavaScript. Now currently their type system is based off of ECMAScript 3 but they have a personal goal to align it with ECMAScript 6. And so, for the TypeScript, what we're really interested in is the introspection part. In other words, being able to look at these type annotations and meta data annotations at runtime, and use them to control the behavior of the application. And they are missing that specific piece. And so rather than inventing a whole new type system that will be yet another type system, that would further complicate the standardization process, we're basically saying, “Hey, let’s just look around. What's the most popular thing out there?” It looks like TypeScript is the most popular. It also is this progressive enhancement thing that an ECMAScript 3 is a valid TypeScript program. Now as I said, they are not ECMAScript 6 yet, but their goal is to become ECMAScript 6. And when that happens, then AtScript and TypeScript will be aligned.** JOHN: **So you said that their goal is to be ECMAScript 6. When you say “their”, are you talking about TypeScript&nbsp; in that case?** MIŠKO: **TypeScript, yes. And I don’t wanna speak for them, but that's my understanding from the chats we have had with them.** JOHN: **Right. So I’ve talked to the team in the past and I have a love-hate relationship with TypeScript. And I'm very open and honest about it. There's certain things I love about it. Some things I'm kind of like, “Eh.” But I believe that is their goal other than there's some additional things, just like you guys, that they feel like ECMAScript 6 won’t have, but would be nice to have, like types for example. That's not going to be in ES6, right?** MIŠKO: **Correct. So this is the types in a sense that when you have a function declaration, and you can optionally. And the keyword here is “optional.” I cannot stress this enough. You can optional specify additional type information about what you expect or what you're going to return. And the optional thing is super important. Because if you wanna work with existing set of libraries, you cannot expect everybody to automatically start adding type system. And frankly, types are not old to think that they’re cracked up to be. If I am a team of one or two people, it's not clear that types are really that beneficial. And also it's not clear that it's beneficial for a small project. Types really start to shine when you have a team of 50 people, couple of million lines of code and no one person knows the whole system. All of a sudden types become definitely an important guideline. Kind of an important “light” for you to shine on your source code, so that you can get around. So it is very important that we don’t make this mandatory. And that this is totally optional. If you think you can benefit from types, then by all means, go ahead and use them.&nbsp; If you don’t think that they are beneficial to you, then keep doing what you’ve been doing. And again, to stress this, an ES6 or ES5 is a valid, will be, a valid TypeScript when TypeScript gets aligned with ES6. And is a valid AtScript program today. So you _can_ start with no types. And then at some point in the future say, “You know, I really could benefit from this thing.” And so you can turn on type checking for yourself without affecting any of the existing code base.** AARON: **So it sounds like this is going to be a cool tool for pretty much any project, like thinking about using a Node and thinking about other frameworks using it. Sounds like it could be pretty cool. So I was thinking about how cool it is while you we're talking, I'm wondering who’s going to maintain this project because if it's like in the Angular repo, I'm imagining that will like shy a bunch of people away from using it. So who's going to maintain this? Is it the Angular team or you guys are going to have like own repo?** JOHN:**It's just Miško by himself, man. [Laughter]**MIŠKO: **As of right now in order to get started and get things going, it is currently an Angular repo. Once we get Angular 2.0 out and many of these things get ironed out, we are going to move it to its own repository. And once it's in its own repository, we are actually actively looking for people to maintain this. We have some budget for several individuals to kind of work on this fulltime. So, the kinds of things we would like to do with AtScript you know… what we have today is just the syntax and we have a Traceur which can transpile this for introspection. We also can generate runtime checks. When you say something is&nbsp; a string, we'll verify it on runtime that it's indeed a string. So we can do that today. What we would like to add is kind of an offline, the static analysis with the combination of inference engine, so that you can statically… just like TypeScript has, these language services that plug in very well to the IDEs, same exact idea here is that we would like to analyze these code base statically and then provide you helpful hands that could also be optionally integrated into an IDE.** JOE: **That's really cool. Have you actually maybe spoken with like… the IDE that I feel like is most responsive to these sorts of things is JetBrain’s WebStorm which I personally love. Have you guys actually had any preliminary talks with them about this?** MIŠKO: **Yes, we're chatting with them. We're also chatting with NetBeans. And so we're actively reaching out to the IDEs, giving them heads-up what's coming out. And from the IDE’s point of view, it's actually not a lot of work. I mean, I don’t wanna speak to them too much, but because it is essentially just ES6 and it is essentially just TypeScript, they just have to add couple of new things into their parser so that they don’t barf on these new syntax. And then everything else is an already handled by the existing parser. So it's also for IDEs as incremental improvement that they can add to the system and add support for this.** JOHN:**I think that's what makes TypeScript [unintelligible] I know Visual Studio and others, they use the types to actually get better tooling in those IDEs. But if I can switch gears or maybe you already kind of covered a little bit of this already is, I hear a lot this “not invented here” syndrome. So this is being used for Google for Angular, but is there use for AtScript that side of Angular that you could talk about? And what other web tech is influencing your direction besides kind of just what Angular is [unintelligible].**MIŠKO: **I've kind of already touched on it that imagine you have an Express server and instead of configuring the Express in the current way, you could just have methods. And you could annotate these methods that basically would say something like, “This method is for a Git request on the following URL and the following things have to be extracted out of the URL.” “This is a POST method or a PUT method and so on.” So really, any framework can really benefit from being able to declaratively give the developer declarative tools of specifying intent rather than getting the intent through an imperative kind of programmatic API. So I see the benefit for it is way beyond Angular. And if you kind of wanna see what benefits could be like, again I would direct you to look at the Java ecosystem and the annotations and how much use they get in that ecosystem. And it's used anywhere from writing unit tests to writing frameworks and everything in between.** CHUCK: **Yeah. I have to say that I have a lot of friends who are very involved in writing Java. And what Miško was talking about is exactly what they complain about when they go to a weakly typed or non-typed system such as JavaScript or Ruby.** MIŠKO: **This is a very good point you bring up. And lot of back end developers are moving towards frontend, and sometimes they are really afraid like, “Hey, what did you do with my types? I've been used to them for so long. Where are they? And why can’t I have my annotations, etcetera.” And all of these things are beneficial to the community at large. These not benefits just for Angular. And this is why I don’t know how to stress this further, it's like, “Yes, it's coming from an Angular team, but in no way is this thing Angular specific.”** JOE: **Was the driving force behind inventing AtScript essentially you and the problems you were having or was it a reflection of bigger things?** MIŠKO: **It wasn’t necessarily a problem for us. We’ve spent a lot of… debating and thinking about the end-user and developer. We wanna make sure that the developer experience, the people who are actually building the web applications, that those people have a wonderful experience. And we end up debating all kinds of things. Anything from the dependencies between different classes, because all these things implicate how the stability is going to be possible, how the application gets assembled, etcetera. And this is yet another way that we debate the system in terms of like, “How can&nbsp; we allow the declarative nature of assembling the application into a more explicit manner, so that the developers have easier time to understand the code?” And remember, it's not just writing the code but it's also when somebody else comes to a project, they are a new person to a project, they wanna understand how the system is put together. And when they can look at things that are declarative, these are kind of global statements that makes sense all the time. Whereas imperative code only makes sense when you're executing or when the right sense of fields and properties are set in the right particular way. And so they are very localized which you can infer from, from imperative code. And I'm not saying that declarative is be-all and end-all, rather that you need to have a balance of both of them. And currently, we have this very rich imperative world. And we have very, very poor declarative world. So it's not like I'm saying, “Everything should be declarative.” It's rather that there are situations for which declarative hammer is better than the imperative hammer but yet we don’t have the declarative hammer. And this is what we're bringing to the table.** JOE: **Interesting.** JOHN: **We've talked a lot about what AtScript is and where it's coming from, but if somebody wants to get started learning more about it, beyond watching your video up there, is there other plans for putting more material out there for people to get up to speed?** MIŠKO: **There are. Actually Vojtajina has a Playground set up in his repository on GitHub. And in that playground, you grab it and we have to setup the whole thing where we set up the Gulp, the Karma. The whole environment is basically ready to go so you can just start dropping&nbsp; in source code and see how it goes. And speaking about the user Git&nbsp;&nbsp; &nbsp; experience, one of the things we also care about is that we don’t spend a lot of time compiling or rather the transpile step is pretty seamless because it's very important for us that you should be able to just write code, and hit Alt+Tab and hit F5 or Alt+R and be able to see instant response to your code. And so the way the compiler is set up is that it's on profile. It's integrated to karma so you can write you disk with it. And it's all very seamless so that you're not even realizing that it's there. We had Gulp setup to automatically watch the file system and transpilers file by file and so on. So I think the Playground is a good place to start because it kind of gives you the whole experience of which you can have if you have the environment setup properly.** JOHN:**Ooh, you said “Gulp” twice! [Chuckles] I love Gulp.**AARON: **So I'm guessing Angular will have… it will essentially register some annotations that can be used. And then our code we'll be just like, “Hey, we'll annotate a class with a directive annotation.” And then the system would be like, “Okay, Angular will know how to react to that annotation being used.” Is there documentation? Like will it be easy to add annotations or is adding a new annotation ugly?** MIŠKO:**No, new annotations is absolutely trivial. All the annotation is, is a class declaration. As I said, if you say “@foo” it just means there is a class “foo” declared. If you say, @foo (string bar) then it just means that there is a foo, has a constructor that has a method. The constructor takes an argument which happens to be a string that gets saved in for example a name. So, making new annotations is super trivial.**AARON: **Okay. cool. That’s awesome. That's what I wanted to know.** CHUCK: **All right. Well, if we don’t have any other questions, let’s go ahead and do the picks. Go ahead, Aaron.** AARON: **So I'm going to pick “stop complaining about Angular 2.0” because it makes you sound silly.** JOE:**[Laughs] Awesome.**AARON: **That's my pick. Because 2.0 is going to be awesome. Don’t complain about change because change is necessary. Don’t complain about “it's not going to be supported” because it's going to be supported. Stop complaining about 2.0. My pick for the week. People who are not complaining -- that's my pick.** CHUCK: **I just have a really hard time complaining about something that I haven’t seen yet.** JOE: **Is that also your tip for Angular?** AARON: **I think I'm going to double up on that one. If we come back around the tip, that will be my tip as well.** CHUCK: **Yeah, why don’t you go ahead and share a tip with us.** AARON: **My tip is going to be, if you don’t complain about Angular 2.0, that's better than complaining about Angular.** JOE: **More effective.** AARON: **It's my tip.** JOE: **You should write a blog article, “Complaining found harmful.”** CHUCK:**[Chuckles]**AARON:**By the [Ember team?]. [Laughter]**CHUCK: **All right. Joe, what are your picks?** JOE:**My pick is going to be a restaurant we have here. It's called “Blue Lemon.” Awesome restaurant. And I'm not picking it just because the food was good, because the food was really good. But also because I think it's a great example of what design can truly do for your product. When you go in the entire experience [unintelligible], it's very clean. It just makes you feel very comfortable eating their food. From the chairs to the colors -- everything. The way the whole restaurant is designed really does a good job of giving you a great eating experience, and making you comfortable and enjoying your food. So I'm going to pick the restaurant Blue Lemon.**CHUCK: **Cool. We should do like a Utah lunch meet up there or something.** JOE:**Yeah, it's a good one. Definitely a good place to eat. And then my Angular tip will be a new backend as a service that has Angular directives called Back&. They are sort of similar to Firebase, but what’s unique about them is you can actually use a relational database in the backend or a non-relational data store in the backend. They kind of just run an [unintelligible] for you. You can use your own schema. It's a really cool, very interesting backend as a service. And it looks like they are going to be present at ng-conf, which is very cool.**CHUCK: **Very nice. All right, so my pick this week is a book called The Legacy Journey by Dave Ramsey. It really made an impact on me and I really enjoyed it. And I don’t really have an Angular tip this week, so I'm just going to pass on that. Miško, do you have a pick for us?** MIŠKO: **Yeah. I really like this podcast. It's called, let me think… Adventures in Angular. You should really listen to that. That's my pick.** CHUCK: **You should go on that podcast, dude.** MIŠKO:**I should. [Chuckles] should I?**CHUCK: **I hear you know a little about Angular, so I think you'd be a good guest.** AARON: **You just use recursion.** JOHN:**I predict now that anybody who’s watching our podcast or listening to it will actually be listening to it now. [Laughter]**CHUCK: **Awesome. Do you have a tip for us?** MIŠKO: **Tip? If you have something useful to share, please share it constructively.** CHUCK: **You and Aaron must be friends.** JOE:**[Chuckles]**JOHN: **If you want somebody to listen to you, actually, if your goal is just to whine that's one thing. If you want somebody to listen to you, be constructive.** CHUCK: **_But I'm good at whining…_** MIŠKO: **Everybody is good at whining. I'm very good at it too. But if you want it to actually have an effect, to change the world, then have the, for example if you want to whine about the Angular team and you want the Angular team to actually do something different, then give it to us in a very constructive way with which we can use it and in corporate it in some way. We’d love feedback which is not very keen on whining.** JOHN: **Charles, can I do a pick?** CHUCK: **Oh, did I skip you? Go ahead.** JOHN:**I have a pick, which is, I have an ngclean Course that I put out about a month ago for PluralSight. And one of the reason I'm picking this is that there's things that I do in there which [unintelligible] with getting people ready for what's coming with Angular, and kind of using patterns and being consistent is… I think being consistent with the way you go to Angular is important for your team to be able to provide a migration story down the road. So that's one of my picks. And my tip is there's a filter called json in Angular. And I use this a lot to do debugging. When I've got some kind of a binding… you can use Batarang or ng-inspect or other plugins that do this, but if you just do “| json” on your model and then it can print it right to the screen, you wanna get fancy, a lot of times that's just really helpful to see what are my actual bindings [unintelligible]. So it's a really old school way of just putting it out.**MIŠKO: **That was definitely intentional on our part. This was our original debugging story.** JOHN: **Yeah. I love that you guys left that in. I mean, I use it all the time.** AARON: **Pre-Batarang?** MIŠKO: **Pre-Batarang. That's right.** AARON: **Nice.** CHUCK: **Yeah. Got to love the print statement basically for debugging.** JOHN: **Alert!** CHUCK: **Alert! Alert! Before we wrap up I've been working on pulling together a mobile JavaScript roundtable, where we can have that discussion. But we've had to reschedule it. So if you were worried that it was too late, it's not too late. Go to JSPowerup.com or text “MobileJS” to 38470. And we'll get to the details on that as soon as we have them with the rescheduling. So I apologize for that, but keep an ear out. Other than that. Thanks for coming, Miško. We'll wrap up and we'll catch you all next week!** MIŠKO: **It's a pleasure to be here.** _&nbsp;[This episode is sponsored by Mad Glory. You’ve been building software for a long time and sometimes it gets a little overwhelming; work piles up, hiring sucks, and it's hard to get projects out the door. Check out Mad Glory. They are a small shop with experience shipping big products. They're smart, dedicated, will augment your team, and work as hard as you do. Find them online at madglory.com or on Twitter at @madglory.]_****_&nbsp;[Hosting and bandwidth provided by The Blue Box Group. Check them out at bluebox.net]_****_[Bandwidth for this segment is provided by Cache Fly, the world’s fastest CDN. Deliver your content fast with Cache Fly. Visit cachefly.com to learn more.]_**