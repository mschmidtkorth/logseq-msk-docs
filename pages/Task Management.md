alias:: tasks

- Logseq has basic task management functionality. You can create tasks, change their status, specify a priority or deadline and query for them ([[queries]]).
- **USAGE**
	- Tasks are added via a `/` [[Command]] or simply by writing one of the keywords (`TODO, DOING, DONE, WAITING, NOW, LATER, CANCELED`) at the beginning of a line
	- _Priorities_ can be set via `/A` or `/B` or `/C` (hover over the priority to quickly switch)
	  #+BEGIN_TIP
	  Priorities can also be used outside of tasks.
	  #+END_TIP
	- _Due dates_ can be defined via `/Scheduled` and _deadlines_ can be defined via `/Deadline`
	- _Dates_ can be specified, however they are simply plain text without additional meaning (however, the `/Date Picker` or `/Yesterday, /Today, /Tomorrow, /Current Time` simplify it)
-
  #+BEGIN_TIP
  Tasks have to be on their own block (not a new line).
  #+END_TIP
- **EXAMPLES**
	- TODO A simple task
	- DONE A completed task
	- WAITING A task I am waiting for
	- TODO A task with a deadline 
	  DEADLINE: <2021-08-01 Sun>
	- TODO A scheduled task 
	  SCHEDULED: <2021-08-01 Sun>
	- DOING  [#A] A high priority task I am working on
	- LATER  [#C] A low priority task I am going to be working on