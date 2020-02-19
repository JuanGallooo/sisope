# WINDOWS POWERSHELL TALLER 1

En este archivo md se encuentra el desarrollo de las preguntas del taller de PowerShell.

# PRIMERA

PS C:\Users\Juan Esteban Gallo\Desktop\Archivos> cd .\ejercicios

PS C:\Users\Juan Esteban Gallo\Desktop\Archivos\ejercicios> notepad archivo1.txt

PS C:\Users\Juan Esteban Gallo\Desktop\Archivos\ejercicios> notepad archivo2.txt

PS C:\Users\Juan Esteban Gallo\Desktop\Archivos\ejercicios> Compare-Object -ReferenceObject (Get-Content .\archivo1.txt) -DifferenceObject (Get-Content .\archivo2.txt)

```
InputObject                           SideIndicator

Contenido dos completamente diferente =>           
Contenido 1                           <=           
```

PS C:\Users\Juan Esteban Gallo\Desktop\Archivos\ejercicios> 

2.

out-file : No se puede procesar el argumento porque el valor del argumento "path" es NULL. Cambie el valor del argumento "path" a un valor no nulo.
En línea: 1 Carácter: 42

```
+ get-service | export-csv servicios.csv | out-file
+                                          ~~~~~~~~
    + CategoryInfo          : InvalidArgument: (:) [Out-File], PSArgumentNullException
    + FullyQualifiedErrorId : ArgumentNull,Microsoft.PowerShell.Commands.OutFileCommand
```
Primeramente se puede ver un error de que no existe un path especificado para out-file.
Ademas de que el | al reaclizar un proceso de exportacion no retorna ningun objeto en el que se pueda trabajar.

3.

El uso del parametro delimiter permite cambiar el uso de este char para separar por cualquier caracter especificado 

``[[-Delimiter] <Char>]`` 

en este caso utilizariamos 

``Get-Process | Export-Csv procesos.csv -Delimiter ";"`` 


4.

El parametro para no permitir una sobre escritura, sirve mucho cuando creas muchos archivos y con pequeñas variaciones
en el nombre, por tanto no entras en el error de sobre escribir un archivo por equivocación.

``[-NoClobber]``

Esto permite no crear el archivo si ya existe en el directorio.

```
PS C:\Users\Juan Esteban Gallo\Desktop\Taller PoweShell\Archivos> Get-Process | Export-Csv procesos.csv -NoClobber

Export-Csv : El archivo 'C:\Users\Juan Esteban Gallo\Desktop\Taller PoweShell\Archivos\procesos.csv' ya existe.
En línea: 1 Carácter: 15
+ Get-Process | Export-Csv procesos.csv -NoClobber
    + CategoryInfo          : ResourceExists: (C:\Users\Juan E...os\procesos.csv:String) [Export-Csv], IOException
    + FullyQualifiedErrorId : NoClobber,Microsoft.PowerShell.Commands.ExportCsvCommand
	
```
 
5.
El comando que podriamos utilizar para cambiar la lista de idiomas , especificando un nuevo idioma de listas a utilizar.

Especificariamos como parametro el idioma que contenga el separador del sistema como separador determinado.

``Set-WinUserLanguageList -LanguageList (New-WinUserLanguageList -Language en-GB) -Force`` 

Apartir de una consulta o listado utlizamos el export-csv procesos.csv
Un ejemplo podría ser la obtención de servicios como :

``get-process | export-csv procesos.csv`` 

Para especificar a una ruta en la cual esportar utilizamos el -path osino se iría a documentos de manera determinada.

6.


``Get-Random 10``

Este comando obtendrá un número entre 0 y 9

``Get-Random 10 -Minimum 3``
Este comando obtendrá un número entre 3 y 9

``5 | Get-Random``

Este comando obtendrá un número entre 0 y 4


PS C:\Users\Juan Esteban Gallo\Desktop\Taller PoweShell\Archivos> Get-Random 10
2


7.

``Get-date``

PS C:\Users\Juan Esteban Gallo\Desktop\Taller PoweShell\Archivos> get-date

martes, 18 de febrero de 2020 11:03:57

8.

Retorna un DateTime objet que representa la fecha actual o una fecha que usted especifica.


```
PS C:\Users\Juan Esteban Gallo\Desktop\Taller PoweShell\Archivos> (get-date).GetType()

IsPublic IsSerial Name                                     BaseType                                                                                                                                      
-------- -------- ----                                     --------                                                                                                                                      
True     True     DateTime                                 System.ValueType 
```

9.

``get-date| Select-Object -Property "DayOfWeek"``

PS C:\Users\Juan Esteban Gallo\Desktop\Taller PoweShell\Archivos> get-date| Select-Object -Property "DayOfWeek"

DayOfWeek
---------
  Tuesday

10.

``Get-WmiObject`` 
El comando mencionado obtiene instancias de las clases de WMI o información sobre las clases de WMI disponibles, en las 
que se encuentra la clase Win32_QuickFixEngineering donde se representa una pequeña actualización a nivel de todo 
el sistema, comúnmente conocida como actualización de ingeniería rápida (QFE)

PS C:\Users\Juan Esteban Gallo\Desktop\Taller PoweShell\Archivos> Get-WmiObject Win32_QuickFixEngineering 

```
Source        Description      HotFixID      InstalledBy          InstalledOn              
------        -----------      --------      -----------          -----------              
PLUR          Update           KB4534132     NT AUTHORITY\SYSTEM  14/02/2020 0:00:00       
PLUR          Security Update  KB4515383     NT AUTHORITY\SYSTEM  06/10/2019 0:00:00       
PLUR          Security Update  KB4516115     NT AUTHORITY\SYSTEM  07/10/2019 0:00:00       
PLUR          Security Update  KB4521863     NT AUTHORITY\SYSTEM  09/10/2019 0:00:00       
PLUR          Security Update  KB4524569     NT AUTHORITY\SYSTEM  15/11/2019 0:00:00       
PLUR          Security Update  KB4528759     NT AUTHORITY\SYSTEM  20/01/2020 0:00:00       
PLUR          Security Update  KB4537759     NT AUTHORITY\SYSTEM  14/02/2020 0:00:00       
PLUR          Security Update  KB4538674     NT AUTHORITY\SYSTEM  14/02/2020 0:00:00       
PLUR          Update           KB4532693     NT AUTHORITY\SYSTEM  14/02/2020 0:00:00       
```

11.

Comando utilizado 
`` Get-WmiObject Win32_QuickFixEngineering | Select-Object -Property InstalledOn, CSName ,HotFixID`` 

PS C:\Users\Juan Esteban Gallo\Desktop\Taller PoweShell\Archivos>  Get-WmiObject Win32_QuickFixEngineering | Select-Object -Property InstalledOn, CSName ,HotFixID

```
InstalledOn        CSName HotFixID 
-----------        ------ -------- 
14/02/2020 0:00:00 PLUR   KB4534132
06/10/2019 0:00:00 PLUR   KB4515383
07/10/2019 0:00:00 PLUR   KB4516115
09/10/2019 0:00:00 PLUR   KB4521863
15/11/2019 0:00:00 PLUR   KB4524569
20/01/2020 0:00:00 PLUR   KB4528759
14/02/2020 0:00:00 PLUR   KB4537759
14/02/2020 0:00:00 PLUR   KB4538674
14/02/2020 0:00:00 PLUR   KB4532693
```
12.

El comando utilizado fue el siguiente 

``PS C:\Users\Juan Esteban Gallo\Desktop\Taller PoweShell\Archivos> Get-WmiObject Win32_QuickFixEngineering | Select-Object -Property InstalledOn, CSName ,HotFixID, Description | Sort-Object -Property Description|  ConvertTo-HTML | Out-file hotFixes.html``


Guardando un archivo el cual se encuentra en la carpeta sources de este repositorio hotFixes.html .

13.

El comando utilizado fue el siguiente

`` Get-EventLog -LogName system -Newest 50| Sort-Object -Property TimeWritten,Index | Select-Object -Property Index, TimeWritten, Source``

PS C:\Users\Juan Esteban Gallo\Desktop\Taller PoweShell\Archivos> Get-EventLog -LogName system -Newest 50| Sort-Object -Property TimeWritten,Index | Select-Object -Property Index, TimeWritten, Source

```
Index TimeWritten         Source                       
----- -----------         ------                       
80988 18/02/2020 12:57:34 Microsoft-Windows-WHEA-Logger
80989 18/02/2020 12:57:34 Microsoft-Windows-WHEA-Logger
80990 18/02/2020 12:57:48 Microsoft-Windows-WHEA-Logger
80991 18/02/2020 12:57:48 Microsoft-Windows-WHEA-Logger
80992 18/02/2020 12:58:17 Microsoft-Windows-WHEA-Logger
80993 18/02/2020 12:58:20 Microsoft-Windows-WHEA-Logger
80994 18/02/2020 12:59:28 Microsoft-Windows-WHEA-Logger
80995 18/02/2020 13:00:15 Microsoft-Windows-WHEA-Logger
80996 18/02/2020 13:01:01 Microsoft-Windows-WHEA-Logger
80997 18/02/2020 13:01:18 Netwtw04                     
80998 18/02/2020 13:01:22 Microsoft-Windows-WHEA-Logger
80999 18/02/2020 13:01:36 Microsoft-Windows-WHEA-Logger
81000 18/02/2020 13:03:30 Microsoft-Windows-WHEA-Logger
81001 18/02/2020 13:03:41 Microsoft-Windows-WHEA-Logger
81002 18/02/2020 13:04:43 Microsoft-Windows-WHEA-Logger
81003 18/02/2020 13:04:48 Microsoft-Windows-WHEA-Logger
81004 18/02/2020 13:05:10 Microsoft-Windows-WHEA-Logger
81005 18/02/2020 13:05:30 Microsoft-Windows-WHEA-Logger
81006 18/02/2020 13:06:50 Microsoft-Windows-WHEA-Logger
81007 18/02/2020 13:06:55 Microsoft-Windows-WHEA-Logger
81008 18/02/2020 13:06:55 Microsoft-Windows-WHEA-Logger
81009 18/02/2020 13:07:01 Microsoft-Windows-WHEA-Logger
81010 18/02/2020 13:07:49 Microsoft-Windows-WHEA-Logger
81011 18/02/2020 13:08:14 Microsoft-Windows-WHEA-Logger
81012 18/02/2020 13:08:20 Microsoft-Windows-WHEA-Logger
81013 18/02/2020 13:08:26 Microsoft-Windows-WHEA-Logger
81014 18/02/2020 13:08:46 Microsoft-Windows-WHEA-Logger
81015 18/02/2020 13:08:52 Microsoft-Windows-WHEA-Logger
81016 18/02/2020 13:08:56 Microsoft-Windows-WHEA-Logger
81017 18/02/2020 13:09:36 Microsoft-Windows-WHEA-Logger
81018 18/02/2020 13:10:09 Microsoft-Windows-WHEA-Logger
81019 18/02/2020 13:11:33 Microsoft-Windows-WHEA-Logger
81020 18/02/2020 13:12:18 Microsoft-Windows-WHEA-Logger
81021 18/02/2020 13:12:23 Microsoft-Windows-WHEA-Logger
81022 18/02/2020 13:12:51 Microsoft-Windows-WHEA-Logger
81023 18/02/2020 13:13:08 Microsoft-Windows-WHEA-Logger
81024 18/02/2020 13:13:13 Microsoft-Windows-WHEA-Logger
81025 18/02/2020 13:14:32 Microsoft-Windows-WHEA-Logger
81026 18/02/2020 13:14:42 Microsoft-Windows-WHEA-Logger
81027 18/02/2020 13:14:57 Microsoft-Windows-WHEA-Logger
81028 18/02/2020 13:15:37 Microsoft-Windows-WHEA-Logger
81029 18/02/2020 13:16:05 Microsoft-Windows-WHEA-Logger
81030 18/02/2020 13:16:29 Microsoft-Windows-WHEA-Logger
81031 18/02/2020 13:16:53 Microsoft-Windows-WHEA-Logger
81032 18/02/2020 13:17:04 Microsoft-Windows-WHEA-Logger
81033 18/02/2020 13:18:25 Microsoft-Windows-WHEA-Logger
81034 18/02/2020 13:18:40 Microsoft-Windows-WHEA-Logger
81035 18/02/2020 13:19:25 Microsoft-Windows-WHEA-Logger
81036 18/02/2020 13:19:52 Microsoft-Windows-WHEA-Logger
81037 18/02/2020 13:19:52 Microsoft-Windows-WHEA-Logger
```



