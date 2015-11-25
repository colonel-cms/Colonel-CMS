![Colonel CMS](https://raw.githubusercontent.com/colonel-cms/Colonel-CMS/master/assets/colonel-logo%401000x325.png)

# Colonel

Colonel is planned Content Managment System written for Swift.

# Status

This is still just a proposal. Development starts when Swift is Open Sourced, which should be sometime this year.
The developement of this project also require some infrastructure to be in place.

1. A Package Manager
2. Templating Engines

# Mission

Colonel cms will be as modular as possible, where everything from the User system to the Authenticaion System to the Databse Provider is written more like an extension than anything else.

The idea is that, no matter how you want to setup your website, it should be possible.

Maybe you want to use a WordPress site to host you users(So you can have the same users on the Colonel site as the WordPress site), no problem, just switch out the User provider module.

Maybe you want to run some custom hipser Database System that your company wrote, well, no problem. Just write a Database Provider and user that instead.

## The wordpress action system

<blockquote>
If you are not familiar with wordpress, skip this section.
</blockquote>
Why am I bringing this up?, well, we should learn from mistakes.<br>
The WordPress `action` and `filter` system probably seemed like a good idea 
when it was written, and probably seems like a good idea if your just semi-familiar with WordPress. But it is simply a nightmare to work with in the long term.

Everything the WordPress `action` and `filter` system does can be done cleaner, better, more readable with good Object Oriented design. 

# Basic Project Structure

# Modules

The most basic seperation is the Kernel, and everything else.<br>
The kernel is what "glues everything together". The modules does eveything else.<br>
This is still a work in progress, but the Modules so far are.


## User Provider

## DB Provider

## Post Provider

## Relationship Provider

# Config File

