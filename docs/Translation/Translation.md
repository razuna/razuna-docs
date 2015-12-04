**Translations**

> **Razuna 1.6** : As of Razuna 1.6 we have changed the translation system.

___

**Translation Razuna 1.6 and later**

Since Razuna 1.6 we store all translations in a central location and they are available for all tenants. Translations are hold in .properties files. Please read below how you can translate and extend the translation system.

___

**Translate Razuna to your language**

> *This section is for **ADDING** a translation. If you would like to **CUSTOMIZE** wording then please see the dedicated section for this!*

> **Public translation** : As of Razuna 1.6 all translations live at a centralized place at [http://translate.razuna.org](http://translate.razuna.org./). You can use this service to translate Razuna into your respected language anytime!

|Language|ID|Provider|
|--------|--|--------|
|English|1|Nitai|
|German|2||
|French|3|Bruce Lane|
|Dutch|4|David Wuyts|
|Danish|5||	 
|Arabic|	6|	Walid Zaiaty|
|Vietnamese|	7|	Phan Chi Nguyen|
|Romanian|	8|	Florin Bubuianu|
|Spanish|	9|	Julio Torres|
|Italian|	10|	 |
|Norwegian|	11||	 
|Slovenian|	12||	 
|Ukrainian|	13||	 
|Brazilian|	14||	 
|Catalan|	15||	 
|Chinese_Simplified|	16||	 
|Chinese_Traditional|	17||	 
|Hungarian|	18||	 
|Persian	|19||	 
|Swedish	|20	|| 
|Portugese|	21||	 
|Japanese|	22||	 
|Russian|	23	||

___

**Customize a translation**

If you want to change the wording of a translation you can do so by creating a new directory in the tenant directory named with the same translation and place the HomePage.properties file inside.The structure would look like this:

raz1/dam/translation/custom/English

In order to overwrite existing translations with your own you would simply overwrite it within the custom translation. Say you want to a different wording for "welcome" you would simply add "welcome" into your properties file and add your own translation.

Once saved, you do not need to do anything else. Razuna will pick up the custom translation immediately.

___

**Translation Pre-1.6 release**

*Translate Razuna to your language*

Razuna holds all translations in XML files. Thus, in order to translate Razuna to your preferred language you simply have to create a new XML file, give it the name of your language and add it to Razuna. Please follow the below guidelines to translate.

*Location of translation files.*

Actually there are 2 (TWO) translations available within Razuna. One is for the General Administration, found at [http://localhost:8080/razuna/admin](http://localhost:8080/razuna/admin), where the CMS and administration takes place and the other is for the Digital Asset Management (DAM) part. Mostly this is the one you want to translate, since your users are interacting with this part to 99%.

You can find the XML files at;

For the **DAM** you can find the translation files in your "Host" folder in the folder "translations" (demo/dam/translations).

For the **Admin** you can find them at "Admin/translations".

When you want to test your translation you will have to put it into one of those places.

___

**How to start translating**

    
**Grab the latest English.xml file**

  Best is to get it from the Subversion (SVN) repository. Thus when we do changes those will be reflected in the SVN. Read over at the Subversion Guide how to access Razuna on SVN. The main thing for you to know is that the translation files reside in the "trunk" folder under the demo host (demo/dam/translations). If you don't feel comfortable with SVN access then let us know and we will send you the XML by another way.
    
**Create your own XML file**
    
  Open the english.xml file and copy it to your preferred language. Say you want to create a Italian translation you would copy the english.xml to italian.xml.
    
**Change the ID**

  Each translation has its own ID. You will need to change this ID! Incrementing it by one with the below list. Look at the below list to see what ID's are taken and add your own translation and ID.
    
**Let us know**

  Once you started add your status in the below table (yes, you can edit it) and let us know that you work on it. Of course, we would totally appreciate if you would send us a copy of your file. We will give you praise and mention your name wherever we can (smile) 


___

**Available Translations and their IDs**

Here is a list of available translations and their ID's

|Language|File Name|ID|Provider|1.3.5|1.4|
|--------|---------|--|--------|-----|---|
|English|english.xml|1|Nitai|done|done|
|German|german.xml|2|Nitai|done|done|
|French|french.xml|3|Bruce Lane|done|open|
|Dutch|dutch.xml|4|David Wuyts|done|open|

___

**Escaping foreign characters in the XML file**

**Important**

```
<![CDATA[Deconnexion]]>
```

Without wrapping this French word in CDATA the parsing of this XML file would fail, since the parser does not know French or foreign characters. The same applies if you would like to add HTML code in your translation. In short, you have to wrap all text with a CDATA when it would contain HTML or foreign characters.

HTML in XML

```
<![CDATA[I want this word to be <b>bold</b> and have a paragraph <p>in this text</p>]]>
```
In order to be able to read/parse the XML file properly all characters have to be escaped in a XML file. Now to make life easy on you, you can wrap your text in a "CDATA". Please take a look at the following example;


