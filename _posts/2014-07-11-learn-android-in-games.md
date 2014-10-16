---
layout: post
title: "learn android by game"
date: 2014-07-11 19:00:00
categories: post
---
#Adb shell command for play
	
	1. getprop ro.sf.lcd_density //get lcd density
	2. dumpsys window | grep -i display	//get resolution
	3. input ...
       input text <string>
       input keyevent <key code number or name>
       input tap <x> <y>
       input swipe <x1> <y1> <x2> <y2>
    4. getprop //many kinds of properties
    
#Begin play
	input tap 1067 77
	input tap 676 586
	input tap 1060 51
	
	//get resource 1
	input swipe 1271 1 1 711
	input tap 600 400
	input tap 484 658
	input tap 400 557
	input tap 306 508
	input tap 212 456
	input tap 124 367
	
	
	//get resource 2
	input swipe 1 1 1271 711
	input tap 600 400
	input tap 883 663
	input tap 965 593
	input tap 1073 554
	input tap 1150 480
	input tap 1199 391
	
	
	//invade resist B level
	input swipe 1 1 1271 711
	input tap 481 418
	input tap 658 291
	input tap 808 581
	
	//