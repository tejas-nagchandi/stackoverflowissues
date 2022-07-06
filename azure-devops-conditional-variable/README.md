# azure-devops-conditional-variable
This repo is created for https://stackoverflow.com/questions/69652609/azure-devops-yml-pipeline-if-else-condition-with-variables/70184550?noredirect=1#comment124097630_70184550


## Test 1:
Value of variable is true

![image](https://user-images.githubusercontent.com/76960497/144466438-d2259168-1694-450f-9dab-96f90ae61b27.png)

### Expected Result: 
value1 should be the outcome

### Original Result:
![image](https://user-images.githubusercontent.com/76960497/144466504-4d1acd66-d55d-4d7c-956b-c7bff8891333.png)

## Test 2:
Value of variable is false

![image](https://user-images.githubusercontent.com/76960497/144466630-808a0b81-6db3-4d4c-b16f-c8f34eb1dcd9.png)

### Expected Result: 
value2 should be the outcome

### Original Result:
![image](https://user-images.githubusercontent.com/76960497/144466819-6ddf9ab6-54bb-4d4e-ab5e-fa8e448777a9.png)

## Reason why if condition was not working with `${{ if condition }}:`
**Note the syntax `${{<expression>}}` for compile time and `$[<expression>]` for runtime expressions.**

https://docs.microsoft.com/en-us/azure/devops/pipelines/process/expressions?view=azure-devops

## How replace works?
Reference: https://docs.microsoft.com/en-us/azure/devops/pipelines/process/expressions?view=azure-devops

### replace
Returns a new string in which all instances of a string in the current instance are replaced with another string

Min parameters: 3. Max parameters: 3

replace(a, b, c): returns a, with all instances of b replaced by c

### Explaination of the condition used:
* `eq(variables['test'], 'True')` → returns *True* if condition matches, *False* if not
* `replace('True',eq(variables['test'], 'True'), 'value1')` → Replace **True** with **value1** if above expression returns True and returns *value1* else returns *True*
* `replace(replace('True',eq(variables['test'], 'True'), 'value1'),'True','value2')` → Replace **True** with **value2** if above expression results True and returns *value2* else returns original value of the above expression which is *value1*.
