Specification.  
testingConfigPy.xml file format
====

*Editors: *  
*Date: *  
*Version: *  
----

## Content

[1. generalSettings](#generalSettings)  
[2. taskGroups](#taskGroups)  
[3. Tasks of specific types](#tasksOfSpecificTypes)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.1. taskGroup](#taskGroup)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.2. sftpSync](#sftpSync)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.3. keyPhrase](#keyPhrase)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.4. objectExist](#objectExist)  
&nbsp;&nbsp;&nbsp;&nbsp;[3.5. dataMatch](#dataMatch)
&nbsp;&nbsp;&nbsp;&nbsp;[3.6. creationHistory](#creationHistory)
&nbsp;&nbsp;&nbsp;&nbsp;[3.7. generateTests](#generateTests)  
___
testingConfigPy.xml stores serialized tasks entities as well as common configuration settings. The specification contains a brief information about the testingConfigPy.xml structure and parameters for customizing individual tasks.

Table 1. - A brief testingConfigPy.xml structure

| Name of the field        | Description                                                                                                                   |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| **\<generalSettings/>**  | intended for storing common configurations settings of the tasks: common paths, switching on/off output of certain data, etc. |
| **\<taskGroups/>**       | intended for listing tasks to be executed as well as defining their order of execution.                                                |
| **\<task1/>...<taskN/>** | every element might be either a single task or a task group with arbitrary number of nesting level                            | 

&nbsp;

## <a name="generalSettings">1. generalSettings</a>

<!--```
<sensor type="BR" serialNo="M1071364749" equipmentDataPoint="1" resonantFrequency="10000" channelsNumber="1" primaryChannelNo="1" lowFrequency="4" highFrequency="10000" sensitivity="32" sensitivityCorrection="1" description="Basic sensor parameters"/>
```
Picture 1.1. - Writing format in config.xml of settings **\<sensor/>**
-->
&nbsp;

Table 1.1. - **\<generalSettings/>** structure

| Name of the element      | Description                                                                                                                                                                                    |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **\<taskGroup/>**                  | Reference element for a task of the type `taskGroup`                                                                                                                          |
| **\<sftpSync/>**      | Reference element for a task of the type `sftpSync` |
| **\<keyPhrase/>**              | Reference element for a task of the type `keyPhrase`                                                                        |
| **\<objectExist/>**        | Reference element for a task of the type `objectExist`                  |
| **\<dataMatch/>**      | Reference element for a task of the type `dataMatch` |
| **\<creationHistory/>**          | Reference element for a task of the type `creationHistory`          |
| **\<generateTests/>**          | Reference element for a task of the type `generateTests`         |
| **\<defaultBehaviour/>**         | ??? |
| **\<testingReport/>**           | Configures report generation properties  |
| &nbsp;&nbsp;*shortLogEnable*           | On/off saving testing messages to the testing report  |
| **\<testsInputPath/>** | <td rowspan=2> Specifies functional test's input folder                                                   |
| &nbsp;&nbsp;*inPath* |   |
| **\<rawdataInFold/>** | <td rowspan=2> Required name of raw data directory in the input path. It will be created in testing object input path and all wav files will be copied in specified folder.                  |
| &nbsp;&nbsp;*path* |                                               |
| **\<commonInputData2_Path/>**, | Source of default Framework's input data                                              |
| &nbsp;&nbsp;*name* |                                               |
| &nbsp;&nbsp;<a name="def3">*path*</a> |                                               |
| **\<commonInputData3_Path/>**, | Source of default Framework's input history data                                              |
| &nbsp;&nbsp;*name* |                                               |
| &nbsp;&nbsp;<a name="def3">*path*</a> |                                               |
| **\<standardConfig_Path/>** | <td rowspan=2>Relative path to the Framework's standard config file |
| &nbsp;&nbsp;*path* |                                               |
| **\<standardInformativeTags_Path/>** | <td rowspan=2>Relative path to the standard informative tags file |
| &nbsp;&nbsp;*path* |         |
| **\<taskGroups/>**         | Specifies specific behaviour of tasks with certain statuses |
| &nbsp;&nbsp;*runUnlistedTasks* | If *runUnlistedTasks*="`1`" then tasks which are not presented in **\<taskGroups/>** are treated like regular tasks (like if they were in taskGroups) |
| &nbsp;&nbsp;*showUnlistedTasks* | If *showUnlistedTasks*="`1`" then tasks which are not presented in **\<taskGroups/>** are included in test report with status defined in *unlistedTasksStatus* |
| &nbsp;&nbsp;*showDisabledTasks* | Enable/disable referencing of tasks with status `Disabled` in a console and a testing report      |
| &nbsp;&nbsp;*showMissedTasks* | Enable/disable referencing of tasks with status `Missed` in a console and a testing report  |
| &nbsp;&nbsp;*unlistedTasksStatus* | Specifies the status for tasks which are not presented in **\<taskGroups/>** |
| **\postProcessing/>**         | ???  |
| &nbsp;&nbsp;*useCmd* |         |
| &nbsp;&nbsp;*saveInputDataOfFailedTests* |         |
| &nbsp;&nbsp;*saveOutputDataOfFailedTests* |         |


&nbsp;

## <a name="taskGroups">2. taskGroups</a>

- The element **\<taskGroups/>** specifies tasks to be executed as well as defines order of their execution.
- **\<taskGroups/>** might not be present in the testing config at all.
- Elements listed in the **\<taskGroups/>** might re-specify attributes of the corresponding tasks and its nested tasks.

```

```
Picture 2.1. - Writing format of **\<taskGroups/>** in testingConfigPy.xml

&nbsp;

## <a name="tasksOfSpecificTypes">3. Tasks of specific types</a>

&nbsp;

All the elements listed in the table 3.1 are common for any task.

&nbsp;

Table 3.1 - common elements of a generic task

| Name of the field | Description                                                          |
|-------------------|----------------------------------------------------------------------|
| *enable*    | Enable/disable execution of a task |
| *testType*    | Every task must have an attribute *testType*, whose value might be one of the following: `taskGroup`, `sftpSync`, `keyPhrase`, `objectExist`, `dataMatch`, `creationHistory`, `generateTests`.<br/><br/>Also the value of *testType* might have the following format: `inherit(parentTask)`, where `parentTask` is the tag of the parentTask.<br/><br/>If parentTask is a nested task, it is highly recommended to specify tags of its outer tasks: `inherit(outerTaskOfParentTask/parentTask)`.<br/><br/>Explicit specifying of outer tag(-s) can be omitted only in the case when it's guaranteed that there aren't or won't be any other task whose tag is equal to the one of parentTask. |

&nbsp;

Elements listed in the table 3.2 are common for any testing task (i.e. for `keyPhrase`, `objectExist`, `dataMatch`, `creationHistory`, `generateTests`).

&nbsp;

Table 3.2. - common elements of a testing task

| Name of the field | Description                                                          |
|-------------------|----------------------------------------------------------------------|
| **\<inputData/>**          |  |
| &nbsp;&nbsp;<a name="copyIn">*copyIn*</a>    | All: Specifies specific actions executed prior framework's call. In the case of many actions they are listed as comma separated values(i.e. *copyIn*="`cmd1, cmd2, cmd3`", where `cmd1`, `cmd2`, `cmd3` are placeholders for commands listed in the table 3.3). |
| &nbsp;&nbsp;<a name="inPath">*inPath*</a>    | Specifies path of tests' input data. Might be empty. |
| &nbsp;&nbsp;*editConfig*    | Specifies values to modify in the framework's config in the following format: `elementTag, attributeTag, valueToSet`. If there are multiple such entries then either '; ' or ';; ' is used as a delimiter (but both cannot be used simultaneously!). ';; ' is used in cases when changing value has ';'. |
| &nbsp;&nbsp;*filesToRemove*    | Specifies path(-s) to remove prior framework's call. |
| &nbsp;&nbsp;*filesToMove*    |  |
| &nbsp;&nbsp;**    |  |
| **\<outputData/>**          |  |
| &nbsp;&nbsp;<a name="copyOut">*copyOut*</a>     | All: Specifies specific actions executed after framework's call. In the case of many actions they are listed as comma separated values(i.e. *copyOut*="`cmd1, cmd2, cmd3`", where `cmd1`, `cmd2`, `cmd3` are placeholders for commands listed in the table 3.3). |
| &nbsp;&nbsp;*finInLog*    | KP, CH: Specifies keyphrases to find in framework's execution log. Used by tasks of types `keyPhrase` and `creationHistory`. |
| &nbsp;&nbsp;*filesToCheck*    | OE: Specifies path(-s) to check existence for. Used by task of type `objectExist`. |
| &nbsp;&nbsp;*filesToRemove*    | Specifies path(-s) to remove after framework's call. |
| &nbsp;&nbsp;*filesToMove*    |  |
| &nbsp;&nbsp;**    |  |

&nbsp;

Table 3.3. - possible commands of *copyIn* and *copyOut*

| Name of the field | Description                                                          |
|-------------------|----------------------------------------------------------------------|
| `none` or `` | Do nothing |
| `0` or `clri` | Empty classifier's 'In' folder |
| `1` or `spc1` | Copies contents of folder specified in [*inPath*](#inPath) into classifier's 'In' folder |
| `2` or `seqh` |  |
| `def1` | ????? |
| `def2` | Copies contents of ['def2'](#def2) folder into classifier's 'In' folder. |
| `def3` | Copies contents of ['def3'](#def3) folder into classifier's 'In' folder. |
| `delw` | Deletes \*.wav-files in classifier's 'In' folder. |
| `delf` | Deletes files defined in either `outputData/@filesToRemove` or `inputData/@filesToRemove` (it depends where `delf` is declared: in [*copyIn*](#copyIn) or [*copyOut*](#copyOut)) |
| `movf` | Moves files defined in either `outputData/@filesToMove` or `inputData/@filesToMove` (it depends where `movf` is declared: in [*copyIn*](#copyIn) or [*copyOut*](#copyOut)) |
| `daec` or `daef` | Deletes everything except 'config.xml' in classifier's 'In' folder. |
| `sftp` | Fetches from SFTP some input data for tests of type `generateTests`. |
| `cpif` | For failed tests copy contents of classifier's 'In' folder into 'FunctionalTesting\testsOutPython\outerTaskTag_taskTag\In', where 'outerTaskTag_taskTag' is the name of a folder formed by concatenating tag of a task and tags of its outer tasks. |
| `cpof` | For failed tests copy contents of classifier's 'Out' folder into 'FunctionalTesting\testsOutPython\outerTaskTag_taskTag\Out', where 'outerTaskTag_taskTag' is the name of a folder formed by concatenating tag of a task and tags of its outer tasks. |

&nbsp;

### <a name="taskGroup">3.1. taskGroup</a>

```
	<taskGroup enable="0" testType="taskGroup" />
```
Picture 3.1.1. - Writing format in config.xml of a task with *testType*=`taskGroup`

&nbsp;

### <a name="sftpSync">3.2. sftpSync</a>

```
	
```
Picture 3.2.1. - Writing format in config.xml of a task with *testType*=`sftpSync`

&nbsp;

Table 3.2.1. - structure of a task with *testType*=`sftpSync`

| Name of the field | Description                                                          |
|-------------------|----------------------------------------------------------------------|
| *path* | Root path of a local mirror. |
| **\<localPath/>**          | Specifies local path for synchronization. |
| &nbsp;&nbsp;*path* | Root path of a local mirror. |
| &nbsp;&nbsp;*exclude* | Specifies path(-s) which is(are) ignored during synchronization. |
| **\<remotePath/>**    | Specifies remote path(-s) to synchronize with. |
| &nbsp;&nbsp;*include* | One or more paths on the remote to synchronize with. |
| &nbsp;&nbsp;*exclude* | One or more paths on the remote which are ignored during synchronization. |
| **\<options/>**         |                     |
| &nbsp;&nbsp;*deletePresentOnlyLocally* | When *deletePresentOnlyLocally*="`1`" then elements which present locally and absent remotely are deleted; when *deletePresentOnlyLocally*="`0`" then they are placed to the remote.  |
| &nbsp;&nbsp;*updateRemote*     | If *updateRemote*="`0`" then do nothing if a local file is newer than the corresponding remote one; when *updateRemote*="`1`" then upload the file to the remote (with overriding the file which was there before). |
| &nbsp;&nbsp;*preLocalCopying*     | Enable/disable the following chain of actions:<br/><br/>1) Copying everything (except folders starting with '!_') from '\FunctionalTesting\ftpTemp\SingleTests' to '\FunctionalTesting\testsIn';<br/><br/>2) there's special treatment of folders '!_defaultInputData_auto' and '!_defaultInputData_history':<br/><br/>&nbsp;&nbsp;2.1)copying \*.wav-files, 'historyFiles' folder, 'files.xml' and 'equipmentProfile.xml' from the corresponding folder located in '\FunctionalTesting\ftpTemp\SingleTests';<br/><br/>&nbsp;&nbsp;2.2) copying 'standardConfig.xml' and 'standardInformativeTags.xml' located in '\ComputeFramework\Classifier\Library\commonFunctions\preProcessing' with renaming into 'config.xml' and 'informativeTags.xml' respectively;<br/><br/>3) for tasks with *testType*="`generateTests`" creating folders specified in *inPath* and copying there 'equipmentProfile.xml' located in '\ComputeFramework\Equipment\_dataset_\taskTag', where 'taskTag' is a tag of task's element |
| &nbsp;&nbsp;*postLocalCopying*     | Copying of 'historyFiles' folder from task's folder in 'testIn' into corresponding folder in 'ftpTemp/SingleTests'. This is only done for tasks with *testType*="`generateTests`", *enable*="`1`" and *generate*="`1`". After this synchronization with sftp is performed |

&nbsp;

### <a name="keyPhrase">3.3. keyPhrase</a>

```
	
```
Picture 3.3.1. - Writing format in config.xml of a task with *testType*=`keyPhrase`

&nbsp;

Table 3.3.1. - structure of a task with *testType*=`keyPhrase`

| Name of the field | Description                                                          |
|-------------------|----------------------------------------------------------------------|
| **\</>**          |  |
| &nbsp;&nbsp;**    |  |
| &nbsp;&nbsp;**    |  |

&nbsp;

### <a name="objectExist">3.4. objectExist</a>

```
	
```
Picture 3.4.1. - Writing format in config.xml of a task with *testType*=`objectExist`

&nbsp;

Table 3.4.1. - structure of a task with *testType*=`objectExist`

| Name of the field | Description                                                          |
|-------------------|----------------------------------------------------------------------|
| **\</>**          |  |
| &nbsp;&nbsp;**    |  |
| &nbsp;&nbsp;**    |  |

&nbsp;

### <a name="dataMatch">3.5. dataMatch</a>

```
	
```
Picture 3.5.1. - Writing format in config.xml of a task with *testType*=`dataMatch`

&nbsp;

Table 3.5.1. - description of additional fields in a task with *testType*=`dataMatch`

| Name of the field | Description                                                          |
|-------------------|----------------------------------------------------------------------|
| **\<outputData/>**          |  |
| &nbsp;&nbsp;*datamatch_fields*    | Contains an XPath-expression which returns fields to compare in status and reference files. In the case when *datamatch_fields*="``" then all corresponding items in status and reference will be compared. |
| &nbsp;&nbsp;*datamatch_tolerance*    | Contains either a numeric value of tolerance or an XPath-expression for quering the framework's config for it. |

&nbsp;

### <a name="creationHistory">3.6. creationHistory</a>

```
	
```
Picture 3.6.1. - Writing format in config.xml of a task with *testType*=`creationHistory`

&nbsp;

Table 3.6.1. - structure of a task with *testType*=`creationHistory`

| Name of the field | Description                                                          |
|-------------------|----------------------------------------------------------------------|
| **\</>**          |  |
| &nbsp;&nbsp;**    |  |
| &nbsp;&nbsp;**    |  |

&nbsp;

### <a name="generateTests">3.7. generateTests</a>

```
	
```
Picture 3.7.1. - Writing format in config.xml of a task with *testType*=`generateTests`

&nbsp;

Table 3.7.1. - structure of a task with *testType*=`generateTests`

| Name of the field | Description                                                          |
|-------------------|----------------------------------------------------------------------|
| **\</>**          |  |
| &nbsp;&nbsp;**    |  |
| &nbsp;&nbsp;**    |  |

&nbsp;

## <a name="descriptionExamples">4. Description examples</a>  

### <a name="inheritanceExample">Example 1. Inheritance</a>

The following xml-snippet depicts the usage of inheritance when specifiyng value of *testType*:
```

```

### <a name="sftpSyncExample1">Example 1. sftpSync usage</a>
