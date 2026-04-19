# Reference
https://www.elastic.co/docs/reference/query-languages/eql/eql-syntax

# Rule to detect Claude tool usage on accept

```
sequence by prompt.id
[ any where event.name == "user_prompt" ]
[ any where event.name == "tool_decision" ]                       
[ any where event.name =="tool_result"]
```

Building block rule to detect tool usage, roll this up into an actionable alert on tools + tool usages we care about.
