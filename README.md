```python
# get maya commands library
from maya import cmds
```



```python
# you can find documentation of the function
help(list)
# list all the functions of a
a = list()
dir(a)
```



[cmds.ls(selection=True)] [len()] [cmds.ls(dag=True, long=True)()] [list.sort(key=len, reverse=True)] [string.split("|")[-1]]

```python
selection = cmds.ls(selection=True)

if len(selection) == 0:
    '''
    dagObjects(dag): get objects that are listed in the outliner and none of the hidden 	objects
    '''
	selection = cmds.ls(dag=True, long=True)

# 按长度排序，并且反转
selection.sort(key=len, reverse=True)
'''
go through every item inside selected items, split them by "|" and take the very last object
'''
for obj in selection:
    shortName = obj.split("|")[-1]
    
    children = cmds.listRelatives(obj, children=True, fullPath=True) or []
```

