# SetReleaseVariable
A task to set an Azure DevOps Release Variable in a way that can be shared between pipelines

Out of the box, Azure DevOps does not provide an easy way to shared variables between Jobs in a Release Stage, or between Stages.

<a href="http://donovanbrown.com/post/Passing-variables-from-stage-to-stage-in-Azure-DevOps-release" target="_blank">Donovan Brown</a> and <a href="https://stefanstranger.github.io/2019/06/26/PassingVariablesfromStagetoStage" target="_blank">Stefan Stranger</a> have demonstrated how to use the Azure DevOps REST API to update Release Variables from a Powershell script.

What I have done is to modify their scripts slightly and export an Azure DevOps Task that you can import into your own projects to enable this functionality. By default, exporting a Task Group may result in some of the system variables that your script depends on being created as parameters of the task group. 

I followed <a href="https://medium.com/objectsharp/how-to-hide-a-task-group-parameter-b95f7c85870c" target="_blank">Dave Lloyd's</a> guide to setting a `visibleRule` that is always false that will prevent these required parameters from being shown when you add the task to to your Pipeline. Annoyingly they are still shown in the imported Task Group, but at least we have minimised the risk of them being amended in the Pipeline itself.

To use:

1. Create a Release Variable you want to amend
1. Go to your Project's task groups and Import the Json
1. Ensure that your organisation's `Project Collection Build Service` has the `Pipelines\Manage Build Resources` permission set to `Allow`
1. Add the task to a Release Job. 
1. Set the ReleaseVariableName and ValueToSet parameters
1. From this point on in any job or stage you can access the value of your Release Variable in the normal way.
