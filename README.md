# OCMaR
Open for Collab Malware Research


<img src="/assets/main.png" width="100%" />

Included malware(s) database are only for educational purposes!

Feature:
1. Malware Type
2. Sample
3. Indication of Suspicious Actions
4. Payload/Dangerous Functions
5. Ways to immobilize


Explaination regarding releases:
- Malware(s) will be filled accordingly to the collaboration of the people that helps with reversing malware that are already available or that is coming.
- False-Positive(s) will be filled to show that the software is not actually dangerous and does not have any dangerous functions within it.

Guidance on what you need and how-to (Briefly)
- Setup VMWare/Sandbox on a device or an isolated device (if possible)
- Setup tools which you can get:
    - Static Analysis
        1. EXEInfoPE: Get From https://www.softpedia.com/get/Programming/Packers-Crypters-Protectors/ExEinfo-PE.shtml
        2. PEStudio: https://pestudio.en.lo4d.com/windows
        3. apktool / apkeditor : https://github.com/AbyssalArmy/SmsEye (APK Editor) and https://github.com/iBotPeaches/Apktool
    - Dynamic Analysis
        1. Procmon: https://www.bleepingcomputer.com/download/process-monitor-procmon/
        2. ProcDOT: https://cert.at/en/downloads/software/software-procdot
        3. Fakenet-ng: https://github.com/mandiant/flare-fakenet-ng
    - Dissassembly and Patching
        1. Ghidra: https://github.com/NationalSecurityAgency/ghidra
        2. X64dbg: https://x64dbg.com/
     

For Details, here is the explained guidance with pictures. Feel free to check them!
 
========================================================================================================================================================================================

->For those who are new, we will start with Sandbox or VMWare. Sandbox/VMWare needed to be used to prevent the malware from activating and running on the host (your main computer), therefore the activity and the length of what malware can do is or at least limited.<-

Full Guide
1. To install VMWare, you can go here https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html and download the file needed. Afterwards, follow the steps needed.

<img src="/assets/Screenshot_19.png" width="100%" />
<img src="/assets/Screenshot_1.png" width="100%" />
<img src="/assets/Screenshot_2.png" width="100%" />
<img src="/assets/Screenshot_3.png" width="100%" />

2. Prepare to install windows ISO File from here https://support.microsoft.com/id-id/windows/create-an-iso-file-for-windows-10-38547366-1dcb-7afd-1726-9eb222d72705.

<img src="/assets/Screenshot_5.png" width="100%" />

3. The windows ISO File can be downloaded by downloading a Media Creation Tool and Follow the steps to install it on USB/as a ISO File.

<img src="/assets/Screenshot_6.png" width="100%" />
<img src="/assets/Screenshot_7.png" width="100%" />
<img src="/assets/Screenshot_8.png" width="100%" />
<img src="/assets/Screenshot_9.png" width="100%" />
<img src="/assets/Screenshot_10.png" width="100%" />
<img src="/assets/Screenshot_11.png" width="100%" />


4. Create a new device in VMWare that you just downloaded. Select the ISO File and configure the system, then complete the windows setup.

<img src="/assets/Screenshot_4.png" width="100%" />
<img src="/assets/Screenshot_12.png" width="100%" />


5. Download Necessary Tools to analyze the malware such as:
    For Static Analysis: ExeinfoPE, PEStudio, APK Editor / apktool

   <img src="/assets/Screenshot_13.png" width="100%" />
      <img src="/assets/Screenshot_14.png" width="100%" />
      <img src="/assets/apktool.png" width="100%" />
    For Dynamic Analysis: Procmon, Procdot, Fakenet-ng

   <img src="/assets/Screenshot_15.png" width="100%" />
      <img src="/assets/Screenshot_16.png" width="100%" />
      <img src="/assets/Screenshot_17.png" width="100%" />
    For Reverse and Patching: Ghidra Disassembler, X64dbg / X32dbg
      <img src="/assets/Screenshot_18.png" width="100%" />
      <img src="/assets/Screenshot_21.png" width="100%" />


7. Ghidra Disassembler requires you to have Java 17 64-bit Runtime and Development Kit (JDK), there are few sources to install from:
    - Free LTS by Adoptium Temurin (https://adoptium.net/temurin/releases)
    - Free LTS by Amazon Coretto (https://docs.aws.amazon.com/corretto/latest/corretto-17-ug/downloads-list.html)
      <img src="/assets/Screenshot_20.png" width="100%" />


8. Procdot, you will need WinDump/TCPDump and Graphviz to be able to create a visualization of the processes. You can download from here:
    - WinDump : http://www.winpcap.org/windump/install/default.htm
    - Graphviz : http://www.graphviz.org/download_windows.php
   On the first run, Procdot will ask you to locate the WinDump and Graphviz executables files.
      <img src="/assets/Screenshot_22.png" width="100%" />
      <img src="/assets/Screenshot_23.png" width="100%" />


9. Step by step Instructions on How to Analyze (Windows Malware)
- Open up VMWare, and disconnect/the internet just to be cautios of the malware. While you do so, the windows defender should be turned off to prevent any interference from it.
      <img src="/assets/Screenshot_24.png" width="100%" />
      <img src="/assets/Screenshot_25.png" width="100%" />
    
    
- Static Analysis, drag and drop the executables that you want to analyze inside of Exeinfope and PEStudio to analyze it further.
        Exeinfope will give you an information if the malware is packed and the good part is, it also tells you how to unpack.
      <img src="/assets/Screenshot_26.png" width="100%" />
      <img src="/assets/Screenshot_27.png" width="100%" />
        PEStudio will tell you indications on what functions/api that will be used alongside the windows libraries file.
      <img src="/assets/Screenshot_28.png" width="100%" />
      <img src="/assets/Screenshot_29.png" width="100%" />
    
    
- Dynamic Analysis, before trying to run the malware it is recommended to start fakenet-ng incase the malware is trying to connect to an external network/IP.
      <img src="/assets/Screenshot_36.png" width="100%" />
        Procmon can be used to capture and log the activity of the malware.
      <img src="/assets/Screenshot_41.png" width="100%" />
      Filter can be applied also into the captured logs, those filter are ProcessCreate, WriteFile, SetDispositionInformationFile, TCP and UDP, & RegSetValue
       <img src="/assets/Screenshot_31.png" width="100%" />


ProcessCreate can show the malware is creating a new process when it is executed, while WriteFile and SetDispositionInformationFile is tracking what file or temporary files are created.
RegSetValue also keep tracks of the value of registry that are being set. TCP and UDP are to logs if the malware is requesting a request to external IP/Websites.
Afterwards, Procmon can create/export the logs using CSV so that Procdot can read them.
       <img src="/assets/Screenshot_32.png" width="100%" />


While using Procdot, you can use the CSV file that you got from Procmon and insert them. Pick the process of the malware that was running on the device and hit refresh to visualize the process.
       <img src="/assets/Screenshot_33.png" width="100%" />
       <img src="/assets/Screenshot_34.png" width="100%" />
       <img src="/assets/Screenshot_35.png" width="100%" />
    
    
- Disassembly and Patching: Ghidra, you can use it to analyze the executables. It will analyze the imports such as functions and necessary DLL file that are being used also being able to decompile some part of the malware is a nice thing to have.
      <img src="/assets/Screenshot_37.png" width="100%" />


- By doing decompile on the code, you can analyze what conditions does it have to run certain functions and/or finds out what is the killswitch. 
Finally, after you have got the killswitch and analyze the conditions you can import/open the executeables in X64dbg or X32dbg to patch that specific functions.
You can either change the value like changing from 1 to a 0 or going with the NOP on functions that are marked as suspicious/dangerous.
      <img src="/assets/Screenshot_38.png" width="100%" />
      <img src="/assets/Screenshot_39.png" width="100%" />
      <img src="/assets/Screenshot_40.png" width="100%" />



And that's all about it. Feel free to let me know if you have any different ways so I can add it into this guide/make a alternative guidance. Thanks !
