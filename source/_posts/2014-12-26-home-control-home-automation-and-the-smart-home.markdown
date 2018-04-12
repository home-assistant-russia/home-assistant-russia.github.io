---
layout: post
title: "Home Control, Automation &amp; the Smart Home"
description: "Overview of how the internet of things relates to home control, home automation and the smart home."
date: 2014-12-26 10:23:13 -0800
date_formatted: December 26, 2014
author: Paulus Schoutsen
author_twitter: balloob
comments: true
categories: Internet-of-Things
---

The internet has been buzzing over the last year about home automation. A lot of different terms fly around like the internet of things, home automation and the smart home.
This article will try to explain how they all relate.

The first thing to introduce is the **Internet of Things** (IoT). This refers to a new generation of devices that cannot only be controlled by humans via buttons or remotes but also provide an interface to communicate with other devices and applications. For example, an IoT-capable coffee machine could receive commands to create different types of coffee and be able to broadcast the amount of water left in its reservoir.

There is no widely adopted open standard for smart device communication. This prevents a lot of devices to communicate with one another. And even if they could, most devices are not designed to manage other devices. To solve this we need a device to be able to communicate with and manage all these connected devices. This device is called a **hub**. 

As a bare minimum a hub has to keep track of the state of each device and should be able to control them if possible. For example, it has to know which lights are on or off and offer a way to control the lights. For a sensor it only has to know the value. A hub with these capabilities offers **home control**.

<p class='img'>
  <a href='{{site_root}}/images/screenshots/nexus_7_dashboard.png'>
    <img alt='Hub dashboard example'
         src='{{site_root}}/images/screenshots/nexus_7_dashboard.png' />
  </a>
  Example of a hub's dashboard. Showing the state of 2 persons, 4 lights and the sun.
</p>
<!--more-->
A step up from home control is to have the user setup triggers to send commands based on information in the home control layer. For example, to turn on the lights when a person arrives home. A hub with these capabilities is capable of **home automation**.

Most hubs on the market today offer this in various degrees of functionality and usability. Some IoT-capable devices offer this too, but only control themselves and are usually limited to location and time-based events.

The last category, and this is still very much in the future, is the **smart home**. A self-learning and adopting system that will decide which events should impact other devices.

An example of a smart home in action is that it observes that when person A comes home, the lights in the living room and the kitchen switch on. While if person B comes home, the lights in the living room and the study room are switched on. The next time person A or B comes home, the smart home will turn on its preferred lights without any configuration being set by the user.

A glimpse today at how the future can look is the [Nest thermostat](https://nest.com/). A thermostat smart enough to learn your schedule and adjust its own temperature accordingly.

All this results in the following overview of Home Automation.

<p class='img'>
  <a href='{{site_root}}/images/architecture/home_automation_landscape.png'>
    <img alt='Home Automation landscape'
         src='{{site_root}}/images/architecture/home_automation_landscape.png' />
  </a>
  Overview of the home automation landscape.
</p>

### Challenges

You are probably wondering, this all seems relatively simple, why don't I have my very own smart home yet? There are a couple of challenges today that keep us from stepping into the future.

#### More Internet of Things-capable devices

The majority of the IoT products out there are either lights, switches or presence detection. That's not enough for your home to be very smart about. We need televisions, fridges, ovens and more to join the party to increase the number of devices that we can control.

#### More data

Most first generation IoT devices are only exposing information that is needed for controlling it. We need to be able to track all interactions with each device for our smart home to learn how interaction with devices influence other things. For example, we need to be able to track how many cups of coffee were made or how often the fridge was open. This will increase the information flow and open up a whole bunch of new possibilities. For example, the smart home can order new coffee when you're running low.

#### Easy to use, open software that we can trust

To increase adoption we will need people to trust their smart home system. It will be very tough to convince people to upgrade all their devices and upload all interactions with each of them to the cloud. This data could reveal their whole life including all bad habits. That's why such a system should be simple and open-source so people can validate that their data generated at home stays home.

Anoter important booster for adoption is that the software should be easy to set up and use by the average user. A lot of people are not burning their hands yet on Home Automation because they are scared of configurating it.

Home Assistant is trying to be this software. It is not there yet but trying hard. Device discovery and a user interface for configuring home automation are problems we hope to tackle in 2015 while not sacrificing any modularity or usability.

Happy new year!
