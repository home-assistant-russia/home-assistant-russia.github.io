---
layout: page
title: "Z-Wave Query Stage"
description: "What are the Query Stages."
date: 2017-09-21 11:49
sidebar: true
comments: false
sharing: true
footer: true
---

| Stage                  | Description                                                        |
|------------------------|--------------------------------------------------------------------|
| None                   | Query process hasn't started for this node                         |
| ProtocolInfo           | Retrieve protocol information                                      |
| Probe                  | Ping device to see if alive                                        |
| WakeUp                 | Start wake up process if a sleeping node                           |
| ManufacturerSpecific1  | Retrieve manufacturer name and product ids if ProtocolInfo lets us |
| NodeInfo               | Retrieve info about supported, controlled command classes          |
| NodePlusInfo           | Retrieve ZWave+ info and update device classes                     |
| SecurityReport         | Retrieve a list of Command Classes that require Security           |
| ManufacturerSpecific2  | Retrieve manufacturer name and product ids                         |
| Versions               | Retrieve version information                                       |
| Instances              | Retrieve information about multiple command class instances        |
| Static                 | Retrieve static information (doesn't change)                       |
| CacheLoad              | Ping a device upon restarting with cached config for the device    |
| Associations           | Retrieve information about associations                            |
| Neighbors              | Retrieve node neighbor list                                        |
| Session                | Retrieve session information (changes infrequently)                |
| Dynamic                | Retrieve dynamic information (changes frequently)                  |
| Configuration          | Retrieve configurable parameter information (only done on request) |
| Complete               | Query process is completed for this node                           |
