+++
title = "Troubleshooting CloudFormation"
weight = 40
+++

This topic describes some of the issues that can happen with CloudFormation. It also talks about how you can detect these issues, and offers some ways to fix the issues.

## Invalid JSON
JSON must be syntactically valid. For example, if you don't type in the final `}` character in a template, the `euform-create-stack` command returns an error message. 

```bash
euform-create-stack: error (ValidationError): Unexpected end-of-input: 
expected close marker for OBJECT (from [Source: java.io.StringReader@56b3916d; 
line: 1, column: 0]) at [Source: java.io.StringReader@56b3916d; line: 38, 
column : 849]
```

If you see an error like this, there is most likely something syntactically wrong with your JSON template. Some editors can detect things like unbalanced parentheses, but in the worst case you can paste your template into this URL [http://jsonparseronline.com/](http://jsonparseronline.com/) and it will help you find syntax errors. 


## Invalid Argument
If you try to create, for example, a stack that already exists, you will get a simple error message. 

```bash
euform-create-stack: error (AlreadyExists): Stack already exists
```

## Invalid Reference
If you use an invalid reference to, for example, a resource that doesn't exit, Eucalyptus returns a simple error message. 

```bash
euform-create-stack: error (ValidationError): Template format error: Unresolved resource dependencies [MySecurityGroup2] in the Resources block of the template>
```

## Complex Errors
Not all errors are simple. We recommend that you use `euform-describe-stacks` (or `aws cloudformation describe-stacks`) and `euform-describe-stack-resources` to determine the current state of the stack. If there's an error, it will usually be shown in the `euform-describe-stack-events` output. Otherwise, you will have to dig into the *cloud-output.log* file for further information. You can also manually delete resources if they are causing issues. If a `euform-delete-stack` fails, you can delete the offending resource and try again.

