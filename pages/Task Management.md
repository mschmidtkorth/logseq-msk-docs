alias:: tasks

- Logseq has basic task management functionality. You can create tasks, change their status, specify a priority or deadline and query for them ([[queries]]).
- **USAGE**
	- Tasks are added via a
		- `/` [[Command]], or
		- by simply writing one of the keywords (`TODO, DOING, DONE, WAITING, NOW, LATER, CANCELED`) at the beginning of a line, or
		- by pressing `Cmd+Enter` to cycle through the status.
	-
	  #+BEGIN_NOTE
	  Tasks have to be on their own block (not a new line).
	  #+END_NOTE
	-
	  #+BEGIN_TIP
	  Logseq offers two types of task workflows and state transitions: LATER -> NOW -> DONE and TODO -> DOING -> DONE. Your preferred workflow can be defined in _[[Settings]] > Preferred Workflow_ 
	  #+END_TIP
	- _Priorities_ can be set via `/A` or `/B` or `/C` (hover over the priority to quickly switch).
	  #+BEGIN_TIP
	  Priorities can also be used outside of tasks.
	  #+END_TIP
	- _Due dates_ can be defined via `/Scheduled` and _deadlines_ can be defined via `/Deadline`.
	- _Dates_ can be specified, however they are simply plain text without additional meaning (however, the `/Date Picker` or `/Yesterday, /Today, /Tomorrow, /Current Time` simplify it).
	- Tasks can be _repeated_ by selecting so in the date picker.
	- You can track the time spent on tasks by enabling _[[Settings]] > Enable Timetracking_. This will record the time between any not-done task and when the task was done.
- **EXAMPLES**
	- TODO A simple task #sample
	- DONE A completed task #sample
	- WAITING A task I am waiting for #sample
	- TODO A task with a deadline #sample
	  DEADLINE: <2021-08-01 Sun>
	- TODO A scheduled task #sample
	  SCHEDULED: <2021-08-01 Sun>
	- DOING  [#A] A high priority task I am working on #sample
	- LATER  [#C] A low priority task I am going to be working on #sample