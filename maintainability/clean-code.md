# Clean Code for Research

If you have been programming for more than a month or two (it really doesn't take a lot longer than that), you will probably have run into the issue of trying to fix a bug or add a feature in your code, but realizing that you don't understand anymore what your code is doing. Don't worry, you are not alone! In fact, this issue is so common that people write books about how to overcome this issue. In 2008, Robert C. "Uncle Bob" Martin published *Clean Code: A Handbook of Agile Software Craftsmanship*, which became a classic in software engineering. Martin discusses how to write code that is maintainable, understandable, and extendable. 

You might think that this is mostly important for teams of developers and companies where code needs to be maintained over longer periods of time by multiple people and not your small script that analyses your dataset. This is not the case, however. While it might be true that code developed for research purposes is often only used by one or two researchers for a specific project, it does not mean that the same code wouldn't be useful to someone working on a similar project or that the original author might not need it a few months later for a different dataset. The worse the quality of the code, the harder it gets to reuse and extend it. Furthermore, the worse the quality of the code the harder it is to understand it. The harder it is to understand a piece of code, the harder it is to find and eraticate bugs. 

You might think that the code you are writing for your dissertation project will be done with once you graduate. But what if in your postdoctoral position, you want to extend on your previous research, maybe adapt it? Or maybe someone else is interested in doing so? What, if that code turns out to contain bugs that alter your research results? If you follow good coding pratices early on, the probability that you find flaws in your code decreases, while the ease of adding and reusing it goes up.

In this section, we'll be talking a little bit about the different best practices you can follow to improve your code quality. If you want more details or more recommendations, pick up a copy of Uncle Bob's book (or a different one on clean code and coding best practices)!

## How do you recognize low quality code?

There are many indicators for low quality code, some are less problematic than others. Different "features" of low quality code affect different aspects of maintainability. For instance, badly named variable, methods, or functions affect the readability and understandability of the code, while not following common conventions or recognizable patterns, affect how easy it is to modify it. Duplicate code or spaghetti code (code with no logical structure) increase the probability for side effects and the introduction of bugs. The more experience a developer has, the easier it usually is to recognize low quality code and produce high quality code. However, not all exertise translates when learning a new programming language. There are conventions and features that are specific to a programming language. An expert in one programming language is not necessarily an expert in another language as well.

## Starting with the small things

There are a couple of things, you can easily change when coding that don't require too much extra work or skill. 

### Naming things

A big is how you name your variables, functions, methods, and classes. A good name should be descriptive enough to convey some information about what the named thing is for, but it should not be too long either, since names that are too long can hinder readability. For instance `get_experiment_status()` is better than `get_status_from_experiment_by_date()` (assuming that the function requires a date to be passed as argument). Furthermore, names should be consistent. If you chose `get_status()` in one case, don't choose `fetch_data()` in another; instead call it `get_data()`. Also, make sure to not misspell names, or you won't be able to search for them later on. For example, `get_experment_status()` will not show up when searching for "experiment", making it harder to find any instances in your code that handle experiments.


