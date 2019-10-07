# labby-algorithm-experiments
**Research phase of algorithm choice for student to project assignment in Lambda Labs**


# Labby Releases 1, 2 and 3
  
The decision was made to spread the algorithm implementaion for student team assignment across 3 releases for this Labs16 project.
* Release 1. Included an even distribution of students into teams.
* Release 2. Will assign students to teams based upon projectroles and timezone(UTC).
* Release 3. Will optimize for student's top 3 project choices and teamMember preferences.

## Release 1 is complete.
#### [Sort Students evenly into to teams.](https://github.com/Lambda-School-Labs/labby-be/tree/master/Sorting) 

  
## Release 2 due Oct 14
  
### ~~Experiment 1.  Deferred Acceptance Algorithm for hospital/residents problem~~  
:no_entry: Rejected  RC2 doesn't provide any choice by the student.

    
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

### Assign Students by Timezone to Projects given project constraints

```
Timezone String in UTC

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
Initialize ProjectType
Initialize ProjectOrder

Pair<String, Integer> student = Pair.with(projectRole, timeZone);
or
Pair<String, Integer> student = new Pair<String, Integer>(projectRole, timeZone);
 
for(Object obj : student) {
    ...Assign to project, given projectType
    if studentUnassigned {
      List<projectOrder> reverseOrder = projectOrder.ascending - 1
    }else{
      return projectAssignment;
}

presuming there exists a function that, given a list of students equipped with projectroles, returns an 
assignment satisfying the student per role-constraint (e.g. 1<=backend, 1<=DS<=4, etc.)

with student object sorted by timezone run function against collection finding best match given timezone  
priority. Start at the top for each project.

presume there are unassigned students after first pass, and each project has been assigned an int,  
projectOrder, descending. Then assign remaining students to projects in ascending projectOrder to  
ensure nearest timezone.

if students remain unassigned, throw exception and report for human intervention
```

-------

### Experiment 3.  Constraint solver
#### [Start with Constraint Satisfaction Problem.](https://en.wikipedia.org/wiki/Constraint_satisfaction_problem)

Use case applicable will maximize resource allocation and also minimize timezones.

#### PROBLEM (what)

n Students assigned to n Projects  
Each Project requires certain ProjectRoles and teamSize  
  <sub>  &nbsp;&nbsp;&nbsp;&nbsp;1. Web and Hybrid projects must have => 1 Web BE  
    &nbsp;&nbsp;&nbsp;&nbsp;2. No project has more than =< 2 UI/UX  
    &nbsp;&nbsp;&nbsp;&nbsp;3. No project has more than =< 2 DS  
    &nbsp;&nbsp;&nbsp;&nbsp;4. Web and Hybrid TeamSize = 6, min = 4, max = 9  
    &nbsp;&nbsp;&nbsp;&nbsp;5. DS TeamSize = 2  </sub>  

Objective: assign students to projects while minimzing timeZone deltas

#### PROBLEM RESOLUTION (how)

Find a solution that defines a project for each student.
Find an optimal solution that minimizes timeZone for optimalization of team assignment.
Add other optimalizations easily in future releases, such as, student affinity

#### MODEL

Code snippet or pseudocode to be added

#### VARIABLES

Code snippet or pseudocode to be added

#### CONSTRAINTS

Code snippet or pseudocode to be added

#### SOLVER

Code snippet or pseudocode to be added



#### RULES
```
RULES EXAMPLE 1

Domain:
- Student
   - ProjectRole
   - ProjectChoice //future release
   - Affinity with teamMember: [None, negative, positive] //future release
- Project
   - Type: [DS, Web, Hybrid]
      - Project type impacts teamSize
   - Required ProjectRoles
       - Student project choice impacts team assignment //future release
   - teamMember
      - Student affinity impacts team assignment //future release
      
 Constraints:
 - ProjectRole (HARD): Project.requiredRrojectRoles === Student.projectRole
 - Minimize timeZone delta (SOFT 0)
 - Team size (SOFT 1)
```

```
RULES EXAMPLE 2

Reverse priority of constraints with timeZone as the HARD
and projectRole as the SOFT
```

-------

## Release 3 due Oct 23

UNKNOWN - dependent upon Release 2
