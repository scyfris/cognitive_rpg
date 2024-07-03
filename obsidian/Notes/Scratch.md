2/5/24

Something that's been bothering me is the quality of our pixel art, and how to speed things up .  IT will take a lot time to get all animations and such, unless we go really low resolution which might not be that appealing.

I found this:

https://www.reddit.com/r/PixelArt/s/Q6mm5MNThI

Doing things in blender does offer the ability to speed up things, especially animation.
One other thing to note is there are ALOT of models online for various things (desks, chairs, etc) - we can trasnfer these into our own style , but we don't have to model from scratch.  We could also use these as reference.

Just an idea.

---

```
[Questline]
	[key]mq[/key]
	[title]Main Story[/title]
	
	[Quest]
		[key]scene1[/key]
		[title]Get ready for the day[/title]
		
	    [Task]
	      [key]make_coffee[/key]
	      [title]Make coffee[title]
	      [sequential]True[/sequential] // determines if GetPreq() returns the previous task or nothing.  If True, GetPrereq() returns previous task.  If False, returns NULL and is completely indepedent.
	    [/Task]
	    
	    [Task]
	      [key]check_emails[/key]
	      [title]Check emails[title]
	      [sequential]True[/sequential]
	    [/Task]
	    
	    [Task]
	      [key]get_dressed[/key]
	      [title]Get dressed for work[title]
	      [sequential]True[/sequential]
	    [/Task]
	    
	[/Quest] 
	  [Quest]
		 [Task]
		 [Task]
		 ...
	   [/Quest]
[/Questline]
```

Dialogue files:
mq_scene1 -> main dialogue file for scene 1 (quest 1)
	Quest is given after the initial dialogue. 

UI markers -> check for task name
```
	task full key = <questline key> + "_" + <quest key> + "_" <task key>
```

Quest dialogue
```
	dialogues can check for task completion
		QuestMaster.TaskInProgress(<task name>)
		QuestMaster.TaskCompleted(<task name>)
		QuestMaster.QuestCompleted(<quest name>)
```


Tasks can have the following status
```
TASK_IN_PROGRESS -> If the quest containing this task has been given and the task is not complete.
TASK_COMPLETE -> If the task is complete.
```

Checks on ql, q, and tasks.
```
	QeustMaster.TaskCompleted(<task name>) => Returns True if the corresponding task name in the save file is set as TASK_COMPLETED

	QuestMaster.TaskInProgress(<task key>) => Returns True if the corresponding task name in the save file is set as TASK_IN_PROGRESS

	QuestMaster.QuestCompleted(<quest name>) => Returns True if all tasks under the quest in the save file have bene marked as COMPLETE.
	
	QuestMaster.QuestInProgress(<quest name>) => Returns True if QuestCompleted() == False AND at least 1 have the tasks in the Quest are marked as IN_PROGRESS.
	
	QuestMaster.QuestlineCompleted(<questline name>) => Returns True if all Quests are complete (QuestComplete(<questname>) returns true for all quests.
	
	QuestMaster.QuestlineInProgress(<questline name>) => Returns True if QuestLineCompleted() returns False AND at least 1 Quest HasQuest(<quest name>) returns True.
```

Giving quests
```
QuestMaster.QuestGive(<quest name>) => This gives the player the quest.  This is implemented as just setting all the tasks in the quest as TASK_IN_PROGRESS in the save file.  From that point oon, all relevent QuestMaster functions checking tasks, quests, etc will return sane values.
```

In code:
* Partial Key -> Just the key of the quest, qk, or task without others
* Full Key ->
* ```
```
	** Full Questline Key : <questline partial key>
	** Full Quest key: <questline partial key>_<quest partial key>
	** Full Task key: <questline partial key >_<quest partial key>_<task partial 
```
