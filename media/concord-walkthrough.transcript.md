# Concord: designing data standards together

## Welcome (0:00)

Hi, and welcome to Concord. It's a prototype from the ODI's Standards Hub for designing data standards together, in the open.

In about nine minutes I'll show you what Concord is for, how a standard grows from a conversation into a published release, and then the part I enjoy most: building an app against one of these standards with a coding agent.

This is the hub. Each card is a standard that a community looks after. We'll follow the volunteering standard, which describes volunteering opportunities, the organisations that offer them, and the people who give their time.

## What Concord is for (0:36)

Every standard here is an ontology, written in OWL, the web's language for describing concepts and how they relate.

Concord has three goals. The first is rigour. Standards are strict OWL, a reasoner keeps them logically consistent, and Concord checks them against the FAIR principles: findable, accessible, interoperable and reusable. So data built on them is easier to find and combine.

The second is that the people who use a standard should shape it, whether they join a call, talk to an interviewer, or are a coding agent working on someone's app.

And the third is governance without endless meetings. Every change is classified, checked and reviewed asynchronously, under rules the community agrees for itself.

## Exploring a standard (1:25)

Let's look inside. The Browse page shows the classes and their relationships, so you can get a feel for the model before you read a line of code.

Source and export shows the same ontology however you need it. Turtle is the canonical form, and it's what we keep in git.

LinkML is there too, for teams that generate schemas and documentation from one model.

And there are SHACL shapes, generated from the OWL. SHACL is the W3C's language for describing the shape data should have, so apps can validate their data against the standard.

## Readable shapes (2:02)

The shapes are also available in SHACL compact syntax, which is far easier to read. Each shape fits on a few lines.

## Classes for developers (2:11)

And for developers there's a Classes format: JavaScript and TypeScript classes generated from those shapes, which an app can import straight from the standard's address. We'll use them in a moment.

## Querying in the browser (2:23)

On the Query page you can ask questions of the ontology in SPARQL. The query engine is compiled to WebAssembly and runs right here in your browser.

If you'd rather not write SPARQL, describe what you want in the chat beside the editor. It writes the query for you to check and run, and each follow-up message refines it.

## Gathering requirements (2:44)

Changes start with requirements. People describe how they'd use the standard as use cases, with competency questions: questions the ontology must be able to answer, like which opportunities suit someone free on weekends.

Requirements also come from meetings. You can upload a Google Meet transcript. And with a meeting-bot provider configured, you can invite a bot that joins the call, takes notes, and asks clarifying questions in the chat.

## Changing the standard (3:13)

Requirements become change requests. The model never writes the ontology directly. It proposes terms, and Concord compiles them into validated edits.

Each change is classified as a patch, a minor change or a major one, using explicit versioning rules. Then it's validated: strict checks, the reasoner, a check for alignment with FAIR principles, and any competency tests that have been supplied.

Finally it's reviewed under the standard's governance policy. That might mean a steward's sign-off, a review period where silence means consent, or a formal vote.

The policy is the community's choice. Start from a template, like lazy consensus or a W3C-style working group, and tune it: who signs off, how long reviews run, and what's automated.

Approved changes go into releases. Each release gets a proper semantic version, every format, and for major versions, a migration script.

## Building with the standard (4:16)

So that's the standards side. Now let's put on a developer's hat.

This is Helping Hands, a small web app that lists volunteering opportunities near you. Its data is described with the volunteering standard.

Here's the interesting bit. The app doesn't hand-write any code for the data model. It imports JavaScript classes straight from the standard's web address, and Concord generates those classes from the standard's SHACL shapes.

## Connecting Claude Code (4:45)

To work on the app, I'll use Claude Code on the web, connected to Concord through MCP, the Model Context Protocol: an open standard for plugging tools into AI agents. Connecting it is one custom connector, with Concord's address.

One note before we start. The Claude Code session you'll see is a scripted demonstration. Its calls to Concord are real, but the agent's replies and the code it writes were prepared in advance.

## Signing in (5:13)

The first time Claude Code uses it, a browser window opens so you can sign in to the hub. And the Connect page has one-click install links for other agents too, like Codex and Cursor.

## A feature the standard can't describe yet (5:27)

Here's the feature. Volunteers want to log the hours they've given, and organisers want to see the total for each opportunity.

I'll ask Claude Code to build it, using the volunteering standard for the data.

Before writing any code, Claude checks the standard. It searches for anything about hours, and finds hours per week on time commitment.

But that's the time a role expects, not time someone actually gave. So the concept we need is missing from the standard.

## A fork of my own (5:58)

In the past, that's where you'd stop and wait for the standard to change. Instead, Claude creates a fork: my own development copy of the ontology, right on the hub.

It adds the missing class to the fork, a volunteering activity, with the hours given, who gave them, which opportunity, and the date. The new terms keep the standard's own namespace, so my data stays valid when they land upstream.

And here's the fork in the hub, next to the standard it came from, with its changes and a link back to the main ontology.

Claude also proposes the change upstream, so the community can consider it. Nobody has to wait for anybody.

## Classes straight from the fork (6:40)

The fork has its own address, and it serves generated classes just like the main standard does. Here's the module, with a class for the new volunteering activity.

## Building the feature (6:50)

So the only change Claude needs to make to use the new concept is the import line. It now points at my fork.

Then it writes the feature itself: reading activities through the generated classes, and adding up the hours for each opportunity.

## The finished feature (7:06)

Back in the app, each opportunity now shows the hours volunteers have given, and there's a running total for me at the top.

Let's log a couple of hours at the food bank. And the totals update straight away.

## Meanwhile, on the hub (7:20)

Meanwhile, my proposal is on the hub like any other change request. Concord has classified it as a minor change, because it only adds terms, and the validation has passed.

## Autopilot for app owners (7:31)

Other app owners don't need to read every proposal either. They can connect their app's tests to Concord and switch on autopilot.

Now, whenever a change is proposed, their tests run against it. If nothing breaks, Concord votes yes on their behalf. In this demo the test run is simulated: we report a passing result to Concord ourselves.

## Back to the main standard (7:58)

A few days later, the change has been approved and released in a new version of the standard.

At the start of my next session, Claude checks my forks, sees that the volunteering activity is now in the released standard, and offers to move me back.

It's one line again: the import goes back to the main standard. The app works exactly as before, and my fork has done its job.

## Wrapping up (8:24)

That's Concord. Rigorous, open standards that grow from the people who use them, with governance that doesn't need a meeting, and room for developers to keep building while the standard catches up.

It's an early prototype, and we'd love your feedback. Try it yourself at the link below, and thanks for watching.
