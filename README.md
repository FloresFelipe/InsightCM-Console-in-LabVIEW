# InsightCM-Console-in-LabVIEW
Running InsightCM Console commands from LabVIEW

# Introduction

The main goal of this project is to make it easier to run InsightCM console commands and automate a sequence of commands for the specific purpose of adding a new custom device to InsightCM. In addition to that, this project allows the user to export Data Sets as TDMS Files.


# Same Old State Machine

I pretty much believe that State Machine can solve 80 percent of the application needs and is sometimes underestimated when people start working with more complex architectures, such as QHM or even Actor Framework. I still believe we can stress out the features of our loved State Machine before jumping into more complex design patterns and frameworks (although it is important to have a good knowledge on each one of them).

> I know the state machine is not a silver bullet. It is underestimated, though.

In this project, I wanted to help a customer by giving them a more easy-to-use interface to incorporate a new device into the InsightCM server. It is a very detailed and complex tasks, with a lot of steps to do files to export, import, edit, etc. In addition to that, the interaction with the server should be done by command line. My goal was to help them upload a base version of this device
and they will contract a developer to do the rest (i.e., they are not software developers and are not so ) I built a state machine 
