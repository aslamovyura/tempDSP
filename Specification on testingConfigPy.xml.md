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
testingConfigPy.xml stores serialized tasks entities as well as common configuration settings. The specification contains brief information about the testingConfigPy.xml structure and parameters for customizing individual tasks.

Table 1. - A brief testingConfigPy.xml structure

| Name of the field         | Description                                                                                                                   |
|---------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| **\<generalSettings/>**   | Intended for storing common configurations settings of the tasks: common paths, switching on/off an output of certain data, etc. |
| **\<taskGroups/>**        | Intended for listing tasks to be executed as well as defining their order of execution.                                                |
| **\<task1/>...\<taskN/>** | 'task1' and 'taskN' are placeholders for elements' actual tags whereas a tag name cannot be 'generalSettings' or 'taskGroups' or have a name of an already existing element. Every element might be either a single task or a task group with an arbitrary number of nesting level. These elements' tags are supposed to be referenced in **\<taskGroups/>**.                           | 

&nbsp;

## <a name="generalSettings">1. generalSettings</a>

```
<generalSettings>

	<taskGroup enable="0" testType="taskGroup">
	</taskGroup>
	
	<sftpSync enable="0" testType="sftpSync">
		<localPath path="\ComputeFramework\FunctionalTesting\ftpTemp" exclude=""/>
		<remotePath include="/data/Datasets/FunctionalTesting0/SingleTests" exclude=""/>
		<options deletePresentOnlyLocally="0" updateRemote="0" preLocalCopying="0" postLocalCopying="0"/>
	</sftpSync>
	
	<keyPhrase enable="0" testName="runnabilityAllOn" testFuncName="test_runProcessing_runnabilty" testType="keyPhrase" description="check if runProcessing.m script runs and finishes properly">
		<testPath testFuncPath="\ComputeFramework\FunctionalTesting\testsLib\runProcessing\runnabilityAllOn\test_runProcessing_runnabiltyAllOn.m" description="path to the test"/>
		<inputData copyIn="clri, def2, delw, def3" editConfig="equipmentStateDetectionEnable, value, 1; debugModeEnable, value, 0; printPlotsEnable, value, 1; parpoolEnable, value, 1; frequencyTrackingEnable, value, 1; frequencyCorrectionEnable, value, 1; shaftTrajectoryDetectionEnable, value, 0"/>
		<outputData copyOut="cpif, cpof" findInLog="'Code: I086', 'Code: I088', 'Code: 0006', 'Code: 0007', 'Code: 0008', 'Code: 0009', 'Code: 0010', 'Code: 0011'" outPath="" description=""/>
	</keyPhrase>
	
	<objectExist enable="0" testName="outDirExistence" testFuncName="test_inOutExistence_outDirExistence" testType="objectExist" description="Checking existence of the @Out directory in /ComputeFramework/Classifier/">
		<testPath findPath="0" testFuncPath="\ComputeFramework\FunctionalTesting\testsLib\inOutExistence\outDirExistence\test_inOutExistence_outDirExistence.m" description="path to the test"/>
		<inputData copyIn="clri, def2" findPath="0" inPath="" description="copyIn=3 - use default files only"/>
		<outputData copyOut="cpif, cpof" outPath="" filesToCheck="\ComputeFramework\Classifier\Out" description=""/>
	</objectExist>
	
	<dataMatch enable="0" testName="dataMatchInterf" testFuncName="test_frequencyCorrection_dataMatch" testType="dataMatch" description="check if frequency correction recognises typical cases properly">
		<testPath findPath="0" testFuncPath="D:\Ratgor\GitRepo\FuncTestCopy\ComputeFramework\FunctionalTesting\testsLib\frequencyCorrection\dataMatch\test_frequencyCorrection_dataMatch.m" description="path to the test"/>
		<inputData backupIn="1" copyIn="clri, def2, delw, spc1" findPath="0" inPath="\ComputeFramework\FunctionalTesting\testsIn\frequencyCorrection\dataMatchInterf" description="copy to the input of testing object" editConfig="historyEnable, value, 1; frequencyCorrectionEnable, value, 1"/>
		<outputData copyOut="cpif, cpof" findPath="0" outPath="\ComputeFramework\FunctionalTesting\testsOut\frequencyCorrectionDataMatch" description="compare with output of testing object" datamatch_fields="//*[self::frequencyCorrector]/@estimatedFrequency | /equipment/frequencyCorrector/status/@value" datamatch_tolerance="0.1"/>
	</dataMatch>
	
	<creationHistory enable="0" testName="runabilityFull" testFuncName="test_creatingHistoryFiles_runabilityFull" testType="creationHistory" description="">
		<testPath testFuncPath="\ComputeFramework\FunctionalTesting\testsLib\creatingHistoryFiles\runabilityFull\test_creatingHistoryFiles_runabilityFull.m" description="path to the test"/>
		<inputData copyIn="2" inPath="\ComputeFramework\FunctionalTesting\testsIn\creatingHistoryFiles" description="copy to the input of testing object" editConfig="historyEnable, value, 1; printPlotsEnable, value, 1; equipmentStateDetectionEnable, value, 1; shaftDisplacementEnable, value, 1; frequencyCorrectionEnable, value, 1; frequencyDomainClassifierEnable, value, 1; timeDomainClassifierEnable, value, 1; timeFrequencyDomainClassifierEnable, value, 1; metricsEnable, value, 1; spmEnable, value, 1; iso15242Enable, value, 1; iso10816Enable, value, 1; iso7919Enable, value, 1; octaveSpectrumEnable, value, 1; decisionMakerEnable, value, 1"/>
		<outputData copyOut="cpif, cpof" outPath="" description="compare with output of testing object" findInLog="'[Framework] Framework processing. \n @status.xml file was successfully updated by history.', '[Framework] History processing. \n History processing COMPLETE.'"/>
	</creationHistory>
	
	<generateTests enable="0" testType="generateTests" generateHistory="0" frameworkVersion="v3.3.1" description=""> 
		<inputData copyIn="sftp, 2" inPath="\ComputeFramework\FunctionalTesting\testsIn\highSpeedBearingHistoryDatamatch" editConfig="historyEnable, value, 1;; frequencyCorrectionEnable, value, 1;; frequencyTrackingEnable, value, 1;; bearingsParametersRefinement, value, 1;; evaluation/frequencyTracking, maxPercentDeviation, 6;; evaluation/frequencyTracking, maxPercentDeviationPerSec, 1;; evaluation/frequencyTracking, method, spectrogram;; evaluation/frequencyTracking/spectrogramTracker, type, acc;; evaluation/frequencyTracking/spectrogramTracker/accTracker, frequencyRange, 128:512; 256:1024; 512:2048;;"/>
		<outputData copyOut="cpif, cpof" outPath=""/>
		<SSR_datamatchHistory enable="1" testName="SSR_datamatchHistory" testType="datamatchHistory" description="SSR=???" datamatch_fields="//frequencyCorrector/informativeTags/estimatedFrequency/@value | //frequencyCorrector/informativeTags/initialFrequency/@value" datamatch_tolerance="//frequencyCorrector/displacementInterferenceEstimator/rough/@percentStep | //frequencyCorrector/interferenceFrequencyEstimator/rough/@percentStep"/>
		<SST_datamatchHistory enable="1" testType="datamatchHistory" description="" datamatch_fields="//frequencyTracking/informativeTags/type/@value | //frequencyTracking/informativeTags/method/@value | //frequencyTracking/informativeTags/min/@value | //frequencyTracking/informativeTags/max/@value | //frequencyTracking/informativeTags/peak2peak/@value | //frequencyTracking/informativeTags/mean/@value | //frequencyTracking/informativeTags/std/@value | //frequencyTracking/informativeTags/median/@value" datamatch_tolerance="//frequencyTracking/@accuracyPercent" testName="SST_datamatchHistory"/>
		<BPR_datamatchHistory enable="1" testType="datamatchHistory" description="" datamatch_fields="//bearingsParametersRefinement/informativeTags/bearing/@bd | //bearingsParametersRefinement/informativeTags/bearing/@deviation" datamatch_tolerance="//bearingsParametersRefinement/ballDiameter/@percentStep" testName="BPR_datamatchHistory"/>
		<Periodicities_datamatchHistory enable="0" testType="datamatchHistory" description="" datamatch_fields="" datamatch_tolerance="" testName="Periodicities_datamatchHistory"/>
	</generateTests>

	<defaultBehaviour testEnableDefault="1" waitSlowOsTimeout="20" findPathDefault="3">
		<exampleObject enable="1" objectName="objectName" objectType="objectType" description="unic record of a testing object">
			<objectPath findPath="default" objectPath="\ComputeFramework\Classifier\runProcessing.m" description="path to the object of a testing"/>
			<exampleTest enable="1" clearWorkspaceAfter="1" clearWorkspaceBefore="1" objectPath="D:\Ratgor\Git\ComputeFramework\Classifier\runProcessing.m" testName="testName" testFuncName="test_objectName_testName" testType="keyPhrase" description="some object test action description"> 
				<testPath findPath="0" testFuncPath="\ComputeFramework\FunctionalTesting\testsLib\runProcessing\runnability\test_runProcessing_runnabilty.m" description="path to the test"/>
				<inputData copyIn="2" filesToRemove="\ComputeFramework\Classifier\In" filesToMove="\In\test.xml -&gt; \Out\test.xml" editConfig="0" backupIn="1" findPath="1" inPath="\ComputeFramework\FunctionalTesting\testsIn\!_defaultInputData_auto" backupPath="\ComputeFramework\FunctionalTesting\testsOut\inpitDataBackup" description="copy to the input of testing object"/>
				<outputData copyOut="cpif, cpof, 0" filesToRemove="\ComputeFramework\Classifier\Out" filesToMove="\In\test.xml - \Out\test.xml" findInLog="Code: 0033" filesToCheck="\ComputeFramework\Classifier\Out" compareOut="0" findPath="2" outPath="\ComputeFramework\FunctionalTesting\testsOut\outputDataCopy" comparePath="\ComputeFramework\Classifier\In" errors="0;0.05;0;0.05;0.05;0.05;0.05" description="path to clasifire In, Out and Workspace backups; path to ethalon files"/>
			</exampleTest>
		</exampleObject>
	</defaultBehaviour>
	<testingReport shortLogEnable="1" description=""/>
	<testsInputPath inPath="\ComputeFramework\FunctionalTesting\testsIn" description=""/>
	<rawdataInFold path="rawdata" description="Required name of raw data directory in the input path. It will be created in testing object input path and all wav files will be copied in specified folder."/>
	<commonInputData0_Path name="none" description="mnemonics for of default input composition. 'none' for nothing, 'clri' for clear input folder, 'spc1' for copy special input data #1, 'cdi1' for cpoy common input data #1, 'delw' for delete wavs, etc."/>
	<commonInputData2_Path name="def2" path="\ComputeFramework\FunctionalTesting\testsIn\!_defaultInputData_auto"/>
	<commonInputData3_Path name="def3" path="\ComputeFramework\FunctionalTesting\testsIn\!_defaultInputData_history"/>
	<standardConfig_Path path="\ComputeFramework\Classifier\Library\commonFunctions\preProcessing\standardConfig.xml"/>
	<standardInformativeTags_Path path="\ComputeFramework\Classifier\Library\commonFunctions\preProcessing\standardInformativeTags.xml"/>
	<taskGroups runUnlistedTasks="0" showUnlistedTasks="0" showDisabledTasks="0" showMissedTasks="1" unlistedTasksStatus="notUsed"/>
	<postProcessing saveInputDataOfFailedTests="1" saveOutputDataOfFailedTests="1" useCmd="1" />
</generalSettings>
```
Figure 1.1. - An example usage of **\<generalSettings/>** in testingConfigPy.xml

&nbsp;

Table 1.1. - **\<generalSettings/>** structure

| Name of the element                       | Description                                                                                                                                                                                    |
|-------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **\<taskGroup/>**                         | Reference element for a task of type [`taskGroup`](#taskGroup).                                                                                                                          |
| **\<sftpSync/>**                          | Reference element for a task of type [`sftpSync`](#sftpSync). |
| **\<keyPhrase/>**                         | Reference element for a task of type [`keyPhrase`](#keyPhrase).                                                                        |
| **\<objectExist/>**                       | Reference element for a task of type [`objectExist`](#objectExist).                  |
| **\<dataMatch/>**                         | Reference element for a task of type [`dataMatch`](#dataMatch). |
| **\<creationHistory/>**                   | Reference element for a task of type [`creationHistory`](#creationHistory).          |
| **\<generateTests/>**                     | Reference element for a task of type [`generateTests`](#generateTests).         |
| **\<defaultBehaviour/>**                  | Contains default values of tasks' fields. These values are used when tasks' elements don't have them by themselves. |
| **\<testingReport/>**                     | Configures report generation properties.  |
| &nbsp;&nbsp;*shortLogEnable*              | Enables/disables (`1`/`0`) saving testing messages to the testing report.  |
| **\<testsInputPath/>**                    |                                                    |
| &nbsp;&nbsp;*inPath*                      | Specifies tests' input folder. |
| <a name="rdif">**\<rawdataInFold/>**</a>  |                   |
| &nbsp;&nbsp;*path*                        | Required name of raw data directory in the input path. It will be created in testing object input path and all. wav files will be copied in specified folder. |
| **\<commonInputData2_Path/>**             |  |
| &nbsp;&nbsp;*name*                        | Reference name for the path (`def2`). |
| &nbsp;&nbsp;<a name="def3">*path*</a>     | Source of default Framework's input data. |
| **\<commonInputData3_Path/>**             |                                               |
| &nbsp;&nbsp;*name*                        | Reference name for the path (`def3`).                                              |
| &nbsp;&nbsp;<a name="def3">*path*</a>     | Source of default Framework's input history data.                                            |
| **\<standardConfig_Path/>**               |  |
| &nbsp;&nbsp;*path*                        | Relative path to the Framework's standard config file. |
| **\<standardInformativeTags_Path/>**      |  |
| &nbsp;&nbsp;*path*                        | Relative path to the standard informative tags file. |
| **\<taskGroups/>**                        | Specifies specific behaviour of tasks with certain statuses. |
| &nbsp;&nbsp;*runUnlistedTasks*            | If *runUnlistedTasks*="`1`" then tasks which are not presented in **\<taskGroups/>** are treated like regular tasks (like if they were in taskGroups). |
| &nbsp;&nbsp;*showUnlistedTasks*           | If *showUnlistedTasks*="`1`" then tasks which are not presented in **\<taskGroups/>** are included in test report with status defined in *unlistedTasksStatus*. |
| &nbsp;&nbsp;*showDisabledTasks*           | Enables/disables (`1`/`0`) referencing of tasks with status `Disabled` in a console and a testing report.      |
| &nbsp;&nbsp;*showMissedTasks*             | Enables/disables (`1`/`0`) referencing of tasks with status `Missed` in a console and a testing report.  |
| &nbsp;&nbsp;*unlistedTasksStatus*         | Specifies the status for tasks which are not presented in **\<taskGroups/>**. |
| **\<postProcessing/>**                    |  |
| &nbsp;&nbsp;*useCmd*                      | When *useCmd*="`1`" then conclusion about saving of contents of classifier's 'In'/'Out' folders is made based on presence of 'cpif'/'cpof' commands in *copyOut* of failed tests; *saveInputDataOfFailedTests* and *saveOutputDataOfFailedTests* are used otherwise. |
| &nbsp;&nbsp;*saveInputDataOfFailedTests*  | Enables/disables (`1`/`0`) saving of contents of classifier's 'In' folder (when *useCmd*="`0`"). |
| &nbsp;&nbsp;*saveOutputDataOfFailedTests* | Enables/disables (`1`/`0`) saving of contents of classifier's 'Out' folder (when *useCmd*="`0`"). |


&nbsp;

## <a name="taskGroups">2. taskGroups</a>

- The aim of the element **\<taskGroups/>** is specifying tasks to be executed and defining their execution order.
- **\<taskGroups/>** might not be present in the testing config at all. In this case tasks will be executed based on *enable* values of elements representing them and their order of following in the testing config.
- Elements listed in **\<taskGroups/>** might re-specify attributes of the corresponding tasks and its nested tasks. See the [example](#taskGroupsExample1) for details.
- Exceptional case is a task of type `generateTests`, for which there must be an element in **\<taskGroups/>** and it must have the `generate` attribute (examples are `highSpeedBearing` and `highSpeedGearing` in fig. 2.1.).

&nbsp;

```
<taskGroups>  
	<sftpSyncBefore enable="1" description="preliminary synchronization with sftp and local copying"/>
	<shortestRun enable="1" description="general script for computation Framework running"/>
	<longtestRun enable="1" description="general script for computation Framework running"/>
	<runProcessing enable="1" description="general script for computation Framework running"/>
	<initialization enable="1" description="script for testing initialization's processes"/>
	<equipmentParser enable="1" description="examins common functions in Framework, except initialization"/>
	<equipmentStateDetection enable="1" description="script for testing equipment state detection"/>
	<commonSpectrums enable="1" description="testing for general spectrum calculation"/>
	<frequencyTracking enable="1" description="script for testing shaft frequency tracking"/>
	<frequencyCorrection enable="1" description="script for testing shaft rotational speed refinement"/>
	
	<octaveSpectrum enable="1" description="check caclulations of 1{1/3,1/6}-octave spectrum for easy machine state control"/>
	<metrics enable="1" description="examins metrics method in Framework"/>
	<iso7919 enable="1" description="script for testing ISO7919 method"/>
	<iso10816 enable="1" description="check calculations of mean vibration level in 3 ranges (L,M,H)"/>
	<iso15242 enable="1" description="check calculations of mean vibration level in 3 ranges (L,M,H)"/>
	<spmLRHR enable="1" description="check first shock-pulse method(SPM) calculations with LR/HR level"/>
	<spmDBmDBc enable="1" description="check first shock-pulse method(SPM) calculations with dBc/dBm level"/>
	
	<shaftTrajectoryDetection enable="1" description="script for testing shaft imbalance detection"/>
	<frequencyDomainClassifier enable="1" description="script for testing analysis in frequencyDomain"/>
	<timeFrequencyDomainClassifier enable="1" description="script for testing time-frequency domain classifier"/>
	<scalogram enable="1" description="script for testing scalogram"/>
	<correlationPeriodicyProcessing enable="1" description="script for testing search of periodicities"/>
	<bearingsParametersRefinement enable="1" description="???"/>
	
	<decisionMaker enable="1" description="decion maker testing"/>
	<monitoringHistory enable="1" description="scripts for tesing of history evaluation "/>
	<plottingImages enable="1" description="testing for methods of images plotting"/>
	
	<creatingHistoryFiles enable="1" description="Imitation of history processing for each compute method" />
	
	<highSpeedBearing enable="1" generate="1" description="Generating datamatch tests. for example history datamatch"/>
	<highSpeedGearing enable="1" generate="1" description="Generating datamatch tests. for example history datamatch"/>
	<sftpSyncAfter enable="1" description="local copying and synchronization with sftp intended to put generated history to the remote"/>
</taskGroups>
```
Figure 2.1. - An example usage of **\<taskGroups/>** in testingConfigPy.xml

&nbsp;

## <a name="tasksOfSpecificTypes">3. Tasks of specific types</a>

All the elements listed in the table 3.1 are common for any task.

Table 3.1 - common elements of a generic task

| Name of the field | Description                                                          |
|-------------------|----------------------------------------------------------------------|
| *enable*          | Enables/disables (`1`/`0`) execution of a task. Obligatory only for reference tasks in **\<generalSettings/>** (for all reference tasks *enable*="`0`" ). For all other tasks it can be skipped. In this case value of *enable* is taken from a reference task of the same type (of course, if *enable* does not present in task's corresponding element in **\<taskGroups/>**). |
| *testType*        | Every task must have the *testType* attribute, whose value might be one of the following: `taskGroup`, `sftpSync`, `keyPhrase`, `objectExist`, `dataMatch`, `creationHistory`, `generateTests`.<br/><br/>Also the value of *testType* might have the following format: `inherit(parentTask)`, where `parentTask` is a tag of a parent task.<br/><br/>If parentTask is a nested task, it is highly recommended to specify tags of its outer tasks: `inherit(outerTaskOfParentTask/parentTask)`.<br/><br/>Explicit specifying of outer tag(-s) can be omitted only in the case when it's guaranteed that there aren't or won't be any other task whose tag is equal to the one of parentTask. |
| *objectPath*      | Specifies path to an object by which the Framework can be launched (e.g. *objectPath*="`\ComputeFramework\Classifier\runProcessing.m`"). |

&nbsp;

Elements listed in the table 3.2 are common for any testing task (i.e. for `keyPhrase`, `objectExist`, `dataMatch`, `creationHistory`, `generateTests`).

<a name="commonTestElements">Table 3.2. - common elements of a testing task</a>

| Name of the field                                | Description                                                          |
|--------------------------------------------------|----------------------------------------------------------------------|
| **\<inputData/>**                                |  |
| &nbsp;&nbsp;<a name="copyIn">*copyIn*</a>        | Specifies specific actions executed prior Framework's call. In the case of many actions they are listed as comma separated values(i.e. *copyIn*="`cmd1, cmd2, cmd3`", where `cmd1`, `cmd2`, `cmd3` are placeholders for commands listed in the table 3.3). |
| &nbsp;&nbsp;<a name="inPath">*inPath*</a>        | Specifies path of tests' input data. Might be empty. Usage example: *inPath*="`\ComputeFramework\FunctionalTesting\testsIn\creatingHistoryFiles`". |
| &nbsp;&nbsp;*editConfig*                         | Specifies values to modify in the Framework's config in the following format: "`elementTag, attributeTag, valueToSet`". If there are multiple such entries then either '; ' or ';; ' is used as a delimiter (but both cannot be used simultaneously!). ';; ' is used in cases when changing value has ';'. Usage examples: *editConfig*="`equipmentStateDetectionEnable, value, 1; debugModeEnable, value, 0`", *editConfig*="`evaluation/frequencyTracking/spectrogramTracker, type, acc;; evaluation/frequencyTracking/spectrogramTracker/accTracker, frequencyRange, 128:512; 256:1024; 512:2048`" |
| &nbsp;&nbsp;<a name="idftr">*filesToRemove*</a>  | Specifies path(-s) to remove prior Framework's call. |
| &nbsp;&nbsp;<a name="idftm">*filesToMove*</a>    | Specifies items to move prior Framework's call. Written in the following format: `source -&gt; destination`, where `source` and `destination` are placeholders for paths in a filesystem. Example usage: *filesToMove*="`\ComputeFramework\Classifier\In\translations_test.xml -&gt; \ComputeFramework\Classifier\Library\translations\translations_test.xml`" |
| **\<outputData/>**                               |  |
| &nbsp;&nbsp;<a name="copyOut">*copyOut*</a>      | Specifies specific actions to be executed after Framework's call. In the case of many actions they are listed as comma separated values(i.e. *copyOut*="`cmd1, cmd2, cmd3`", where `cmd1`, `cmd2`, `cmd3` are placeholders for commands listed in the table 3.3). |
| &nbsp;&nbsp;<a name="fil">*findInLog*</a>    | Specifies keyphrases to find in Framework's execution log. Every keyphrase is either a code or a message from [this document](../../Docs/SPEC/[SPEC][12] Описание сообщений в лог-файлах.docx). If code is used then following format for each entry is used: `'Code: XXXX'`, where `XXXX` is a placeholder of a 4-character code (e.g. `I086`). Messages are used as like they are presented in [this document](../../Docs/SPEC/[SPEC][12] Описание сообщений в лог-файлах.docx), except the case of multi-line messages. In this case " \n " is used as a delimiter of lines. Usage examples: *findInLog*="`'Code: I086', 'Code: I088'`", *findInLog*="`'[Framework] Initialization processing. \n Common plotting parameters are correct.', '[Framework] Initialization processing. \n Plotting parameters are correct.'`". Used by tasks of types `keyPhrase` and `creationHistory`. |
| &nbsp;&nbsp;<a name="ftc">*filesToCheck*</a>     | Specifies path(-s) to check existence for. Used by a task of type `objectExist`. |
| &nbsp;&nbsp;<a name="odftr">*filesToRemove*</a>  | Specifies path(-s) to remove after Framework's call. |
| &nbsp;&nbsp;<a name="odftm">*filesToMove*</a>    | It has the same specification as the one in **\<inputData/>** except performing moving after Framework's call. |

&nbsp;

Table 3.3. - possible commands of *copyIn* and *copyOut*

| Name of the field | Description                                                          |
|-------------------|----------------------------------------------------------------------|
| `none` or ``      | Does nothing. |
| `0` or `clri`     | Empties classifier's 'In' folder. |
| `1` or `spc1`     | Copies contents of folder specified in [*inPath*](#inPath) into classifier's 'In' folder. |
| `2` or `seqh`     | Copies contents of ['def2'](#def2) folder into classifier's 'In' folder; resolves ['rawdataPath'](#rdif); deletes \*.wav file(-s) in classifier's 'In' folder. |
| `def2`            | Copies contents of ['def2'](#def2) folder into classifier's 'In' folder. |
| `def3`            | Copies contents of ['def3'](#def3) folder into classifier's 'In' folder. |
| `delw`            | Deletes \*.wav-files in classifier's 'In' folder. |
| `delf`            | Deletes files defined in either [`outputData/@filesToRemove`](#odftr) or [`inputData/@filesToRemove`](#idftr) (it depends where `delf` is declared: in [*copyIn*](#copyIn) or [*copyOut*](#copyOut)). |
| `movf`            | Moves files defined in either [`outputData/@filesToMove`](odftm) or [`inputData/@filesToMove`](#idftm) (it depends where `movf` is declared: in [*copyIn*](#copyIn) or [*copyOut*](#copyOut)). |
| `daec` or `daef`  | Deletes everything except 'config.xml' in classifier's 'In' folder. |
| `sftp`            | Fetches from SFTP some input data for tests of type [`generateTests`](#generateTests). |
| `cpif`            | For failed tests copies contents of classifier's 'In' folder into 'FunctionalTesting\testsOutPython\outerTaskTag_taskTag\In', where 'outerTaskTag_taskTag' is the name of a folder formed by concatenating tag of a task and tags of its outer tasks. |
| `cpof`            | For failed tests copies contents of classifier's 'Out' folder into 'FunctionalTesting\testsOutPython\outerTaskTag_taskTag\Out', where 'outerTaskTag_taskTag' is the name of a folder formed by concatenating tag of a task and tags of its outer tasks. |

&nbsp;

### <a name="taskGroup">3.1. taskGroup</a>

A task of type `taskGroup` is used for aggregation of other tasks.

```
<taskGroup enable="0" testType="taskGroup">
</taskGroup>
```
Figure 3.1.1. - An example usage of a task with *testType*=`taskGroup` in testingConfigPy.xml 

&nbsp;

### <a name="sftpSync">3.2. sftpSync</a>

A task of type `sftpSync` is used for synchronization local folder with sftp's one(-s) and local copying of some data (see Table 3.2.1., [Example 3](#sftpSyncExample1) for details).

```
<sftpSync enable="0" testType="sftpSync">
	<localPath path="\ComputeFramework\FunctionalTesting\ftpTemp" exclude=""/>
	<remotePath include="/data/Datasets/FunctionalTesting0/SingleTests" exclude=""/>
	<options deletePresentOnlyLocally="0" updateRemote="0" preLocalCopying="0" postLocalCopying="0"/>
</sftpSync>
```
Figure 3.2.1. - An example usage of a task with *testType*=`sftpSync` in testingConfigPy.xml

&nbsp;

Table 3.2.1. - structure of a task with *testType*=`sftpSync`

| Name of the field                      | Description                                                          |
|----------------------------------------|----------------------------------------------------------------------|
| **\<localPath/>**                      | Specifies local path for synchronization. |
| &nbsp;&nbsp;*path*                     | Root path of a local mirror. |
| &nbsp;&nbsp;*exclude*                  | Specifies path(-s) which is(are) ignored during synchronization. |
| **\<remotePath/>**                     | Specifies remote path(-s) to synchronize with. |
| &nbsp;&nbsp;*include*                  | Specifies path(-s) on the remote to synchronize with. |
| &nbsp;&nbsp;*exclude*                  | Specifies path(-s) on the remote which (is)are ignored during synchronization. |
| **\<options/>**                        |                     |
| &nbsp;&nbsp;*deletePresentOnlyLocally* | When *deletePresentOnlyLocally*="`1`" then elements which present locally and absent remotely are deleted; when *deletePresentOnlyLocally*="`0`" then they are placed to the remote.  |
| &nbsp;&nbsp;*updateRemote*             | If *updateRemote*="`0`" then do nothing if a local file is newer than the corresponding remote one; when *updateRemote*="`1`" then upload the file to the remote (with overriding the file which was there before). |
| &nbsp;&nbsp;*preLocalCopying*          | Enables/disables (`1`/`0`) the following chain of actions:<br/><br/>1) Copying everything (except folders starting with '!\_') from '\FunctionalTesting\ftpTemp\SingleTests' to '\FunctionalTesting\testsIn';<br/><br/>2) there's special treatment of folders '!\_defaultInputData\_auto' and '!\_defaultInputData\_history':<br/><br/>&nbsp;&nbsp;2.1)copying \*.wav-files, 'historyFiles' folder, 'files.xml' and 'equipmentProfile.xml' from the corresponding folder located in '\FunctionalTesting\ftpTemp\SingleTests';<br/><br/>&nbsp;&nbsp;2.2) copying 'standardConfig.xml' and 'standardInformativeTags.xml' located in '\ComputeFramework\Classifier\Library\commonFunctions\preProcessing' with renaming into 'config.xml' and 'informativeTags.xml' respectively;<br/><br/>3) for tasks with *testType*="`generateTests`" creating folders specified in *inPath* and copying there 'equipmentProfile.xml' located in '\ComputeFramework\Equipment\\_dataset\_\taskTag', where 'taskTag' is a tag of task's element |
| &nbsp;&nbsp;*postLocalCopying*         | Copying of 'historyFiles' folder from task's folder in 'testIn' into corresponding folder in 'ftpTemp\SingleTests'. This is only done for tasks with *testType*="`generateTests`", *enable*="`1`" and *generate*="`1`". After this synchronization with sftp is performed |

&nbsp;

### <a name="keyPhras e">3.3. keyPhrase</a>

This task is intended for checking the Framework's log for presence of certain codes and messages. The set of codes and messages to look for is stored in ['outputData/@findInLog'](#fil) of the task.

```
<keyPhrase enable="0" testName="runnabilityAllOn" testFuncName="test_runProcessing_runnabilty" testType="keyPhrase" description="check if runProcessing.m script runs and finishes properly">
	<testPath testFuncPath="\ComputeFramework\FunctionalTesting\testsLib\runProcessing\runnabilityAllOn\test_runProcessing_runnabiltyAllOn.m" description="path to the test"/>
	<inputData copyIn="clri, def2, delw, def3" editConfig="equipmentStateDetectionEnable, value, 1; debugModeEnable, value, 0; printPlotsEnable, value, 1; parpoolEnable, value, 1; frequencyTrackingEnable, value, 1; frequencyCorrectionEnable, value, 1; shaftTrajectoryDetectionEnable, value, 0"/>
	<outputData copyOut="cpif, cpof" findInLog="'Code: I086', 'Code: I088', 'Code: 0006', 'Code: 0007', 'Code: 0008', 'Code: 0009', 'Code: 0010', 'Code: 0011'" outPath="" description=""/>
</keyPhrase>	
```
Figure 3.3.1. - An example usage of a task with *testType*=`keyPhrase` in testingConfigPy.xml

&nbsp;

### <a name="objectExist">3.4. objectExist</a>

This task is intended for checking for presence of items in file system after Framework's execution. Path(-s) to check is stored in ['outputData/@filesToCheck'](#ftc).

```
<objectExist enable="0" testName="outDirExistence" testFuncName="test_inOutExistence_outDirExistence" testType="objectExist" description="Checking existence of the @Out directory in /ComputeFramework/Classifier/">
	<testPath findPath="0" testFuncPath="\ComputeFramework\FunctionalTesting\testsLib\inOutExistence\outDirExistence\test_inOutExistence_outDirExistence.m" description="path to the test"/>
	<inputData copyIn="clri, def2" findPath="0" inPath="" description="copyIn=3 - use default files only"/>
	<outputData copyOut="cpif, cpof" outPath="" filesToCheck="\ComputeFramework\Classifier\Out" description=""/>
</objectExist>	
```
Figure 3.4.1. - An example usage of a task with *testType*=`objectExist` in testingConfigPy.xml

&nbsp;

### <a name="dataMatch">3.5. dataMatch</a>
A task of type `dataMatch` is used to compare a status-file generated by the Framework and a reference file. Items to compare are defined by an XPath-expression specified in ['outputData/@datamatch_fields'](#df). For numeric values deviation is allowable. Its threshold is stored in ['outputData/@datamatch_tolerance'](#dt). 
```
<dataMatch enable="0" testName="dataMatchInterf" testFuncName="test_frequencyCorrection_dataMatch" testType="dataMatch" description="check if frequency correction recognises typical cases properly">
	<testPath findPath="0" testFuncPath="D:\Ratgor\GitRepo\FuncTestCopy\ComputeFramework\FunctionalTesting\testsLib\frequencyCorrection\dataMatch\test_frequencyCorrection_dataMatch.m" description="path to the test"/>
	<inputData backupIn="1" copyIn="clri, def2, delw, spc1" findPath="0" inPath="\ComputeFramework\FunctionalTesting\testsIn\frequencyCorrection\dataMatchInterf" description="copy to the input of testing object" editConfig="historyEnable, value, 1; frequencyCorrectionEnable, value, 1"/>
	<outputData copyOut="cpif, cpof" findPath="0" outPath="\ComputeFramework\FunctionalTesting\testsOut\frequencyCorrectionDataMatch" description="compare with output of testing object" datamatch_fields="//*[self::frequencyCorrector]/@estimatedFrequency | /equipment/frequencyCorrector/status/@value" datamatch_tolerance="0.1"/>
</dataMatch>	
```
Figure 3.5.1. -  An example usage of a task with *testType*=`dataMatch` in testingConfigPy.xml

&nbsp;

Table 3.5.1. - description of additional fields in a task with *testType*=`dataMatch`

| Name of the field                                  | Description                                                          |
|----------------------------------------------------|----------------------------------------------------------------------|
| **\<outputData/>**                                 |  |
| &nbsp;&nbsp;<a name="df">*datamatch_fields*</a>    | Contains an XPath-expression which returns fields to compare in status and reference files. In the case when *datamatch\_fields*="" then all items in status and reference will be compared. |
| &nbsp;&nbsp;<a name="dt">*datamatch_tolerance*</a> | Contains either a numeric value of tolerance or an XPath-expression for quering the Framework's config for it. By the way *datamatch\_tolerance* might have an empty value or an XPath-expression might return such value. In both of these cases 1e-9 is used as deviation threshold of numeric values. |

&nbsp;

### <a name="creationHistory">3.6. creationHistory</a>

```
<creationHistory enable="0" testName="runabilityFull" testFuncName="test_creatingHistoryFiles_runabilityFull" testType="creationHistory" description="">
	<testPath testFuncPath="\ComputeFramework\FunctionalTesting\testsLib\creatingHistoryFiles\runabilityFull\test_creatingHistoryFiles_runabilityFull.m" description="path to the test"/>
	<inputData copyIn="2" inPath="\ComputeFramework\FunctionalTesting\testsIn\creatingHistoryFiles" description="copy to the input of testing object" editConfig="historyEnable, value, 1; printPlotsEnable, value, 1; equipmentStateDetectionEnable, value, 1; shaftDisplacementEnable, value, 1; frequencyCorrectionEnable, value, 1; frequencyDomainClassifierEnable, value, 1; timeDomainClassifierEnable, value, 1; timeFrequencyDomainClassifierEnable, value, 1; metricsEnable, value, 1; spmEnable, value, 1; iso15242Enable, value, 1; iso10816Enable, value, 1; iso7919Enable, value, 1; octaveSpectrumEnable, value, 1; decisionMakerEnable, value, 1"/>
	<outputData copyOut="cpif, cpof" outPath="" description="compare with output of testing object" findInLog="'[Framework] Framework processing. \n @status.xml file was successfully updated by history.', '[Framework] History processing. \n History processing COMPLETE.'"/>
</creationHistory>
```
Figure 3.6.1. - An example usage of a task with *testType*=`creationHistory` in testingConfigPy.xml

&nbsp;

### <a name="generateTests">3.7. generateTests</a>

Tasks of type `generateTests` have few essential characteristics.
1. Earlier it [was said](#taskGroups) that task's execution is possible even without presence of **\<taskGroups/>** or without presence of a task in **\<taskGroups/>**. Unfortunately it isn't possible for tasks of type `generateTests` yet. For successful execution of tasks of this type there must be an element representing the task in the **\<taskGroups/>** section and it must have the `generate` attribute.
2. Its sctructure slightly differs from general testing task (because technically its not a single task, but rather a compound one). There are 2 variations of this task: before tests generation and after (figures 3.7.1 and 3.7.2 respectively).
3. To generate tests the flag *generate* of the task's element in **\<taskGroups/>** should be set to `1` (like for `highSpeedBearing` in fig. 2.1.).
3. Tests generation includes history creation as well (i.e. when a task is executed with *generate*="`1`" history is created). After tests have been generated there might be need for history creation only. For this case *generateHistory*="`1`" is used.

```
<generateTests enable="0" testType="generateTests" generateHistory="0" frameworkVersion="v3.3.1" description=""> 
	<inputData copyIn="sftp, 2" inPath="\ComputeFramework\FunctionalTesting\testsIn\highSpeedBearingHistoryDatamatch" editConfig="historyEnable, value, 1;; frequencyCorrectionEnable, value, 1;; frequencyTrackingEnable, value, 1;; bearingsParametersRefinement, value, 1;; evaluation/frequencyTracking, maxPercentDeviation, 6;; evaluation/frequencyTracking, maxPercentDeviationPerSec, 1;; evaluation/frequencyTracking, method, spectrogram;; evaluation/frequencyTracking/spectrogramTracker, type, acc;; evaluation/frequencyTracking/spectrogramTracker/accTracker, frequencyRange, 128:512; 256:1024; 512:2048;;" generateTests="SSR: datamatchHistory; SST: datamatchHistory; BPR: datamatchHistory; Periodicities"/>
	<outputData copyOut="cpif, cpof" outPath=""/>
</generateTests>	
```
Figure 3.7.1. - An example usage of a task with *testType*=`generateTests` before tests generation in testingConfigPy.xml

&nbsp;

```
<generateTests enable="0" testType="generateTests" generateHistory="1" frameworkVersion="v3.3.1" description=""> 
	<inputData copyIn="sftp, 2" inPath="\ComputeFramework\FunctionalTesting\testsIn\highSpeedBearingHistoryDatamatch" editConfig="historyEnable, value, 1;; frequencyCorrectionEnable, value, 1;; frequencyTrackingEnable, value, 1;; bearingsParametersRefinement, value, 1;; evaluation/frequencyTracking, maxPercentDeviation, 6;; evaluation/frequencyTracking, maxPercentDeviationPerSec, 1;; evaluation/frequencyTracking, method, spectrogram;; evaluation/frequencyTracking/spectrogramTracker, type, acc;; evaluation/frequencyTracking/spectrogramTracker/accTracker, frequencyRange, 128:512; 256:1024; 512:2048;;" />
	<outputData copyOut="cpif, cpof" outPath=""/>
	<SSR_datamatchHistory enable="1" testName="SSR_datamatchHistory" testType="datamatchHistory" description="SSR=???" datamatch_fields="//frequencyCorrector/informativeTags/estimatedFrequency/@value | //frequencyCorrector/informativeTags/initialFrequency/@value" datamatch_tolerance="//frequencyCorrector/displacementInterferenceEstimator/rough/@percentStep | //frequencyCorrector/interferenceFrequencyEstimator/rough/@percentStep"/>
	<SST_datamatchHistory enable="1" testType="datamatchHistory" description="" datamatch_fields="//frequencyTracking/informativeTags/type/@value | //frequencyTracking/informativeTags/method/@value | //frequencyTracking/informativeTags/min/@value | //frequencyTracking/informativeTags/max/@value | //frequencyTracking/informativeTags/peak2peak/@value | //frequencyTracking/informativeTags/mean/@value | //frequencyTracking/informativeTags/std/@value | //frequencyTracking/informativeTags/median/@value" datamatch_tolerance="//frequencyTracking/@accuracyPercent" testName="SST_datamatchHistory"/>
	<BPR_datamatchHistory enable="1" testType="datamatchHistory" description="" datamatch_fields="//bearingsParametersRefinement/informativeTags/bearing/@bd | //bearingsParametersRefinement/informativeTags/bearing/@deviation" datamatch_tolerance="//bearingsParametersRefinement/ballDiameter/@percentStep" testName="BPR_datamatchHistory"/>
	<Periodicities_datamatchHistory enable="0" testType="datamatchHistory" description="" datamatch_fields="" datamatch_tolerance="" testName="Periodicities_datamatchHistory"/>
</generateTests>	
```
Figure 3.7.2. - An example usage of a task with *testType*=`generateTests` after tests generation in testingConfigPy.xml

&nbsp;

Table 3.7.1. - description of additional fields in a task with *testType*=`generateTests`

| Name of the field                   | Description                                                          |
|-------------------------------------|----------------------------------------------------------------------|
| **\<inputData/>**                   |  |
| &nbsp;&nbsp;*copyIn*                | *copyIn*="`sftp, 2`" is used by default. |
| &nbsp;&nbsp;*generateTests*         | Defines methods and tests types to generate. It is written in the following format: *generateTests*="`Method: testType`". In the case of multiple tests "; " is used to separate entries: *generateTests*="`Method1: testType1; Method2: testType2.`". |
| &nbsp;&nbsp;*generateHistory*       | Enables/disables (`1`/`0`) history generation. |
| &nbsp;&nbsp;*frameworkVersion*      | Used to fetch from sftp 'equipmentProfile.xml' for specified version. Example usage: *frameworkVersion*="`v3.3.1`". In newer Framework's versions equipmentProfile.xml is stored at '\ComputeFramework\Equipment\\_dataset\_\taskTag', where `taskTag` is a placeholder for a task's element tag (e.g. if a task's element tag is `highSpeedBearing`, then 'equipmentProfile.xml' should be taken from '\ComputeFramework\Equipment\\_dataset\_\highSpeedBearing')
| &nbsp;&nbsp;**\<method_testType/>** | Sub-element representing generated test (e.g. **\<SSR\_datamatchHistory/>** in the Fig. 3.7.2.). It has the following attributes: *enable*, *testType*, *description*, *testName*, *datamatch\_fields*, *datamatch\_tolerance*. Writing format of *datamatch\_fields* and *datamatch\_tolerance* is the same as for tasks of [`datamatch`](#dataMatch) type.  |

&nbsp;

## <a name="descriptionExamples">4. Description examples</a>  

### <a name="taskGroupsExample1">Example 1. taskGroups: re-specifiying attributes' values </a>

Assume we have the following simplified\* xml-snippet (\* - here and further in examples some required elements/attributes are omitted for simplicity):
```
<taskGroups>
	<outerTask>
		<innerTask enable="1" />
	</outerTask>
</taskGroups>

<outerTask enable="1" testType="taskGroup">
	<innerTask enable="0" />
</outerTask>

```
In this example the task `./outerTask/innerTask` will be executed because of:
1) the element `./taskGroups/outerTask` does not have an `enable` attribute, so `./outerTask/@enable`'s value is used;
2) `./taskGroups/outerTask/innerTask` has an `enable` attribute, whose value is used instead of `./outerTask/innerTask`'s one.

&nbsp;

### <a name="inheritanceExample">Example 2. Inheritance</a>

The following xml-snippet illustrates an example usage of inheritance when specifiyng value of *testType*:
```
<parentTask enable="1" testType="keyPhrase">
	<inputData copyIn="def2"/>
	<outputData copyOut="cpif, cpof" findInLog="'Code: I086'"/>
</parentTask>

<inheritedTask enable="0" testType="inherit(parentTask)">
	<outputData findInLog="'Code: I087'" />
</inheritedTask>
```

In the example above `inhertitedTask` inherits all the items of `parentTask` with overriding those specified explicitly.<br/><br/>
Technically, `inheritedTask` has the following structure:
```
<inheritedTask enable="0" testType="keyPhrase">
	<inputData copyIn="def2"/>
	<outputData copyOut="cpif, cpof" findInLog="'Code: I087'" />
</inheritedTask>
```

&nbsp;

### <a name="sftpSyncExample1">Example 3. sftpSync usage</a>

Let's assume we have the following file structure on the remote:
```
root/
├── folder1/
│   ├── fileToIgnoreLocally.ext
│   └── plainFile1.ext
└── someFolder/
    └── folder2/
        ├── fileToIgnoreRemotely.ext
        └── plainFile2.ext
```
and the following [`sftpSync`](#sftpSync) task:
```
<exampleTask enable="1" testType="sftpSync">
	<localPath path="\baseFolder\ftpTemp" exclude="\baseFolder\ftpTemp\folder1\fileToIgnoreLocally.ext"/>
	<remotePath include="/root/folder1, /root/someFolder/folder2" exclude="/root/someFolder/folder2/fileToIgnoreRemotely.ext"/>
	<options deletePresentOnlyLocally="0" updateRemote="0" preLocalCopying="0" postLocalCopying="0"/>
</exampleTask>
```
then after running the task, there will be the following file structure on the local (assuming that there weren't any of the items from the remote before):
```
baseFolder\
└── ftpTemp
    ├── folder1\
    │   └── plainFile1.ext
    └── folder2\
        └── plainFile2.ext
```
