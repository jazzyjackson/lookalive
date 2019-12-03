# lookalive

'lookalive' is a new method for composing programs that return structured data as JSON, XML, or HTML.
It can be used to define API endpoints, perform mail merges, and create document templates for reports and web pages. 

Because lookalive programs are valid JSON files, you can write the structure that you want and weave in the results of function calls embedded in this structure. This can make it easy to know what a program does by glancing over the code, without interpreting traditional source code line by line trying to keep track of what will end up happening.

The shear amount of bracket and curly-brace syntax may look overwhelming (it is LISP-y in that way), but a development environment that renders all of that structure into an easy-to-manipulate visual program tree is in the works.


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

