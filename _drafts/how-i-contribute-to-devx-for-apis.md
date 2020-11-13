TODO add frontmatter

respond to this:

https://idratherbewriting.com/learnapidoc/devx-usability-examples.html

random thoughts:

so we had a domain model overhaul. We had to competing concepts -- feature flags and A/B tests. their relationship was unclear, but we made it clear by making flags the root concept, and experiments a type of flag rule. There were two parallel efforts, one in the API and one in the UI, but it turned out they weren't clearly coordinated

what i CAN do:
- getting involved early by reading specs, design docs, etc, notice discrepencies between terminology or concepts, and get people talking early on to resolve them.   
    - ask questions: why does this payload have a rule type field, but that doesn't? Wouldn't including rule type over in this payload let beople avoid hardcoding rule IDs, and wouldn't that be a convenience to them?
    - we need more symmetricy between "sendEvent" option parameter vs returned "decisionLogged" field since once is the result of the other. And 'send" isn't consistent with our SDK internal termonology which is "dispatch event" and which shows up in our docs. (I made suggestions, and the ultimate winners weren't what I suggested but which made sense: "dispatchEvent" and "eventDispatched"
    - why are we exposing experimentKey or flagKey in the API when the new UI will be focused almost esclusively on experimentKey? Supporting experimentKey as a first-class 'thing' in all our call signatures will be really awekard -- it'll make a corner case overexposed and over-documented. Can we remove support for experimentKey? (I got support from this from product managers, and ultimately it was removed)
   


what I CAN'T do:
  - this payload seems convoluted...but it took another person to make an actual untangling suggestion
  - make the big changes (b/c I don't always understand the technical constraints involved). for example, going from decide(key_flag, user_id) to user.decide(key_flag) was an obvious improvement in our API, but I didn't know enough about threading, user persistance, or the typical use-case for how many users a server vs client might be handling to have made such a suggestion...I could only see that it was an obvious improvement as soon as someone suggested it.
