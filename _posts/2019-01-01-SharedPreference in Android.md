---
layout: post
title:  "SharedPreference in Android"
date:   2019-01-01 05:00
by: "Honey Sharma"
categories: Android Technical
permalink: /archivers/test
---

**Shared Preference** in Android are used to save data based on key-value pair. If we go deep into understanding of word: shared means to distribute data within and preference means something important or preferable, so SharedPreferences data is shared and preferred data.

Shared Preference can be used to save primitive data type: string, long, int, float and Boolean.

# What is Preference File? #

A preference file is actually a xml file saved in internal memory of device. Every application have some data stored in memory in a directory data/data/application package name i.e android/data/me.honeysharma.example so whenever getSharedPreferences(String name,int mode) function get called it validates the file that if it exists or it doesn’t then a new xml is created with passed name.

# Two Ways To Save Data Through Shared Preference: #

There are two different ways to save data in Android through Shared Preferences – One is using Activity based preferences and other is creating custom preferences.


## Activity Preferences ##

* For activity preferences developer have to call function **getPreferences (int mode)** available in Activity class
* Use only when one preference file is needed in Activity
* It doesn’t require name as it will be the only preference file for this activity
* Developer doesn’t usually prefer using this even if they need only one preference file in Activity. They prefer using custom getSharedPreferences(String name,int mode).

To use activity preferences developer have to call function **getPreferences (int mode)** available in Activity class. The function getPreferences(int mode) call the other function used to create custom preferences i.e getSharedPreferences(String name,int mode). Just because Activity contains only one preference file so getPreferences(int mode) function simply pass the name of Activity class to create a preference file.

## Custom Preference ##

* Developer needs to use **getSharedPreferences(String name,int mode)** for custom preferences
* Used in cases when more than one preference file required in Activity
* Name of the preference file is passed in first parameter

Custom Preferences can be created by calling function **getSharedPreferences(String name,int mode)**, it can be called from anywhere in the application with reference of **Context**. Here name is any preferred name for example: User,Book etc. and mode is used to set kind of privacy for file.

# Mode And Its Type In Shared Preference: #

To create activity based preferences or custom preferences developer have to pass mode to let the system know about privacy of preference file.

**Before we begin a brief discussion on Context**

Context is an abstract class used to get global information in Android Application resources like strings, values, drawables, assets etc. Here modes are declared and static final constant in Context class.

**There are three types of Mode in Shared Preference:**

1. Context.MODE_PRIVATE – default value (Not accessible outside of your application)
2. Context.MODE_WORLD_READABLE – readable to other apps
3. Context.MODE_WORLD_WRITEABLE – read/write to other apps

**MODE_PRIVATE** – It is a default mode. MODE_PRIVATE means that when any preference file is created with private mode then it will not be accessible outside of your application. This is the most common mode which is used.

**MODE_WORLD_READABLE** – If developer creates a shared preference file using mode world readable then it can be read by anyone who knows it’s name, so any other outside application can easily read data of your app. This mode is very rarely used in App.

**MODE_WORLD_WRITEABLE** – It’s similar to mode world readable but with both kind of accesses i.e read and write. This mode is never used in App by Developer.

# Creating Shared Preference: #

As discussed above, to create shared preference developer needs to call **getPreferences(int mode)** or **getSharedPreferences(String name,int mode)** method. Both of the function return **SharedPreferences** object to deal with save and get values from preference file.

*SharedPreferences* is a singleton class means this class will only have a single object throughout the application lifecycle. However there can multiple preference files so all the preference files can be read and write using SharedPreferences class.

# Save Data In SharedPreferences #

1. To save data in SharedPreferences developer need to called **edit()** function of SharedPreferences class which returns **Editor** class object.

2. **Editor** class provide different function to save primitive time data. For example, Editor have all primitive data function including String type data as **putInt(String keyName,int value).**Common primitive function format is: **put + Primitive Type name (String keyname, Primitive Type value)**

3. Now make sure that key name should be unique for any values you save otherwise it will be overrided. To exactly save the values you put in different primitive functions you must call **commit()** function of Editor.

# Read or get data from SharedPreferences #

1. To read data first developer have to get reference of SharedPreferences object by calling **getPreferences (int mode)** or **getSharedPreferences (String name,int mode).**

2. Then developer can get values using SharedPreferences object by calling different primitive type function starting with get+Primitive Type name. Here every function has an additional parameter for every Primitive Type as default value in case there is no value found corresponding to passed key.

For example, to get saved int value just call **getInt(“GameScore”,-1)** function where “GameScore” is key and -1 is a default value in case no value was saved for GameScore.

# Remove Data Or Clear All Data #

Similar to save data there is a function **remove(String key)** in SharedPreferences. Editor to remove a particular key based data from preference file

To clear all data just call function **clear()** available in SharedPreferences.Editor. Make sure to call **commit()** method to save changes. So clear data will never delete the preference file but make it empty.

# Code Of Saving & Retrieving Data in Shared Preference: #

~~~java

public static final String PREFS_GAME ="com.abhiandroid.abhiapp.GamePlay";
public static final String GAME_SCORE= "GameScore";

//======== Code to save data ===================

SharedPreferences sp = getSharedPreferences(PREFS_GAME ,Context.MODE_PRIVATE);
sp.edit().putInt(GAME_SCORE,100).commit();

//========= Code to get saved/ retrieve data ==============

SharedPreferences sp = getSharedPreferences(PREFS_GAME ,Context.MODE_PRIVATE);
int sc  = sp.getInt(GAME_SCORE,0);
Log.d("AbhiAndroid","achieved score  is "+ sc);

~~~

# Importance #

During application development there are many situation where we need to store or save some data in a file. So rather than creating your own file and then managing it, Android provides mechanism to save data using SharedPreferences. To save some little amount of data SharedPreferences can be used like username and password of user, However if there is need to save large amount of data the always prefer to save data using **sqlite**.

