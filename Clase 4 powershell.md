# WINDOWS POWERSHELL Clase 4

En este archivo md se encuentra el desarrollo de las preguntas del taller de PowerShell de la clase 4

#1

Mostrar una tabla de procesos que incluya únicamente los nombres de los procesos, sus IDs, y si están respondiendo a Windows (la propiedad Responding muestra eso). Haga que la tabla tome el mínimo de espacio horizontal, pero no permita que la información se trunque.


`` Get-Process | select name,id,responding | ft -Wrap ``

Resultado

```
Name                    Id Responding
----                    -- ----------
AdobeUpdateService    4012       True
AGMService            4120       True
AGSService            4156       True
ApplicationFrameHost 11288       True
AppVShNotify          9064       True
audiodg               2524       True
browser_broker       13100       True
Calculator            3272      False
CAudioFilterAgent64  19308       True
         
```

#2

 Muestre una tabla de procesos que incluya los nombres de los procesos y sus IDs. También incluya columnas para uso de memoria virtual y física; exprese dichos valores en megabytes (MB).

``Get-Process | ft -Property name, id, @{n='VM (MB)'; e={$_.VM / 1MB -as [int]}}, @{n='PM (MB)' ; e={$_.PM / 1MB -as [int]}}``

Resultado
```
Name                      Id VM (MB) PM (MB)
----                      -- ------- -------
AdobeUpdateService      4012      45       1
AGMService              4120      59       2
AGSService              4156      64       3
ApplicationFrameHost   11288 2101548      67
AppVShNotify            9064    4177       2
audiodg                 2524 2101417      16
backgroundTaskHost      1768 2101810       8
browser_broker         13100 2101341       2
Calculator              3272    4527      20
CAudioFilterAgent64    19308    4198       2
CNMNSST2               14632      67       1
CompPkgSrv              5160 2101340       2
conhost                 3480 2101335       6
```

#3 

Emplee Get-EventLog para mostrar una lista de los logs de eventos disponibles (revise la ayuda para encontrar el parámetro que le permitirá obtener dicha información). Formatee la salida como una tabla que incluya el nombre de despliegue del log y el período de retención. Los encabezados de columna deben ser NombreLog y Per-Retencion.

`` Get-EventLog -List | fl -Property @{n='nombreLog'; e={$_.Log}}, @{n='Per-Retencion';e={$_.minimumRetentionDays}}``

Resultado 

```
nombreLog     : Application
Per-Retencion : 0

nombreLog     : HardwareEvents
Per-Retencion : 0

nombreLog     : Internet Explorer
Per-Retencion : 7

nombreLog     : Key Management Service
Per-Retencion : 0

nombreLog     : OAlerts
Per-Retencion : 0

nombreLog     : Security
Per-Retencion : 

nombreLog     : System
Per-Retencion : 0

nombreLog     : Windows Azure
Per-Retencion : 7

nombreLog     : Windows PowerShell
Per-Retencion : 0

```

#4

Muestre una lista de servicios, de tal manera que aparezcan agrupados los servicios que están iniciados y los que están detenidos. Los que están iniciados deben aparecer primero.

`` Get-Service |Sort-Object status | fl -GroupBy status ``

Resultado

```
   Status: Stopped


Name                : AarSvc_282aaee
DisplayName         : Agent Activation Runtime_282aaee
Status              : Stopped
DependentServices   : {}
ServicesDependedOn  : {}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : False
ServiceType         : 224

Name                : QWAVE
DisplayName         : Experiencia de calidad de audio y vídeo de Windows (qWave)
Status              : Stopped
DependentServices   : {}
ServicesDependedOn  : {QWAVEdrv, rpcss, LLTDIO, psched}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : False
ServiceType         : Win32ShareProcess

Name                : RasAuto
DisplayName         : Administrador de conexiones automáticas de acceso remoto
Status              : Stopped
DependentServices   : {}
ServicesDependedOn  : {RasAcd}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : False
ServiceType         : Win32ShareProcess

...

```

#5 

Mostrar una lista a cuatro columnas de todos los directorios que están en el raíz de la unidad C:

``ls -Path C:\ -Attributes directory| fw -Column 4``

Resultado 

```

    Directorio: C:\



.Xilinx                                            dev                                                Intel                                             masm32                                           
OracleXE                                           PerfLogs                                           Program Files                                     Program Files (x86)                              
pspdata                                            Temp                                               Users                                             Windows                                          
xampp                                              Xilinx                                                                                                                                                


```

#6

Cree una lista formateada de todos los archivos .exe del directorio C:\Windows. Debe mostrarse el nombre, la información de versión, y el tamaño del archivo. La propiedad de tamaño se llama length en Powershell, pero para mayor claridad, la columna se debe llamar Tamaño en su listado.

`` ls -Path C:\Windows |where -filter {$_.Name -like "*.exe"} | fl -Property name, @{n='tamaño';e={$_.length}}, versionInfo ``

Resultado

```
Name        : bfsvc.exe
tamaño      : 73216
VersionInfo : File:             C:\Windows\bfsvc.exe
              InternalName:     bfsvc.exe
              OriginalFilename: bfsvc.exe.mui
              FileVersion:      10.0.18362.718 (WinBuild.160101.0800)
              FileDescription:  Utilidad de servicio de actualización del archivo de arranque
              Product:          Sistema operativo Microsoft® Windows®
              ProductVersion:   10.0.18362.718
              Debug:            False
              Patched:          False
              PreRelease:       False
              PrivateBuild:     False
              SpecialBuild:     False
              Language:         Español (España, internacional)
              

Name        : explorer.exe
tamaño      : 4622280
VersionInfo : File:             C:\Windows\explorer.exe
              InternalName:     explorer
              OriginalFilename: EXPLORER.EXE.MUI
              FileVersion:      10.0.18362.718 (WinBuild.160101.0800)
              FileDescription:  Explorador de Windows
              Product:          Sistema operativo Microsoft® Windows®
              ProductVersion:   10.0.18362.718
              Debug:            False
              Patched:          False
              PreRelease:       False
              PrivateBuild:     False
              SpecialBuild:     False
              Language:         Español (España, internacional)
```

#7

Importe el módulo NetAdapter (empleando el comando Import-Module NetAdapter). Empleando el cmdlet Get-NetAdapter, muestre una lista de adaptadores no virtuales (adaptadores cuya propiedad Virtual sea falsa. El valor lógico falso es representado por Powershell como $False).

``  Get-NetAdapter | Where -filter {$_.Virtual -eq $false} |fl ``

Resultado

```
Name                       : Wi-Fi
InterfaceDescription       : Intel(R) Dual Band Wireless-AC 7265
InterfaceIndex             : 16
MacAddress                 : DC-53-60-BE-4F-7E
MediaType                  : Native 802.11
PhysicalMediaType          : Native 802.11
InterfaceOperationalStatus : Up
AdminStatus                : Up
LinkSpeed(Mbps)            : 130
MediaConnectionState       : Connected
ConnectorPresent           : True
DriverInformation          : Driver Date 2019-02-12 Version 19.51.19.1 NDIS 6.60

Name                       : Ethernet
InterfaceDescription       : Realtek PCIe GBE Family Controller
InterfaceIndex             : 11
MacAddress                 : 2C-60-0C-F3-F9-BF
MediaType                  : 802.3
PhysicalMediaType          : 802.3
InterfaceOperationalStatus : Down
AdminStatus                : Up
LinkSpeed(Mbps)            : 0
MediaConnectionState       : Disconnected
ConnectorPresent           : True
DriverInformation          : Driver Date 2015-05-05 Version 10.1.505.2015 NDIS 6.40
```

#8 

Importe el módulo DnsClient. Empleando el cmdlet Get-DnsClientCache, muestre una lista de los registros A y AAAA que estén en el caché. Sugerencia: Si el caché está vacío, visite algunos sitios web para poblarlo.

``
Get-DnsClientCache | where -filter {$_.Type -eq (28 ) -or $_.Type -eq 1} |fl
``

Resultado 

```
Entry      : webcache.icesi.edu.co
RecordName : webcache.icesi.edu.co
RecordType : A
Status     : Success
Section    : Answer
TimeToLive : 27544
DataLength : 4
Data       : 200.3.192.46

Entry      : apps.corel.com
RecordName : 
RecordType : AAAA
Status     : NoRecords
Section    : 
TimeToLive : 
DataLength : 
Data       : 

Entry      : apps.corel.com
RecordName : apps.corel.com
RecordType : A
Status     : Success
Section    : Answer
TimeToLive : 534692
DataLength : 4
Data       : 0.0.0.0

...
```

#9
Genere una lista de todos los archivos .exe del directorio C:\Windows\System32 que tengan más de 5 MB.

``ls -Path C:\Windows\System32 | where -filter {$_.Name -like "*exe"} | WHERE -filter {$_.length/1MB -gt 5} |fl ``

Resultado

```
Name           : MRT-KB890830.exe
Length         : 133315992
CreationTime   : 09/06/2018 14:15:05
LastWriteTime  : 14/06/2018 13:37:25
LastAccessTime : 09/06/2018 14:15:05
Mode           : -a----
LinkType       : 
Target         : {}
VersionInfo    : File:             C:\Windows\System32\MRT-KB890830.exe
                 InternalName:     mrt.exe
                 OriginalFilename: mrt.exe
                 FileVersion:      5.61.14929.3
                 FileDescription:  Herramienta de eliminación de software malintencionado de Microsoft Windows
                 Product:          Herramienta de eliminación de software malintencionado de Microsoft Windows
                 ProductVersion:   5.61.14929.3
                 Debug:            False
                 Patched:          False
                 PreRelease:       False
                 PrivateBuild:     False
                 SpecialBuild:     False
                 Language:         Español (España, internacional)
				 
...

```

#10
Muestre una lista de parches que sean actualizaciones de seguridad.

``Get-HotFix | where -filter {$_.description -like "*security*"} |fl ``

Resultado

```
Description         : Security Update
FixComments         : 
HotFixID            : KB4515383
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 06/10/2019 0:00:00
Name                : 
ServicePackInEffect : 
Status              : 

...
```
#11
Muestre una lista de parches que hayan sido instalados por el usuario Administrador, que sean actualizaciones. Si no tiene ninguno, busque parches instalados por el usuario System. Note que algunos parches no tienen valor en el campo Installed By.

`` Get-HotFix | where -filter {$_.installedBy -like "*SYSTEM*"} |fl ``

Resultado

```

Description         : Update
FixComments         : 
HotFixID            : KB4534132
InstallDate         : 
InstalledBy         : NT AUTHORITY\SYSTEM
InstalledOn         : 14/02/2020 0:00:00
Name                : 
ServicePackInEffect : 
Status              : 

```
#12

Genere una lista de todos los procesos que estén corriendo con el nombre Conhost o Svchost.

`` Get-Process | where -filter {$_.Name -eq "Conhost" -or $_.Name -eq "Svchost"} | fl``

Resultado

```
Id      : 3480
Handles : 118
CPU     : 
SI      : 0
Name    : conhost

...

```
