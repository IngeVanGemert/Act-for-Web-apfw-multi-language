# Installation of Act! Premium For Web APFW localized in different languages German French and English
First check that you have an active working installation of Apfw. I have installed Act Premium for Web v24:
<img width="455" height="516" alt="image" src="https://github.com/user-attachments/assets/c08be936-8d0d-4a01-9263-7ef98256baf4" />


your starting point can be  either the English, French or German version of Act! for Web selfhosted.


# step 1 make APFWDE
make a copy of the APFW folder under your installation C:\Program Files\ACT\Act for Web\APFW  and call it APFWDE
<img width="858" height="349" alt="image" src="https://github.com/user-attachments/assets/bd27b899-a121-4cd2-99b4-1561e22f5004" />

Under that folder go to \bin\  and create a folder called \de\
<img width="627" height="296" alt="image" src="https://github.com/user-attachments/assets/4f90b04b-19eb-4970-a8ba-0544af1d54f0" />


# step 2 get localized file
for example from https://www.act.com/de/download/download-act-v24/
unzip but do not install (You have already installed Act for Web, right)

in the installation wizard click browse media

<img width="602" height="450" alt="image" src="https://github.com/user-attachments/assets/b617d6a0-ab3a-4cdc-b26e-bbe2862903fc" />

Look for a file in the installation folder called C:\Act!_Web_v24sp0x204\ACTForWeb\program files 64\ACT\ActInstallDir\APFW\bin\DE-DE\Act.Web.Framework.resources.dll for that language

Copy that file into C:\Program Files\ACT\Act for Web\APFWDE\bin\de\
<img width="617" height="290" alt="image" src="https://github.com/user-attachments/assets/77bc3a09-724a-4edd-b98e-bf48dfc214e5" />

Make sure you use the exact same version from your own installation located a "C:\Program Files\ACT\Act for Web\APFW\bin\Act.Web.Framework.dll" .

# step 3 create website in iis
make sure you point to the new folder
<img width="888" height="475" alt="image" src="https://github.com/user-attachments/assets/fbe061e9-caef-4a5d-a9ba-57c7440b1940" />

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

Go to youw web installation and it should now be in German! https://yourhost/apfwde
<img width="497" height="520" alt="image" src="https://github.com/user-attachments/assets/b48811bc-00c1-44f1-a667-9efaf5fc5af7" />

# step 6 add database 
In Act! go to tools - website administration and add database to this website
<img width="411" height="485" alt="image" src="https://github.com/user-attachments/assets/3009ec3e-e853-4222-8d89-e502a7c032d2" />
You should now be able to login on the website and see German

# step 7 add dropdown list of languages

If you want to have an option to switch between languages:

You need to make a copy of the full APFW folder for each language, for example so youget:
C:\Program Files\ACT\Act for Web\APFW (which is English in my case)
C:\Program Files\ACT\Act for Web\APFWDE (German)
C:\Program Files\ACT\Act for Web\APFWFR (French) 
with all the files inside that filder. 

The German version will have the German language file in the folder:
C:\Program Files\ACT\Act for Web\APFWDE\bin\de\Act.Web.Framework.resources.dll

The French version will have the French language file in the folder:
C:\Program Files\ACT\Act for Web\APFWFR\bin\fr\Act.Web.Framework.resources.dll


You need to create a website for each language in IIS under default website


Then add the language switcher into the main index file in each of the apfw folders.
Add this to default.aspx:
<img width="983" height="232" alt="image" src="https://github.com/user-attachments/assets/3ee76e4b-8310-4cd3-af0b-5339a30e5b17" />



and then add this to where you want your drop down language selector to be probably above the database dropdown:

	    <div class="cent space">
 <asp:DropDownList ID="ddlLanguages" runat="server" CssClass="act-input" 
    onchange="if (this.value) window.location.href=this.value;">
    <asp:ListItem Text="-- Select a Language --" Value="" />
	<asp:ListItem Text="English" Value="https://myhost/apfw" />
    <asp:ListItem Text="German" Value="https://myhost/apfwde" />
    <asp:ListItem Text="French" Value="https://myhost/apfwfr" />
</asp:DropDownList>
    <div class="cent space">

<img width="436" height="560" alt="image" src="https://github.com/user-attachments/assets/08d13d3f-850b-4358-975d-a7ba46b7a17a" />
