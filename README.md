# labby-algorithm-experiments
**Research phase of algorithm choice for student to project assignment in Lambda Labs**


# Labby Releases 1, 2 and 3
  
The decision was made to spread the algorithm implementaion for student team assignment across 3 releases for this Labs16 project.
* Release 1. Included an even distribution of students into teams.
* Release 2. Will assign students to teams based upon projectroles and timezone(UTC).
* Release 3. Will optimize for student's top 3 project choices.

## Release 1 is complete.
#### [Sort People evenly into to teams.](https://github.com/Lambda-School-Labs/labby-be/tree/master/Sorting) 

  
## Release 2 due Oct 14
  
:no_entry: Rejected  
### ~~Experiment 1.  Deferred Acceptance Algorithm for hospital/residents problem~~

    
Deferred Acceptance Algorithm for [hospital/residents problems](https://en.wikipedia.org/wiki/National_Resident_Matching_Program#Matching_algorithm) (a.k.a. college admissions problems) with incomplete rank order lists. Finds the college- or student-optimal stable matchings or the related [stable marriage problem](https://en.wikipedia.org/wiki/Stable_marriage_problem). The implementation allows for incomplete preference lists (some agents find certain agents unacceptable) and unbalanced instances (unequal number of agents on both sides).  
    
 ### Sample Request  
      
```
{
"student_prefs": [
  + { ... }
],
"college_prefs": [
  + { ... }
],
"college_capacity": [
  + { ... }
]
}
```
    
Where student_prefs are equivalent to student_prefs and college_prefs are equivalent to project_prefs. And of course, college_capacity would be equivalent to project_capacity.
    
#### ~~Next Steps~~
  
~~Consider implementation of either the Matching Tools API~~ or build a Lambda Labs specific instance of the algorithm.

~~Test Matching Tools API for appropriate response and transfomation given Lambda Labs inputs.~~

------

### Experiment 2.  Greedy algorithm  
#### [Start with Greedy algorithm.](https://en.wikipedia.org/wiki/Greedy_algorithm)

### Assign People by Timezone to Projects given project constraints

```
int Timezone String in UTC
Create timeZoneBuckets floor-divide to combine 2 timezones per bucket
ex: Math.floor(val); where val = timeZone/2;

Define Projects as (??? will this field be available in the db?)
  1. Data Science
  2. Web
  3. Hybrid
  
Project constraints
1. Web and Hybrid projects must have => 1 Web BE
2. No project has more than =< 2 UI/UX
3. No project has more than =< 2 DS
4. Web and Hybrid TeamSize = 6, min = 4, max = 9
5. DS TeamSize = 2
```
```
Initialize People  
Initialize Project  
Initialize ProjectRoles  

Pair<String, Integer> teamMember = Pair.with(projectRole,timeZoneBucket);
or
Pair<String, Integer> person = new Pair<String, Integer>(projectRole, timeZoneBucket);
 
for(Object obj : teamMember) {
    ...Assign to project
}

presuming there exists a function that, given a list of people equipped with projectroles, returns a random
assignment satisfying the people per role-constraints (e.g. 1<=backend, 1<=DS<=4, etc.)

split up the collection of people by timezone bucket, such that you now have one collection for each bucket. 
Then run the random solver function on each timezone bucket


```
### Experiment 3.  Constraint solver
#### [Start with Constraint Satisfaction Problem.](https://en.wikipedia.org/wiki/Constraint_satisfaction_problem)


## Release 3 due Oct 23

Sort People into projects using The Match
