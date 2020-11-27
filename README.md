# InsightCM-Console-in-LabVIEW
Running InsightCM Console commands from LabVIEW

# Introduction

The main goal of this project is to make it easier to run [InsightCM Console](https://www.ni.com/en-us/support/documentation/supplemental/17/using-the-insightcm-console-application.html) commands and automate a sequence of commands for the specific purpose of adding a new custom device to InsightCM. In addition to that, this project allows the user to export Data Sets as TDMS Files.


### State Machine FTW :heart:

I strongly believe that State Machine can solve a huge amount of the application needs and is sometimes underestimated when people start working with more complex architectures, such as QHM or even Actor Framework. I still believe we can stress out the features of our loved State Machine before jumping into more complex design patterns and frameworks (although it is important to have a good understanding of each one of them).

---

_I know the state machine is not a silver bullet. It is indeed underestimated, though._

---

If you are an enthusiast of State Machines, keep reading this article for a non-standard implementation of it and also check out the [JKI State Machine for LabVIEW by JKI](https://resources.jki.net/state-machine) which is another super powerful variation of this awesome LabVIEW Design Pattern. :smiley::thumbsup:

## The Project

### Project Goal :dart:

In this project, I wanted to help a customer by giving them a more easy-to-use interface to incorporate a new device into the InsightCM server. It is a very detailed and complex tasks, with a lot of steps to do files to export, import, edit, etc. In addition to that, the interaction with the server should be done by command line. My goal was to help them upload a base version of this device
and they will contract a developer to do the rest (i.e., they are not software developers and are not so proficient with those tricky steps). Try to lower their - and mine as a consequence - effort, I built a state machine that automates the more complicated parts.


## Design :notebook:

The diagram below represents the general structure of the State Machine.

![State Machine](/documentation/images/SM_GeneralStructure.png "General Structure of the State Machine")

In the diagram above, the steps in <span style=color:red>__red__</span> are the steps related with the command line interface. For each command we want to send, we have to build the command string, run the command using the System Exec.vi, and Processing the String response. The steps Build Command and Process Standard Output will not be actually implemented, but they represent the general task.

### States Overridden

The <span style=color:red>__Build Command__</span> will have different implementations as states in the code.

![Build Command Implementations](/documentation/images/BuildCommands.png "Commands that are built")

Same thing for the <span style=color:red>__Process Command Output__</span>.

![Process Standard Output](/documentation/images/Process%20Standard%20Output.png "Commands that are built")

The <span style=color:green>__Open File__</span> State is a state that will exclusive to open the TDMS file we pull from the server.


## Implementation :computer:

The implementation relied on the __LabVIEW State Machine Sample Project.__

![SM_SampleProject](/documentation/images/SM_SampleProject.png)

And this is how I structured the project files

![Project](/documentation/images/project.png)


### Running Multiple Commands in sequence

During the development I found the need for running more than one command in sequence before going back to wait for an event. For example, I wanted to Run the both __Import Definitions__ and __List Definitions__ in a row and transition back to __Wait for an Event__. Thinking on the standard State Machine, we can only decide the next state and not a sequence of states. To address that, I made use of the managing the Enum of states in an array of states.

![Array of States](/documentation/images/SM_StatesArray.png "Array of States")

When a user clicks the __Import Definition__ button, the Event Case will determine the next set of states to be executed.  

![Next States](/documentation/images/NextStates.png "Next States When user clicks Import definition")

The State Machine then starts to remove elements from the top of the list of states and the removed element is the state to be executed.

![Next State](/documentation/images/NextState.png)

---

__Note:__ If you want to ignore the following states, put another state at the top of the list, or put another state at any position of the list, you can do it by using the array manipulation functions. For this project, I just passed the array of states through the other states, that is, the Wait on Event is the only state who determines the next set of states.

### Conclusion :checkered_flag:

State machine is probably the first design patter you learn in LabVIEW, but sometimes we stick to this belief that it is just step sequencer and you cannot make it more flexible and scalable than the version of the LabVIEW sample project, but that is not true. Go ahead and open your mind to the possibilities with this simple, but powerful, LabIVEW Design Pattern. :wink:  

---

### Next Steps and Improvements

- [x] Make it more scalable. More projects could benefit of this Build -> Run -> Process structure.
- [ ] Improve Console output processing and Eror Handling

---

:e-mail: __Feel free to send me comments and improvement suggestions on [flores.felipegomes@gmail.com](mailto:flores.felipegomes@gmail.com)__

---
