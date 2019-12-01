# lookalive

Lookalive Software is a new way to compose data and code into programs that take arguments, make network and filesystem requests, and return structured data as JSON, XML, or HTML.

It can be used to define API endpoints, perform mail merges, and create document templates for reports and web pages. 
```
cat helloworld.json
{"#!join": [["Hello, ", "#& name", "!"]]}

lookalive helloworld.json name=everyone
{"#!join": [["Hello, ", "#& name", "!"]]}
{"#!join": [["Hello, ", "everyone", "!"]]}
"Hello, everyone!"

cat square.json
"#!product 0 0"

lookalive square.json 12
"#!product 0 0"
"#!product 12 12"
144

cat hypotenuse.json
{"#!join": [[
  "A triangle with side of ",
  "#& side",
  " and base of ",
  "#& base",
  "has a hypotenuse of",
  {"#!sqrt": [[
    {"#!sum": [[
      "#!product side side",
      "#!product base base"
     ]]}
    ]]}
   ]]}
  ]]}
```

It makes use of just four operators:
#! 'do', naming a function to call, passing the local context and any number of arguments
#= 'is', an assignment operator that allows you to name data to be used in subexpressions
#& 'at', an access operator that lets you pull data from the local context
#? 'maybe', an access operator that resolves each argument given until it finds one that is not null

Function calls are black boxes to lookalive and can be written in any langauge. It just needs to accept and return JSON types (boolean, null, numbers, strings, objects and arrays)

