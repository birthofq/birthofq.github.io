---
layout: post
title: Intelligent Social Matching with Semantic Tagging
---

Anyone who's built social networks or recommendation systems knows the struggle: How do you get the right content to the right people? The traditional approach involves hoarding massive amounts of user data and feeding it into increasingly complex algorithms that then try to guess what people want, or who they want to see or connect with based on their behavior.

After thinking about this problem for a while, I thought to try a radically different approach. Instead of trying to read users' minds through their clicks and scrolls, why not just _ask them_ what they want? My focus in this article is to describe how I'm trying to build (and also how anyone can build) a system that lets people explicitly state what they're looking for in connections, and matches them directly with people who fit those criteria. No algorithmic black boxes, no creepy data collection.

## Sections

- [Capturing User Intent Accurately](#capturing-user-intent-accurately)
- [Semantic Tagging](#semantic-tagging)
- [Intelligent Semantic Tagging System](#intelligent-semantic-tagging-system)
- [Steps in Implementation](#steps-in-implementation)
  - [Design and Implement Tags & Validation Rules](#design-and-implement-tags-and-validation-rules)
  - [Experiment with Direct Tag Matching](#experiment-with-direct-tag-matching)
  - [Add a Semantic Relationship Layer](#add-a-semantic-relationship-layer)
  - [Enhance the Matching System](#enhance-the-matching-system)
  - [User Behavior Learning](#user-behavior-learning)
- [Conclusion](#conclusion)
- [Further Research](#further-research)

## Capturing User Intent Accurately

The tricky part, of course, is figuring out how to let users tell you what they want without making it feel like they're filling out a tax form. How do you capture complex human preferences in a way that's both accurate and painless? From a user experience point of view, how many clicks / actions does it take for a user to give ideally a complete picture of what they want in connections or communities?

This is where semantic tagging comes in. I've been obsessed with this approach lately, and I want to share how it might be an out of the box alternative to the way we design networks that connect people with other people, communities, and ideas.

## Semantic Tagging

At its heart, semantic tagging is beautifully simple: using carefully chosen words to convey maximum meaning with minimum effort.

Let's use a simple example. Say you're building a platform for sports fans, you might have tag categories like "favorite sports," "favorite players," and "favorite coaches." A user could tag their profile with "soccer," "Messi," and "Guardiola," while another might choose "soccer," "Ronaldo," and "Alex Ferguson." The system compares these tags and instantly understands something meaningful about both users and can fairly predict a possibility of a potential connection between them.

Sounds straightforward, right? Well, there's a glaring problem with just relying on directly mapping / comparing tags of users in the network. _Scale_.
Even just taking the sports domain alone, accurately mapping all potential interests would require thousands upon thousands of tags, and without some intelligence behind the system, you'll quickly run into problems like redundancy (is "football" the same as "soccer"?) and data inconsistencies that diminish the quality of connections.

## Intelligent Semantic Tagging System

What we really need is a system smart enough to take two sets of tags and figure out how closely they align, even if they don't match word for word. I've been playing with the idea of building exactly this kind of system, one that helps people form meaningful connections with as little friction as possible.

## Steps in Implementation

### Design and Implement Tags & Validation Rules

First things first, we need to define what tags actually mean in our system. They're not just random words, they're semantic units that carry specific meaning within categories and relationships.

This stage requires spending some time to hammer out validation rules, like character limits (nobody wants to read paragraph-long tags), prohibited symbols (to prevent gaming the system), and duplicate prevention (because having both "football" and "Football" is just annoying).

### Experiment with Direct Tag Matching

Once the foundation is in place, the next logical step would be to design simple user connection rules for the system and then let users start creating tags and tag relationships. When creating their profiles, they could select existing tags or create new ones.

Pro tip: Always show users existing tags before letting them create new ones. This dramatically reduces redundancy and helps build a cleaner dataset.

Once users begin interacting with the system and creating tag relationships, you should start getting ideas and taking note of how people naturally describe their interests. This will help you start thinking about more robust semantic rules for later stages of the system’s development. For instance, you might notice that sports fans often tag specific events (“World Cup 2022”) rather than just general categories (“soccer tournaments”).

### Add a Semantic Relationship Layer

This is where things get interesting. At this stage, you're ready to integrate a lexical database to add more meaningful representations to users' tags. A lexical database at its core is basically an organized collection of words, their meanings, and the relationships between them. Good thing there already exists the perfect lexical database you can implement in this phase - _WordNet_. From the project homepage, the creators of WordNet (folks at Princeton) define it as "a large lexical database of English (where) nouns, verbs, adjectives and adverbs are grouped into sets of cognitive synonyms (synsets), each expressing a distinct concept."

Now you might be wondering, why wait to implement a lexical database when you can just integrate it from the get-go and immediately be able to model user tag relationships and their meanings. Well there are a few reasons I thought about that made me ultimately decide to wait on the implementation:

First, implementing a full semantic layer on day one not only adds more complexity to the development of the system, but it also forces you to build semantic relationships with a lot of guessing and hand-waving alone.

Second, observing how users reason about and choose tags to represent information is relevant in the early stages, to know what tags matter to them and also because user tags might not always directly map cleanly to standardized English words, i.e, slang might be employed more times than expected.

Now after the integration of a lexical database, when someone tags themselves with "football" and another person uses "soccer," the system recognizes they're talking about the same thing (at least in most countries!). This seemingly simple improvement dramatically increases the quality of connections.

### Enhance the Matching System

Next comes the algorithms for calculating similarity between profiles. Not all tag matches are created equal. A direct match on a niche interest (like "underwater hockey") should probably count for more than matching on something broad like "sports."

It might be helpful to implement a weighted scoring system and add crucial feedback mechanisms so when users receive connection suggestions, they can rate their relevance, helping the system learn from its mistakes.

### User Behavior Learning

The longer people use the system, the smarter it gets. For example, if someone consistently connects with others based on their "jazz music" tag but ignores connections based on their "cooking" tag, the system learns to prioritize music-based connections for them.

I've seen this kind of behavioral learning transform a good matching system into an exceptional one. It's like having thousands of tiny personalization knobs that adjust themselves.

## Conclusion

There's still plenty to improve in the system even at this stage. We need granular controls over who sees what in the network (users shouldn't be able to see other users' tags unless they fit the requirements for becoming a viable match) coupled with configurable visibility settings as some tags might communicate information users might deem sensitive. Security is also another big concern as data needs to be properly obfuscated / protected to prevent bad actors from piecing together information about network participants.

Semantic tagging isn't just an interesting concept in itself but I'm convinced that it offers a cheaper, ethical, and more transparent approach to connecting people, ideas and communities in a network as opposed to the black box recommendation algorithms used in popular social media networks. By focusing on explicit user intent rather than inferred preferences, we can build systems that respect user agency while still being incredibly effective at fostering meaningful connections.

I'll write more blogs throughout my experimentation with the idea and document whatever technical or non-technical issues I face during implementation.

If you're building social features into your product, give semantic tagging a serious look, and if you think there are ways to optimize the system even further, or you already went down this rabbit hole and have suggestions or tricks or even warnings about problems that could arise in a system like this, feel free to reach out. I would love to have a chat !
