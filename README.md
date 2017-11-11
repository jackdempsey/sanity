# sanity
Don't let your distributed production system drive you insane. Sanity combines ideas from `github/scientist` and `rspec` to 10x your confidence in your distributed, asynchronous production systems.

## problem
How do you know something has happened? 

In development, you look at a dashboard, query your database, maybe refresh a page.
In a test environment, you have expectations that programmatically run and confirm.
In a real work, distributed, async production environment you.....wait for the Big 5 Metrics dashboard to show a dramatic crash in revenue?

## Solution
Sanity is a system for getting back that confidence you had in production before everything traveled through queues and (maybe) landed on a worker box. Unsure if your code is actually calling that reindex method? Want to prove to the front end team that the data's not getting lost on your side? Install some Sanity.

## Design Considerations

### what are the things I want to ensure:
1. that some code is called
2. as many times as i expect
3. that it received and returns what I expect
4. that something changes as a result of it running
  a. I'll need both pre and post numbers
  b. or a guaranteed way to call them and inspect their difference

### how do i ensure the above (in order)
1. add code in the code i'm talking about to log that it was called; alternatively override the method and automatically log things. this lets you add just one expectation and one code change but then also messes with aliasing etc
2. do #1 then sum and compare
3. alias method, log return value, then return?
4. 


### where might I care (both about setting the expectation and checking it)
1. in the same code area
2. in different places

### Time it's not always about i expect this to happen, run this code, did it happen
it could be one sided checks: "i expect if I'm here this has already happened" (you can always expect something from the past

it's both arrows of time; it is time T. Later at time T1 I expect this to be true.
but also It is time T1. I expect something has happened by now. Here's how to query and see if that is true.

### what is the data I need to do this
for scientist there was a name of an experiment, pre and post conditions (values in ruby to compare), results, cleaned results

can I use a blob of json fired off?

### User Stories
As a Catalog engineer, I want to make sure the prices I get from inventory files end up as the prices in the database.

As a Catalog engineer, I want to make sure that ever item I think I'm reindexing gets reindexed. 

### Challenges

#### How is this any different from just logging things? What's better?
1. automate checking so you don't have to
2. wires it all together. it's not really enough to log X over here and Y over here and be done (why??)
3. automatic logging of data makes it easy to visual and track over time
4. gives structure for how to tie checks together

## Inspiration
clojure/spec
rspec
github/scientist
