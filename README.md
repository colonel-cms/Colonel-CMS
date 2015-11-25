![Colonel CMS](https://raw.githubusercontent.com/colonel-cms/Colonel-CMS/master/assets/colonel-logo%401000x325.png)

# Colonel

Colonel is proposed [Nest](https://github.com/nestproject/Nest) compatible Content Managment System written for Swift.

# Status

This is still just a proposal. Development starts when Swift is Open Sourced, which should be sometime this year.
The developement of this project also require some infrastructure to be in place.

1. A Package Manager
2. Templating Engines

# Mission

The mission of Colonel is to provide a CMS, written in a modern language, and with a better ground up design of both internal code and its interface than any other CMS.

Colonel CMS will also be extremly modular, where everything from the User system to the Authenticaion System to the Databse Provider is written more like an extension than anything else.

The idea is that, no matter how you want to setup your website, it should be possible.

Maybe you want to use a WordPress site to host your users(So you can have the same users on the Colonel site as the WordPress site), no problem, just switch out the User Provider module.

Maybe you want to run some custom hipser Database System that your company wrote, well, no problem. Just write a Database Provider.

Also, Nest compatible means that Colonel can be used with any web server.

## The WordPress action system

<blockquote>
If you are not familiar with wordpress, skip this section.
</blockquote>

Why am I bringing this up?, well, we should learn from mistakes.<br>
The WordPress `action` and `filter` system probably seemed like a good idea 
when it was written, and probably seems like a good idea if your just semi-familiar with WordPress. But it is simply a nightmare to work with in the long term.

Everything the WordPress `action` and `filter` system does can be done cleaner, better, more readable with good Object Oriented design.


# Components

There are 6 major types of components in Colonel

## Gateaway

The gateaway is implemented on a "per webserver" bases. There is, for example, and Apache gateaway. What the gataway does is, take the request from the web server, translate it, and sends the request to the kernel. Thats all.

The reason this exists is to prevent tight coupling. Colonel should be able to run on any web server, therefor, there is a seperate component that translates any type of request.

## Kernel

The kernel is the core of Colonel CMS, it just glues everything together and provides the very most basic functionality.

## Providers

Provider are modules required to be implemented. An example would be the User Provider. The User provider is invoked whenever a user related action is requested. A User Provider is as all provider, required to have an implementation, because it provides some functionality that needs to be present.

## Extension

Extensions are compiled together with the Kernel and Providers to make the Core. Extension are arbitrary code that can extend the functionality in both Providers and the Kernel.

An extension could, for example, override the function in the User Provider that gets users, and add some users from another system, to merge the two user systems.

## Themes

Theme are quote obvious. This is the component that displays the webpage.
Themes does not have access to change the core, but have access, through an interface, to add DataBase tables, theme settings etc.

## Widgets

Widgets are small pieces of content that can, by the user, be placed into a theme. A theme allows for a widget at a spesific location by defining a widget area.

Wigets can be things like; most resent posts, comment, plain text, etc.


# Writing a theme

<blockquote>
The <a>Theme Builder</a> is resposible for compiling the source code, and the <a>Theme Provider</a> is responsible for calling that code when approriate. Both of these are replaceable, therefor, the documentation below is only applicable for the standard Theme Builder and Theme Provder
</blockquote>

## Theme Builder

Themes in Colonel cms are compiled. They are compiled with a tool called the <a>Theme Builder</a>. The theme builder is a CLI tool that compiles your theme and makes sure to link the write header files etc.

## Project Structure

```
theme/
	controllers/   # Contains the controller for each page
	templates/     # Contains templates. The default template provider uses [Stensil](https://github.com/kylef/Stencil)
	lib/           # Contains any functionality besides theme
	theme.json     # Contains information about this theme, author, requirements, etc.
	settings.json  # Defined Theme Settings. Like `primary-color`, or somthing else
	publication-type-{name}.json # Defines a type of publication.
	widget-areas.json # Defines widgets area names
	model.json        # Optional, defines database tables for this theme?
```

<h6> settings.json </h6>
The settings.json file defined theme spesific settings

Example:

```js
[
	{
		"type"  : "text",
		"title" : "Title",
		"description" : "The title displayed on the main page",
		"name"  : "title",
		"require" : true,
		"min"   : 3,
		"max"   : 10,
	},
	{
		"type"  : "list",
		"name"  : "front-page-slider",
		"title" : "Front Page Slider",
		"min"   : 1,
		"description" : "Define the images in the front page slider",
		"elements" : [
			{
				"type" : "image",
				"name" : "image",
				"title": "Image",
				"min-width" : 800,
				"min-heigh" : 500,
				"ratio"     : 2
			}
		]
	}
]
```

The above is an example of a theme settings.json file.

## Writing a Provider

Providers are extension guaranteed to be there, because they are required for the kernel to work. Providers can theirfor safly be presumed to be avaiable in Extensions. Providers include DBProvider, User Provider, Theme Provider, Backend Provider etc. Read about all of these below.


The different providers are

## User Provider

Is called whenever there is a user related request. This provider may or may not use the DB Provider to handle these requests.

## DB Provider

Handles all database requests.

## Post Provider

Is called whenever there is a post related request. This provider may or may not use the DB Provider to handle these requests.

## Theme Provider

The theme provider handles all front end requests by calling the appropriate theme with the appropriate arguments.

## BackEnd Provider

This is basically the backend theme


## Writing an Extensions

Extensions(Which includes providers) and the Colonel Kernel are all compiled together to make up the Core.

Extensions are compiled together with the kernel to give them the power to change functionality in providers and kernels. Including override methods in providers/kernel, filter the output, etc. With this method there is just mroe flexebility.

This provider does everything from the moment that the kernel desides that the request was a "front end" request.
When that happens, the kernel invokes the Theme Provider, which handles calling the theme with the right parameters, to get the right output. And finally, the kernel will print that output so the Adapter gets it.

### Assets Provider

### Template Provider

# Config File

