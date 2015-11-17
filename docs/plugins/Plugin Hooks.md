# Plugin Hooks

> **Plugin API** : *The plugin API is available as of Razuna 1.6.*

Following is a listing of all the available hooks. Hooks allow you to execute your plugin code/pages within Razuna.

Example: You want that your code gets executed when the user adds a file to Razuna. In order to do so, you need to let Razuna know (register) your function. In order to register your hook you need to call the add_action() function and pass in the required parameters with one of the hooks below as in:

```
<cfset add_action(pid="#this.myID#", action="on_file_add", comp="mycomponent", func="myfunction")>
```

Here we register the component ("yourcomponent") with the function ("myfunction") when a file is being added (action="on_file_add"). Thus your function will be executed when a new file is uploaded.

   * settings
   * on_folder_settings
   * on_file_add
   * on_file_edit
   * on_file_remove
   * on_file_move
   * on_folder_remove
   * on_rendition_add
   * show_in_direct_link
   * show_in_folderview_select_wx
   * show_in_folderview_select_r
   * add_tab_detail_wx
   * show_in_detail_link_wx

___

**settings**

*This will be called when users enters the settings page of the plugin administration.*

___

**on_folder_settings**

*Will include your code on the folder properties page.*

___

**on_file_add**

*Will execute when files(s) are being added to a folder which has this hook activated. Executes on uploading of file and when files are being moved into this folder as well.*

___

**on_file_edit**

*Will execute when users are saving a file.*

___

**on_file_remove**

*Will execute when the file(s) are being removed.*

___

**on_file_move**

*Will execute on any move action of the file(s). This action is being triggered when a file is being move out or into a folder!*

___

**on_folder_remove**

*Will execute when the folder is being removed.*

___

**on_rendition_add**

*Will execute when a new rendition is being created.*

___

**show_in_direct_link**

*When user clicks on direct link, the content of this hook will be shown (useful if you want to show a custom link).*

___

**show_in_folderview_select_wx**

*Content of your plugin to show when user selects files in the folderview. The "_wx" means that the content is being shown to all users who have NOT read permission.*

|Return variable|example|
|---------------|-------|
|plwx|result.cfc.plwx.(functionname).(variablename)|

___

**show_in_folderview_select_r**

*Content of your plugin to show when user selects files in the folderview. The "_r" means that the content is being shown to all users who ONLY have read permission.*


|Return variable|example|
|---------------|-------|
|plr|result.cfc.plr.(functionname).(variablename)|

___

**add_tab_detail_wx**

*This adds an additional tab and a div to the files detail view. The div will be called according to your function (just like the view). The "_wx" means that the content is being shown to all users who have NOT read permission. The following parameters are available to you;*

|name|value||
|----|-----|-----|
|result.cfc.plwx.(functionname).file_id|The ID of the file||
|result.cfc.plwx.(functionname).folder_id|The FOLDERID the file is in||
|result.cfc.plwx.(functionname).cf:show|The FILE TYPE|img = images ; vid = videos ; aud = audios ; doc = documents|

*With these 3 variables you can continue calling your own plugin code like: &file_id=#attributes.file_id#&type=#attributes.cf_show#&folder_id=#attributes.folder_id#*

*In order to create the tab you have to add the following line in your view:*

```
<li><a href="##yourfunction" onclick="loadcontent('yourfunction','index.cfm?fa=c.plugin_direct&comp=yourcomponent&func=yourfunction&file_id=#result.cfc.plwx.(functionname).file_id#&folder_id=#result.cfc.plwx.(functionname).folder_id#&type=#result.cfc.plwx.(functionname).cf_show#');">My tab</a></li>
```

*This will add a new tab to the detail view and at the same time create a div with the name of the view! Thus make sure that the "yourfunction" is of the same value!*

|Return variable|example|
|---------------|-------|
|pllink|result.cfc.pllink.(functionname).(variablename)|


