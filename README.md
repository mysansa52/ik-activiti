# ik-activiti
activiti study 

## 关于沟通的实现
沟通的需求为：
* 在流程任何人工步骤中，都可以找若干个（一个或多个）人员进行沟通，让他们给出意见。
* 沟通发起人可以提供一条沟通事由
* 沟通人员可以为流程提供 认可，不认可，说明信息，以及附件
* 沟通不必作为主流程的过程必要条件，即使发出了沟通，不需要等所有人沟通回复后，才能继续。
沟通发起人随时可以继续流程，忽略之后的沟通回复。
* 沟通信息会以 5/7/10 这种模式显示，分表表示 认可数/沟通回复数/沟通人员总数

暂时考虑的实现方式为:<p>
因为沟通人数不定，抽象为每向一个人沟通为一个子流程，可以并发多个子流程来达到向多人沟通的目的。

## 关于会签 
可以考虑用Multi-instance来实现。以下为示例代码:
```xml
<userTask id="miTasks" name="My Task" activiti:assignee="${assignee}">
  <multiInstanceLoopCharacteristics isSequential="false"
     activiti:collection="assigneeList" activiti:elementVariable="assignee" >
    <completionCondition>${nrOfCompletedInstances/nrOfInstances >= 0.6 }</completionCondition>
  </multiInstanceLoopCharacteristics>
</userTask>
```

