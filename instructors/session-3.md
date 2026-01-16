

# Session 3


## Required Self-Study

- [Using AI within Pipelines via `ellmer`](../episodes/ai-pipelines-ellmer.md)
- [Understanding and Setting LLM parameters](../episodes/llm-parameters.md)



## Session Plan


### AI-usage via ellmer

- ? `ellmer` installed and working? chat-check, see material !

- ? What is a major problem, when using `ellmer` via map?
  - Advantages of "aggregated calls"
  - idea of batch processing

- GROUP: 
  * ! identify at least 4 reasonable use cases for AI-calls via `ellmer`!
  * ? what kind of tasks are not suited for AI-calls or can be done otherwise?
  * ? what are drawbacks/cons of AI-usage in data processing?

- ? Thoughts about reproducability and reliability?
- ? How to guide the reliability of an LLM?
  - discussion of 
    - [*temperature* parameter](https://www.vellum.ai/llm-parameters/temperature)
    - *top p* = top tokens with cumulative probability up to *p* (lower = more restrictive)
    - *top k* = *k* highest tokens (lower = more restrictive) (not always supported)
  
- ? and energy consumption?!?

- ? AI vs. human in data processing... whom to trust? when and why?

- Best practice discussion/summary


### Reproducability

- ? why care about reproducability?

- discussion of pseudo randomness and seeding in computers
  - general problem of randomness in data processing

- GROUP: local LLMs vs. API-based LLMs
  - ? what are pros and cons of local vs. API-based LLMs?
  - ? how to control reproducability in both cases?
  - ? what seems most appropriate for research?

- ? How to document LLM usage in data processing?
- Best practice discussion/summary



### Closing Discussion

- ? What are your major take-aways from this session?
- ? What topics would you like to explore further?
- ? Any open questions?
- Feedback collection


