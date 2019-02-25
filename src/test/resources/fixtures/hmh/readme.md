# HMH Caliper Events V1.1

All json files located under the `<caliper producer dir>/released` directory where `caliper producer dir` is RIMI, Ren Learning, Assessment Service etc... are currently supported by Ed Analytics, meaning all attributes are collected.  
Anything outside of `released` directory may only be partially supported.

# Development / Release Directories
* `development` - any event in here is not signed off and is under going changes.
* `released` - any event in here is signed off and currently supported by Ed Analytics.


# How to get Ed Analytics to support a Caliper Event?
1. Firstly because github.com/hmhco/caliper-java generates the json for the Caliper Event json files in this repo,
ensure you have opened a PR in github.com/hmhco/caliper-java for your new Caliper Event. 
2. Using the json generated from the previous step, create your Caliper Event json in the `development` directory.
3. Open a Pull Request for your event in `github.com/hmhco/caliper-java`   
    AND   
    a corresponding Pull Request for your event here   
    AND 
    notify `@here` in the Slack channel `#edanalytics-dev` of both PRs.
4. Once Ed Analytics approves PR, files in both repos will be moved to their corresponding `released` directories and merged.

# Caliper Event Reference Help:
## Common Event Data amongst all event types
  * actor - In 99% of use cases this represents the person that Caliper Event is about. i.e. the Student/Teacher etc...
  * actor.id - User Id (must be from HMH IDS database)
  * edApp - the entity who created the caliper event
  * membership - the membership block is associated with the actor.
  * membership.id - random guid
  * membership.organization.id - the school ref id of the actor (must be from HMH IDS database)
  * membership.organization.subOrganizationOf.id - the district ref id of school ref id (must be from HMH IDS database)    "organization":{
  * membership.roles - the actor roles
  
## Graded Events  
  * object.id - last attempt id
  * object.assignee - same as actor id - the user
  * object.assignable - the assessment id  
  * object.duration - duration for object in ISO 8601 duration format
  * generated.id - a random guid to uniquely identify the generated block within the event
  * generated.type - Score - the type of generated entity
  * generated.name - (Optional) The name by which the score can be called. E.g. For Star scores from Ren Learn, they set this field to 'star'.  
  * generated.attempt - same as object.id - the last attempt id
  * generated.scoredBy - the entity that generated the score
  
## Assessment Started
  * object.id - assignment activity id

## Assessment Item Started  
  * object.id - the actor's item id
  * object.isPartOf.id - object id specified in the AssessmentStartedEvent
  * object.maxScore - for practice questions set this to zero
  * generated.id - the attempt id that was made against the object.id
  * generated.type - Attempt - the type of generated entity
  * generated.assignee - same as actor.id
  * generated.assignable - same as object.id
  * generated.isPartOf.id - previous attempt id (first time round this won't exist)
    
  * generated.attempt - same as object.id - the last attempt id
  * generated.scoredBy - the entity that generated the score
  
  
    

