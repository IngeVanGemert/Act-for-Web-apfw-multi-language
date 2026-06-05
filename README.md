First check that you have an active working installation of Apfw. I have installed Act Premium for Web v24:
<img width="455" height="516" alt="image" src="https://github.com/user-attachments/assets/c08be936-8d0d-4a01-9263-7ef98256baf4" />


your starting point can be  either the English, French or German version of Act! for Web selfhosted.


# step 1 make APFWDE
make a copy of the APFW folder under your installation C:\Program Files\ACT\Act for Web\APFW and call it APFWDE 
under that folder go to \bin\  and create a folder called \de\


# step 2 get localized file
for ecample from https://www.act.com/de/download/download-act-v24/
unzip but do not install (You have already installed Act for Web, right)

in the installation wizard click browse media

<img width="602" height="450" alt="image" src="https://github.com/user-attachments/assets/b617d6a0-ab3a-4cdc-b26e-bbe2862903fc" />

Look for a file in the installation folder called C:\Act!_Web_v24sp0x204\ACTForWeb\program files 64\ACT\ActInstallDir\APFW\bin\DE-DE\Act.Web.Framework.resources.dll for that language

copy that file into C:\Program Files\ACT\Act for Web\APFWDE\bin\de\

Make sure you use the exact same version from your own installation located a "C:\Program Files\ACT\Act for Web\APFW\bin\Act.Web.Framework.dll" .
# step 3 create website in iis
<img width="888" height="475" alt="image" src="https://github.com/user-attachments/assets/fbe061e9-caef-4a5d-a9ba-57c7440b1940" />

make sure you pint to the new folder
set the authorisation / impersonation correct and test the connection

<img width="696" height="481" alt="image" src="https://github.com/user-attachments/assets/09977a9d-b258-4622-9639-2a198dc51afc" />
# step 4 select language
in iis in globalization choose German (de)
<img width="1171" height="321" alt="image" src="https://github.com/user-attachments/assets/71fcc26b-7151-4202-9fca-12f352d3e530" />

as alternative you can:
Open web.config  in notepad
Look for the word 'glob'
Edit:
  <globalization culture="de" uiCulture="de" requestEncoding="utf-8" responseEncoding="utf-8" />
reset iis

# step 5 test

go to youw web installation and it should now be in German!
<img width="497" height="520" alt="image" src="https://github.com/user-attachments/assets/b48811bc-00c1-44f1-a667-9efaf5fc5af7" />

 # step 6 add database 
 In Act! go to tools - website administration and add database to this website
 
 <img width="411" height="485" alt="image" src="https://github.com/user-attachments/assets/3009ec3e-e853-4222-8d89-e502a7c032d2" />
you should now be able to login and see german
# step 7 add dropdown list of languages

this will change your installation into German
If you want to have an option to switch between languages:
You need a separate application pool for each language.
You need to make a copy of the full APFW folder for each language, for example so youget:
C:\Program Files\ACT\Act for Web\APFW
C:\Program Files\ACT\Act for Web\APFWDE
C:\Program Files\ACT\Act for Web\APFWFR
with all the files inside that filder. 

The German version will have the German language file in the folder:
C:\Program Files\ACT\Act for Web\APFWDE\bin\de\Act.Web.Framework.resources.dll

The French version will have the French language file in the folder:
C:\Program Files\ACT\Act for Web\APFWFR\bin\fr\Act.Web.Framework.resources.dll



You need to create an application pool for each language and a website for each language in IIS under default website


Then add the language switcher into the main index file:
Add this to the top of default.aspx:
<!--taal-->
<script runat="server">
  protected void selectLanguage_SelectedIndexChanged(object sender, EventArgs e)
    {
 InitializeCulture();     
   System.Threading.Thread.CurrentThread.CurrentUICulture = System.Globalization.CultureInfo.CreateSpecificCulture(selectLanguage.SelectedValue);
    }
</script>
<!--EINDE taal-->


and then add this to where you want your drop down language selector to be probably above the database dropdown:



<!--taal verwijzing-->
<div>
<label for="ddlDatabaseSelector" id="lblLanguage" style="font-weight:bold;">Language:</label>

<asp:DropDownList runat="server" AutoPostBack="true" ID="selectLanguage" OnSelectedIndexChanged="selectLanguage_SelectedIndexChanged">
            <asp:ListItem Text="English" Value="en-IE"></asp:ListItem>
            <asp:ListItem Text="German" Value="de" selected></asp:ListItem>
German
        </asp:DropDownList>
</div>
<!--EINDE taal verwijzing-->

