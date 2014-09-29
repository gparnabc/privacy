steps to create css sprite using compass and image magic.
setting up the environment:
	1. install compass using ruby gem.
		please follow the steps provided in http://thesassway.com/beginner/getting-started-with-sass-and-compass
		alternatly it is install in PC242392(My Pc), please ues the system.

	2. create a compass project anywhere in d:\ using following command:
		compass create myProject
		one compass project will get created. inside it one *.rb file will be available. generally it is config.rb
		edit the file and change below mentioned params

			http_path = "/"
			css_dir = "stylesheets" ----> change it to --> css_dir = "css"
			sass_dir = "sass"
			images_dir = "images"	
			javascripts_dir = "javascripts" ----> change it to --> javascripts_dir = "js"

	3. put all dax css files in sass directory and change the file extension ".css" to ".scss", now if we run command "compass compile" inside myProject directory from commandline, compass will compile all scss files and create output css files in "css_dir"

	4.  create a directory "spriteimages" inside "images_dir" and place all thumbnail images inside it.

now our development encironment is ready for sprite implementation.
	1. for all scss files, at the top put tese lines
		@import "compass/utilities/sprites";
		@import "spriteimages/*.png";

	2. if we have an image say images/spriteimages/breadcrumb_arrow.png corresponding css rule in "templatefix.scss" is as below

	.aui .stoxx .stoxx-breadcrumbs li {
  margin-left: 0;
  padding-left: 27px;
  background: url("../images/stoxx/stoxxcom/breadcrumb_arrow.png") no-repeat scroll 10px 15px transparent; }

  for implementing the sprite, we need to change it as below

  	.aui .stoxx .stoxx-breadcrumbs li {
 		margin-left: 0;
 		padding-left: 27px;
	  	@include spriteimages-sprite(breadcrumb_arrow);
	  	background-repeat:no-repeat;
	  	background-color:transparent;
  }

@include spriteimages-sprite(breadcrumb_arrow); will create sprite position say "background-position: 0 -64px;", if we need to make the image right aligned, change it to "background-position: right -64px;"

if we need some adjustment like right padding(5px)/ top padding(3px) of the image, we need to edit image, change canvas size. this can be done using imagemagic from commandline.
ref:http://www.imagemagick.org/script/