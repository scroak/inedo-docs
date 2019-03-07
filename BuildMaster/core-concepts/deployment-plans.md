﻿---
title: Deployment Plans
subtitle: Deployment Plans
sequence: 300
keywords: buildmaster, plans
show-headings-in-nav: true
---
  Deployment plans are the instructions that tell BuildMaster exactly how to deploy your build and perform any other needed tasks during a release.

  They are written in language called OtterScript, and can be developed using the drag-and-drop editor. This saves you from having to learn the syntax before you can start building a plan. You can switch back-and-forth between visual and text modes to get a feel for the syntax and structure of the language pretty quickly, and master it in no time.

<tab-block>
<tab name= "Visual Mode">

![](/resources/documentation/otter/plan-blocks.png)

</tab>
<tab name="Text Mode (OtterScript)">

![](/resources/documentation/otter/plan-block-text.png)

</tab>
</tab-block>

### Creating Deployment Plans {#creating-deployment-plans data-title="Creating Deployment Plans"}

You can create a deployment plan at the application- or global-level. Global plans behave in exactly the same manner, except you may only reference global modules.

You may associate a deployment plan with an environment after you create it, which will allow you to restrict certain users from viewing its contents by defining an environment-scoped [access control](/support/documentation/buildmaster/administration/security). There's no good reason to do this, as you shouldn't be putting sensitive information in your deployment plans… but sometimes it can't be helped.

### OtterScript Basics {#otterscript-basics data-title="OtterScript Basics"}

OtterScript is a Domain-Specific Language that was designed for high-level orchestration and automation across servers, and is used to represent [configuration plans and orchestration plans](/support/documentation/otter/core-concepts/plans) in Otter, and deployment plans in Hedgehog and BuildMaster.

 OtterScript is interpreted as a series of statements and blocks, in a top-down manner.   

 **Statements** are mostly [operations](/support/documentation/buildmaster/reference) that perform certain tasks, but there are a few other statements including [set variable](/support/documentation/buildmaster/reference/operations/buildmaster/set-release-variable), log message, set execution status, call template, and raise error.

**Blocks** contain statements and other blocks. There are four types of blocks:    

{.docs}
- [General block](/support/documentation/buildmaster/execution-engine/statements-and-blocks/general-blocks); helps with grouping and organizing your statements, and offers various properties that define how statements and blocks will run
- [Loop block](/support/documentation/buildmaster/execution-engine/statements-and-blocks/loop); execute statements in a loop using an enumeration, such as a list of servers or roles
- [Try/Catch block](/support/documentation/buildmaster/execution-engine/statements-and-blocks/try-catch); introduce error-handling logic or change the execution success/failure status
- [If/Else block](/support/documentation/buildmaster/execution-engine/statements-and-blocks/if-else); conditionally execute statements based on an expression you specify   

If you're comfortable with programming or scripting, you may already be familiar with how these blocks work. To learn more, check out the [OtterScript Guide](/support/documentation/various/execution-engine/otterscript) in the Inedo Execution Engine documentation.

### PowerShell and Shell Scripting {#power-and-shell data-title="PowerShell and Shell Scripting"}

OtterScript was designed to seamlessly integrate with PowerShell and Bash/Sh, and can run inline script blocks, evaluate scripting expressions into variable values, and call externally -stored script files called assets.

Script assets can be added to BuildMaster at the application- or global-level. Once added, your scripts will appear in the statement list in the visual plan editor, and the parameters to those scripts will be parsed and displayed as textboxes when editing in visual mode.

### Deployment Modules {#deployment-modules data-title="Deployment Modules"}

Modules are reusable plans that can be called from a deployment plan or other modules, as if it were an operation. Like deployment plans, modules can be created at the application- or global-level, and are edited using the visual plan editor.

To create or edit modules, go to the Modules tab on the plans listing page. Modules are available in the statements list in the visual plan editor.   

#### Module Parameters {#module-parameters data-title="Module Parameters"}

Similar to operations, modules can have input- and output parameters. You can edit these by clicking on the Module Properties button in the Visual Plan Editor (when in visual mode), or by editing the OtterScript directly. These parameters are then accessible as variables within the module.   

:::attention {.best-practice}
Modules are run within the scope of whatever block calls it, which means it will inherit all of that block's variables. As a result, you should generally avoid relying on externally-defined variables in modules.
:::

**Note:** *modules* are called *templates* in BuildMaster v5.

## Plan Version Control and Rollback {#plan-version-control data-title="Plan Version Control and Rollback"}

BuildMaster 5.8 and later maintains a history of edits and allows rollback to any plan version, similar to a "revert" in source control. Version history is maintained for both deployment plans and deployment modules.    

### Comparing Versions {#comparing-versions data-title="Comparing Versions"}

On any plan's listing page, select the version number to display a list of all versions of the plan. From the Plan Version Listing page, there are options to compare any previous versions with the current. On the Plan Version Comparison page, any global plan or plan from any application visible to a user may be compared side-by-side.

### Plan Rollback {#plan-rollback data-title="Plan Rollback"}

To roll back to a previous version of a deployment plan, select the "edit" option of the desired version from the Plan Version Listing page, and then save the plan. This will create a new version of the plan with the same contents as the rollback target.