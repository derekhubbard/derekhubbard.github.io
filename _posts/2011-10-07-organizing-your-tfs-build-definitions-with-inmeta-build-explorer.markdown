---
layout: post
title: Organizing Your TFS Build Definitions with Inmeta Build Explorer
tags:
- Blog
- Team Foundation Server
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  _thumbnail_id: '214'
  _avia_elements_avia_options_propulsion: a:7:{s:4:"hero";s:0:"";s:6:"layout";s:0:"";s:17:"dynamic_templates";s:0:"";s:15:"_slideshow_type";s:11:"fade_slider";s:19:"_slideshow_position";s:5:"small";s:19:"_slideshow_autoplay";s:5:"false";s:19:"_slideshow_duration";s:1:"5";}
  _avia_elements_theme_compatibility_mode: a:7:{s:4:"hero";s:0:"";s:6:"layout";s:0:"";s:17:"dynamic_templates";s:0:"";s:15:"_slideshow_type";s:11:"fade_slider";s:19:"_slideshow_position";s:5:"small";s:19:"_slideshow_autoplay";s:5:"false";s:19:"_slideshow_duration";s:1:"5";}
---
The project I am currently working on is using Team Foundation Server for builds and we have a lot of build definitions.  The project is a large enterprise-level project, with multiple Visual Studio solutions.  Each Visual Studio solution has at least two branches – maybe more – and usually a corresponding build definition for most of those branches.  Hopefully that gives you a good idea of the number of build definitions.

One of my coworkers at this client was nice enough to point me towards the Inmeta Build Explorer add-in for Visual Studio.  The add-in plugs directly into the Team Explorer window in Visual Studio and provides you an organized hierarchical list of the build definitions in your team project.  This is done using a naming convention for the builds in your team project.  The add-in uses “.” as the default separator, but the developers of the add-in were nice enough to make it customizable.  And the Inmeta Build Explorer add-in is a client plugin, so only the developers on your team that are interested in using it have to install it – if you don’t look at the build definitions on a daily basis, then you don’t have to install it.

Just to give you an idea of the structure of the builds underneath the Inmeta Build Explorer node, here is what the Inmeta Build Explorer add-in looks like in our team project.
<p style="text-align: center;"><a href="/images/posts/Win7Dev-1-1-2.jpg"><img class="size-full wp-image-214 aligncenter" title="Win7Dev-1-1-2" src="/images/posts/Win7Dev-1-1-2.jpg" alt="" width="318" height="342" /></a></p>
&nbsp;

Another nice feature of this add-in is the ability to easily queue up the “default” build for a specific build definition.  If you right-click on one of the builds, an option named “Queue Default Build(s)” is available on the context menu.  Selecting this will automatically queue a new build for that build definition, bypassing the build properties window that lets you override the default build settings.

You can get the Inmeta Build Explorer on the Visual Studio Gallery.

<a title="http://visualstudiogallery.msdn.microsoft.com/35daa606-4917-43c4-98ab-38632d9dbd45" href="http://visualstudiogallery.msdn.microsoft.com/35daa606-4917-43c4-98ab-38632d9dbd45">http://visualstudiogallery.msdn.microsoft.com/35daa606-4917-43c4-98ab-38632d9dbd45</a>
