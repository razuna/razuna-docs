### Plugins

**Workflow**

The Razuna Workflow plugin give you the option to automate many different tasks during an event in Razuna. The Razuna Workflow plugin is a payable plugin and a license can be bought from Razuna. Please [contact us to do so](mailto:sales@razuna.com).

___

**Installing the plugin**

Once you received the plugin you can upload it within Razuna with the "Add new" link. Take the workflow.zip and select it. The plugin will then install itself.

![](/admin/img/Screenshot1.png)
___

**Activating the plugin**

Once installed you should see the plugin in the list. In order to use it within Razuna you have to activate it and additionally choose which tenant is allows to use the workflow plugin.

![](/admin/img/Screenshot2.png)

Activate the plugin with the "activate" link. Now, you need to assign the plugin to each host you want to use the plugin. Do so by selecting the "Plugin tenant activation" tab and check each tenant you want to have access to the workflow.

![](/admin/img/Screenshot3.png)

Click on "Save" and the plugin will be activated/deactivated for each tenant. 

___

**Accessing the plugin**

Once the plugin has been installed and activated, you can access it from the Razuna DAM admin panel. Please note that it will only be available, if you have acticated it on the relevant tenant as described in the link above. 

To access the plugin, go to the Administration section by clicking on your name top right and selcting "Administration." In the administration panel go to the "Plugins" tab. If you have installed the plugin correctly, you will now see it in the list of installed plugins.

___

**Creating a workflow**

In order to create a workflow, click on "Settings" below the plugin. If you have not created any workflows before, you can create your first workflow be naming it in the first field and writing a description in the second field and then clik "Add new."

The workflow is now created and will show up in the list of workflows.

___

**Editing a workflow**

By clicking on "Edit" in the list of workflows, you will be taken to the Workflow Edit menu. 

First select which Event should trigger and Action. You can add as many events and actions to each workflow as you wish.

**Defining an Event**

To define the Event, click on the dropdown to select the relevant Event.

Choose between:

   * Add file(s)
       * The action is triggered upon upload/ingest
   * Edit file(s)
       * The action is triggered, if a file is edited
   * Move files(s)
       * The action is triggered, if a file is moved
   * Delete files(s)
       * The action is triggered, if a file is deleted
   * Add folder
       * The action is triggered, if a folder is added

![](/admin/img/image20131.png)

**Defining an Action**

Once you have chosen the event, you can now select the action to be carried out.

You can choose between the following actions:

   * Notify users/groups
       * Will notify users and/or groups that an asset has been added with you custom message and the assets ID
   * Move asset(s)
       * Will move the asset to a folder that you specify
   * Apply rendition template
       * This will add a rendition template (convert the asset). You need to have created a rendition template first.
   * Call external URL
       * This will call an external URL, f.ex. [www.yoursite.com/?xxxx](www.yoursite.com/?xxxx) where xxxx is all asset information (name, ID, metadata)
   * Add value to metadata field
       * This will allow you to automatically assign values to standard meta-data fields (XMP, IPTC)
   * Add value to custom field
       * This will allow you to automatically assign values to a custom field
   * Add label(s)
       * This will allow you to automatically add one or more labels to the asset

![](/admin/img/image20132.png)

**Adding more Actions**

Once you have selected an action, you can add more actions by repeating the steps above. You cannot have multiple events in one workflow, but you may add as many actions as you wish. So once an action has been added, simply click on "Select Action(s)" for this workflow and add you next action. It will automatically be added below the previous action.

**Reorder the Actions**

You can reorder the Actions by clicking on the green Reorder icon and move the actions up or down.

![](/admin/img/image20133.png)

Once completed click on "Save Workflow". The workflow will be saved but you will remain in the same window.

___

**Adding a workflow to a folder**

In order to add the workflow to a folder, simply go to the desired folder and click on "Folder Sharing & Settings" in the top right part of the pane.
On the first tab, "Folder Settings" you will see the workflow menu at the very bottom below your user groups. It's headed: "Apply workflow to files in this folder"
Click in the field below and select the desired workflow, which you want to attach to the folder. You can attach multiple workflows to the same folder.

![](/admin/inmg/image20134.png)

___

**Metadata Form Plugin**

The Razuna metadata form plugin is a simple plugin that allows you to force the users to fill in certain fields upon upload of new assets to Razuna. You can force the user to fill in one or more fields. If not filled in, the assets will not be added. The plugin is a global plugin for each tenant and if activated will work across all folders and user groups.

**Accessing the Metadata Plugin**

Once the plugin has been installed and activated, you can access it from the Razuna DAM admin panel. Please note that it will only be available, if you have acticated it on the relevant tenant as described in the link above. 

To access the plugin, go to the Administration section by clicking on your name top right and selcting "Administration." In the administration panel go to the "Plugins" tab. If you have installed the plugin correctly, you will now see it in the list of installed plugins.


**Configuring the Metadata Plugin**

By clicking on "Settings" underneath the metadata plugin, you will access the configuration page. 

![](/admin/img/image20135.png)

First select whether the Metaform is active or inactive. Ny default it will be inactive.

Next decide which field(s) must be filled in. You can select all custom fields as well as the default fields in first file information tab, i.e. file name, keywords, description and labels.

If you need to add more fields, simply click on "Add field" and then another Metadata field dropdown will show up underneath the previous. You may reorganize the order of the fields by clicking on the green reorder icon. You can decide whether a field is required or not by selcting the appropriate radio button.

Once completed, click on Save Settings. Your users will now be prompted to fill in the required (or optional) fields upon upload.


___
* Razuna Metaform Plugin : The metaform plugin gives you the option to add a metadata form during uploading.

* Razuna Workflow Plugin : Workflow plugin by the official Razuna Team. Delivers mechanism to put assets and folders into a workflow.

![](img/admin_plugins.jpg)

___

Razuna Metaform Plugin Setting :

![](img/admin_plugins_Metaform_setting.jpg)


___

Razuna Workflow Plugin Setting :

![](img/admin_plugins_workflow_setting1.jpg)

___