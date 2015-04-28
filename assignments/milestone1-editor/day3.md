# Day 3: Syntactic Editor Services

In this lab, you add a pretty-printer and syntactic editor services to your MiniJava editor.

## Overview

### Objectives

1. Extend generated folding rules with hand-written rules. 
You should include only structures, where folding is reasonable. 
2. Integrate generated pretty-printing rules and completion templates into your MiniJava editor.
Improve your syntax definition to support 
  * textual labels in these templates,
  * hiding optional placeholders,
  * multi-line templates and
  * consistent indentation.
3. Extend your editor with additional, hand-written completion templates.

### Submission

You need to submit your MiniJava project with a pull request against branch `assignment3` on GitHub. 
Your GitHub repository contains a step-by-step procedure how to file such a request. 
As part of your submission, we ask you to provide a short explanation of the organisation of your syntax definition in `MiniJava/syntax/README.md`. 
The deadline for submission is October 8, 17:59.

### Grading

You can earn up to 10 points for your folding patterns.
We will take the overall editor experience into account and
we will deduct points for too many (and by this unusable) folding options.

You can further earn up to 70 points for your improved syntax templates.
We will focus on readability of pretty-printed code and completion suggestions and 
on consistent indentations.

Finally, you can earn up to 20 points for hand-written completion templates.

### Early Feedback

This assignment is graded manually. Thus, we do not provide early feedback for this submission.

## Detailed Instructions

### Anatomy of a Spoofax Project

Until now, you mainly worked on files in the `syntax` folder of your project. 
During this lab you will also edit files in the `editor` and `trans` folders.
So this is a good point to talk about the general structure of a Spoofax project.

First of all, every Spoofax project is an Eclipse plug-in project. 
This allows you to deploy your editor as a plugin using the Eclipse update site mechanism. 
Users do not need to have Spoofax installed for using your editor. 
You will find the typical administrative boilerplate code for such plug-ins in files 
`plugin.xml`, `build.properties`, `META-INF/MANIFEST.MF`, and `editor/java`.

The actual language definition is spread over three folders:

* `syntax` contains all syntax definition files, including the main file `MiniJava.sdf3`.
* `trans` contains all transformation files, including the main file `minijava.str`. 
* `editor` contains editor service definition files, including the main file `MiniJava.main.esv`,
  which you have seen already during the last lab.
  
In the `src-gen` folder, you will find files which were generated from your syntax definition. 
For each file `<name>.sdf3`, there are generated files

* `syntax/<name>.sdf`: an SDF2 definition which is equivalent to the SDF3 definition.
* `completions/<name>-esv.esv`: completion templates derived from SDF3 templates.
* `pp/<name>-pp.str`: pretty-printing strategies derived from SDF3 templates.
* `signatures/<name>-sig.str`: signatures derived from SDF3 templates.

You can find more generated files in `editor` and `include` folders:

* `editor/MiniJava-Folding.generated.esv`: folding patterns derived from your syntax definition.
* `include/MiniJava.def`: your complete syntax definition in SDF2.
* `include/MiniJava-Permissive.def`: a permissive version of the syntax definition, which supports error recovery.
* `include/MiniJava.tbl`: the parse table of your language.
* `include/MiniJava.str`: the signature for ASTs of your language.
* `include/MiniJava-parenthesize.str`: strategies to add parentheses to an AST according to the priorities of your language.
* `include/minijava.ctree` and/or `include/minijava.jar`: compiled Stratego code of your language.

### Preliminaries

Before you start with the actual assignment, you should make sure that

1. your syntax definition provides all start symbols needed by your test cases,
2. your context-free syntax is specified in templates of the form

        Sort             = <...>
        Sort.Constructor = <...>
        Sort             = [...]
        Sort.Constructor = [...]

3. your start symbol in `editor/MiniJava.main.esv` is set to `Program` or `Start` so that your editor accepts only complete MiniJava programs. 
4. your Spoofax is up-to-date.

#####Hints: 
For old SDF3 files, with deprecated constructors, you can also apply the ``Lift to SDF3`` builder, under the `Format` menu, to lift your grammar into the new SDF3 style, getting a new file in the ``src-gen/formatted`` folder, with no deprecated constructs.

``Lift to SDF3`` has two different versions: it can **lift productions into templates** or it can **lift them into productive productions**. Therefore, it can be used to generate default templates from regular productive productions in a different file, on `src-gen/formatted`. All .sdf3 files in the ``src-gen`` folder are only temporary and should be manually deleted before building the project.

If you are using Windows, you might not be able to build your project because it locks your `minijava-jar.jar`, forbidding updates to this file. This can be solved by manually deleting it before building the project.

If you were able to update Spoofax, those deletions are automatic.


### Folding Rules

Presentational editor services such as code folding and syntax highlighting are defined 
in `.esv` files in the `editor` folder.
When you build your editor and open a MiniJava file, you can see that the editor provides already some folding points.
These points are syntax-dependent and are specified by folding rules in `editor/MiniJava-Folding.generated.esv`.
All editor services follow the same basic structure: 
they have a derived file (`EntityLang-Folding.generated.esv`) 
and a custom definition file (`EntityLang-Folding.esv`). 
The first file is automatically generated from your syntax definition, each time the project is built.
You can use the second file to customize the editor. 

Folding rules indicate which syntactic constructs can be folded, and take one of the following forms:

    <Sort>.<Constructor>
    <Sort>._
    _.<Constructor>

The `(folded)` annotation can be used for constructs that should be folded automatically:

    _.Imports (folded)

Spoofax uses heuristics to automatically derive folding rules, 
 based on the logical nesting structure in the syntax of the language. 
Currently, it derives folding rules from productions rules with a lexical identifier and child elements.
While not perfect, the heuristics provide a good starting point for a new folding definition. 
Any undesired definitions in the generated file can be disabled 
 by using the `(disabled)` annotation in a custom rule:

    Definition._ (disabled)

You should now specify additional custom folding rules. 
It is important, to include only those structures, where folding is reasonable. 

### Completion Templates

Syntactic content completion provides users with completion suggestions based purely on static, syntactic templates. 
For example

    completion template Statement : "while(true) {}" =
      "while(" <true:Exp> ") " <{}:Statement> (blank)  

is a syntactic completion template for `while` loops. 
Such templates are composed of static strings and placeholder expressions. 
Static strings allow for precise control of the presentation and are enclosed by double quotes. 
They can use `\n` for newlines or `\t` for one indentation level (following the user’s tab/space configuration). 
Placeholder expressions are indicated by angular brackets. 
The editor automatically moves the cursor to these expressions once the user selects a completion proposal, 
allowing the expressions to be filled in as the user continues typing.

Spoofax generates completion templates from `templates` sections in your syntax definition.
You can find these templates in `src-gen/completions/<name>-esv.esv` files. 
Until now, these completion templates are not integrated into your editor.
You can change this, by importing the generated `src-gen/completions/MiniJava-esv.esv` file into `editor/MiniJava-Completions.esv`.
For a successfull build, it is important to avoid any cyclic import in your syntax definition.
After building your project, you can test completion in a MiniJava editor by pressing `Ctrl + Space`.

Typically, your completion templates lack proper indentation and line breaks. 
You can fix this by improving your templates in the syntax definition.
The completion templates follow the indentation and line breaks from the syntax definition.
You can hide particular placeholders from completion templates with a `hide` option or 
change a placeholder label with a `text="label"` option.
Read the [SDF3 documentation](http://metaborg.org/wiki/sdf) on templates and placeholders for more information.

You should improve your syntax definition in order to get readable completion templates with a consistent indentation.
You might read on [indent styles](http://en.wikipedia.org/wiki/Indent_style) for some inspiration.
Finally, you should specify few additional completion templates manually.
This might involve larger code patterns or useful variants of the generated templates.

### Pretty-Printing

Spoofax also generates pretty-printing rules from your syntax definition.
You can find these rules in `src-gen/pp/<name>-pp.str`.

There is already a menu entry named `Format` that uses the strategy `pp-debug` in the `trans/pp.str` file to pretty-print a MiniJava file. However, to add parentheses to your MiniJava program following the priority rules from your syntax definition, it is important that you add the `include/MiniJava-parenthesize` to the imports and also change the strategy `pp-MiniJava-string` to apply the parenthesize strategies to your ast.


    module pp
    
    imports
      ...
      include/MiniJava-parenthesize
      ...
    
    pp-MiniJava-string =
      parenthesize-MiniJava
    ; prettyprint-SDF-start-symbols
    ; !V([], <id>)
    ; box2text-string(|120)

    ...

The strategies from `include/MiniJava-parenthesize` obey the priority rules of your syntax definition.
__You might need to import the generated__ `src-gen/pp/*-pp.str` __files here if your start symbols are not defined in the main SDF3 module__.

In order to test the pretty-print builder, you need to build your project.
Create or open a `.mjv` test file with a valid program, press the down-facing arrow on the right of the `Syntax` button and choose `Format`.
This will apply `Format` to the current file and show the result in a new editor.
