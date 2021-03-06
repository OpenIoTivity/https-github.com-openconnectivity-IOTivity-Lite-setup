# IOTivity-lite on windows


Installation of IOTivity-Lite as indicated in Readme.md

Folder structure after everything is installed and code is generated:
    
    ~/iot-lite        
        |-- core             core resource definitions (in swagger) 
        |-- DeviceBuilder    The device builder tool chain
        |-- device_output    The output of device builder.
        |         |
        |         |-- code   The generated code.
        |               |    the files will be copied to folder iotivity/examples/OCFDeviceBuilder
        |               |- server.cpp
        |               |- server_security.dat         SVR data
        |               |- server_introspection.dat.h  introspection device data, encoded in header file
        |
        |-- iotivity-lite         IOTivity source code
        |        | 
        |        |-- apps
        |        |      |- simpleserver_windows.c            <--- generated code
        |        |      |- simpleserver_windows.c_org        <--- original application 
        |        |
        |        |-- include
        |        |      |- server_introspection.dat.h         <--- generated introspection data
        |        |
        |        |-- port/windows/vs2015
        |                          |- IoTivity-Constrained.vcxproj  <--- project file
        |                          |- IoTivity-Constrained.sln      <--- solution file
        |                          |- SimpleClient.vcxproj          <--- project file <not used>
        |                          |- SimpleClient.sln              <--- solution file <not used>
        |                          |- SimpleServer.vcxproj          <--- project file
        |                          |- SimpleServer.sln              <--- solution file
        |                   
        |-- IOTDataModels    oneIOTa resource definitions (in swagger format)
        |-- IOTivity-Lite-setup   This github repo.
        |-- swagger2x        swagger2x code generation
        |- gen.sh            generation command to convert the example.json in to code
        |- example.json      the input for device builder scripts.
            
            
     legenda:  folder
                  |-- folder
                  |-- folder/subfolder
                  |- file

        
        
The installDeviceBuilder script generates scripts in the folder above this repo.
These scripts are convienent scripts, e.g. they are short cuts for entering the generation command.
    
    
# development flow  

The development flow is depicted the figure below:

                   start
                     |       
                     v
               --------------                  
              |              |     
              | edit_input.sh|             --- edit the input file for the code generation
              |              |                 default file contains the binary switch resource
               -------------- 
                     |
                     |       
                     v
               --------------
              |              |
              |    gen.sh    |             ---  generates the code & introspection file
              |              |             --- script contains the device type, 
               --------------                  change the argument to change the device type.
                     |
                     | initial code        --- in iotivity-lite tree, to build
                     v                     --- introspection header files
               --------------                  
              |              |     
              |    visual    |<--------    --- edit/compile/run the generated code
              |    studio    |         
               --------------       
 
        Note: if gen.sh is run again, the generated code is overwritten.
        e.g. before running that tool again, safe the file in the iotivivty tree to another name 
        if one wants to keep that code as reference


# Initial Flow
Based on visual studio community 2017, version 15.7.1

The Initial flow is doing a generation (with the supplied example):
1. [gen.sh](#generate-code)
2. start up visual code/studio with the IOTivity-Constrained solution file (.sln)
   note dependend on the use version of studio/code solution conversion will take place.
3. retarget the solution, so that it actual builds
   tab -> Project -> Retarget solution
4. set the SimpleServer as default target
   solution explorer -> SimpleServer -> Set as StartUp Project
5. tab -> Build -> Build Solution
6. tab -> Debug -> Start Debugging
   

# visual studio
See microsoft to install visual studion on your windows machine at:

https://visualstudio.microsoft.com/vs/community/
