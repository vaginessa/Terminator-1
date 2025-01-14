<p align= "center">
  <img src="https://img.shields.io/github/languages/top/Chainski/Terminator?style=flat&color=red">
   <img src="https://img.shields.io/github/stars/Chainski/Terminator?style=flat&color=red">
     <img src="https://img.shields.io/github/last-commit/chainski/terminator?color=red">
   <img src="https://img.shields.io/github/license/chainski/terminator?color=red">
    <img src="https://hits.sh/github.com/chainski/terminator.svg?label=views&color=red">
   <br>
</p>

<h1 align="center">Terminator</h1>

<p align="center">
<img src="https://github.com/Chainski/Terminator/assets/96607632/6deac6c5-9df1-4143-a8ab-9aecb811de34", width="200", height="200">
</p>

Terminator is a compact utility coded in C#, designed to end processes that have ```RtlSetProcessIsCritical``` enabled see [bsod.cs](https://github.com/Chainski/Terminator/blob/main/bsod.cs)

### Requirements
- An administrator account.
- Tested on ```Windows 10, version 22H2 (19045.4355) amd64```

### Usage
- Download the program from [releases](https://github.com/Chainski/Terminator/releases).
- Run ```Terminator.exe```

### Proof of Concept 👁

https://github.com/Chainski/Terminator/assets/96607632/135842a2-e5f8-41b4-abbc-72b6bec5fdbd

### How it Works ?
Terminator defines a method called ```UnProtectAndTerminate``` that aims to terminate a specified process after removing its protection. It utilizes platform invoke to call functions from system DLLs.
First, it imports functions from ```ntdll.dll``` and ```kernel32.dll``` using DllImport attribute. These functions are ```NtSetInformationProcess``` to alter process information and ```TerminateProcess``` to forcibly terminate a process.
Within the ```UnProtectAndTerminate``` method, it enters debug mode using ```Process.EnterDebugMode()```. Then it attempts to open the target process using ```OpenProcess```, passing necessary parameters including the process ID.
Afterward, it calls ```NtSetInformationProcess``` with appropriate arguments to remove the process protection. If successful, it terminates the process using ```TerminateProcess``` with an exit code of 0.
Terminator also provides feedback via console output, indicating success or failure in terminating the process.

### Why was this tool made ?

I developed this tool specifically designed to terminate processes containing the ```RtlSetProcessIsCritical``` feature, after encountering several malware samples utilizing this technique during my analysis. This tool proved invaluable for expediting dynamic analysis, enabling swift termination of potentially harmful processes. By swiftly neutralizing these processes, analysts can efficiently investigate malware behavior, identify malicious activities, and develop effective countermeasures. Such tools not only streamline the analysis process but also enhance cybersecurity efforts by empowering analysts to respond proactively to emerging threats.

### License
This project is licensed under the GNU License - see the [LICENSE](https://github.com/chainski/Terminator/blob/main/LICENSE) file for details
