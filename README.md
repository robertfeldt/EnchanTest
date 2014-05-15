# EnchanTest - automagical sw testing

(Currently, EnchanTest is just getting started; the following is a manifesto of where we are going rather than a good description of the current state... :( )

EnchanTest helps you get the most out of your software specification and testing. It is a framework where you can:

* Specify software behavior by examples, mainly using natural language
* Specify expected behavior only once, then EnchanTest does it for you
* Do high-level testing (system and acceptance testing) as well as low-level testing (integration and unit)
* Test software regardless of programming language or implementation
* User multiple, lower level testing tools and technologies and "glue" them together to achieve your testing goals
* Explore visually and statistically how your testing and sw quality evolves over time

EnchanTest tries to be a technology-neutral as possible. For high-level testing we use Sikuli to test the software visually, through its user interface. The benefits are that the system is exercised in a manner that is as close to how a human would do it as possible. For lower-level testing with a specific programming language or technology you may need a specific plugin. Currently there are plugins for Ruby and Julia but more are planned and will be added over time.

The development of EnchanTest is supported by award-winning software testing research funded through the Swedish research agencies Knowledge Foundation (through the project TOCSYC) and Vinnova (through the projects TIES, AVSATS1 and AVSATS2). It is the integration of many years of research into testing, machine learning and search-based sofotware engineering into one easy-to-use framework.


## Example of usage


### Starting EnchanTest

After installation you start EnchanTest with the command:

  enchantest

This will start EnchanTest in the current directory and enable automated testing by default. It will also print a URL. Open a web browser and go to that url and you can then access EnchanTest through its own web front/app.

### Adding a specification

Click on "Add spec" and you will get to a fresh specification where you can fill in:

* Title - Each spec can have a title that briefly describes it
* Description - A natural language description of the behavior for this spec
* Tags - A spec can have one or more tags so that you can later select subsets of your specs to check
* Examples - Specific examples/variants of this spec that should be tested
* Translation - For low-level testing you can specify in detail how to translate this spec into test code

Only title and description are mandatory but we recommend that you add tags so that you can easily select subsets of specs to be tested. Tags can be hierarchical such as "feature/Radar/UnitInfo" and "GUI/Visual" and can later be matched with simple globs and regexps like "feature/Radar/*" or "*/Visual". We recommend that you try out a "Specification by Example" (tagged "Type/SbE") style of writing specs where the description can have variables which are then linked to examples.

### Running tests

When you have added at least one specification you can then run it. Just press "Run" on the main EnchanTest dashboard page. Your specifications will also be automatically executed if they change or if the software being tested has changed. EnchanTest will automatically collect information about file and spec changes so that it can better prioritize your testing.

As soon as some tests have been executed the main EnchanTest page will show test results as they pour in. The web app is dynamically and asynchronously updated and tries to optimize the feedback it gives you so that you get the most information the quickest.


## Installation

EnchanTest can currently only be installed from the command line, as a Ruby gem:

  gem install enchantest

## Requirements

EnchanTest is based on the following technologies:

* [Ruby](https://www.ruby-lang.org/en/) - for gluing things together and for the command line tools
* [Julia](http://www.julialang.org) - for our own machine learning and testing tools
* [R](http://www.r-project.org/) - for accessing lots of existing statistical analyses and tests (that are not yet available in Julia)
* Javascript, HTML and CSS - for implementing the web front end
* [D3.js](http://d3js.org) - for interactive graphics and presentation of results in the web front end
* [ElasticSearch](http://www.elasticsearch.org/overview/elasticsearch/) - for database handling and quick, free-text search and matching of messages
* [Sikuli](http://www.sikuli.org/) - for visual testing of any software with a GUI
* [GodelTest](http://www.robertfeldt.net/publications/feldt_poulding_2013_finding_test_data_with_specific_properties.pdf) - our search-based software test automation tool
* Forte - our own R package for analysing test outcomes and optimizing your (re-)testing

Through specific plug-ins EnchanTest can also do low-level unit testing for specific languages. 

### Currently available plug-ins:

* Julia

### Planned plug-ins (in rough order of priority):

* Ruby/AutoTest - to interface with Ruby's standard autotest unit testing framework
* CSV
* C# / DotNet
* TTCN-3
* Java
* C
* Python

The CSV plug-in can be used to read in old test runs that have been saved in CSV (comma separated value) files.