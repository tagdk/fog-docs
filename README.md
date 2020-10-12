# fog-documentation

Documentation for FOG 1.X

This gets built by readthedocs via this readthedocs project [https://readthedocs.org/projects/fogproject/](https://readthedocs.org/projects/fogproject/)

The latest version will be available at [https://docs.fogproject.org/](https://docs.fogproject.org/)

See also for more discussion - [https://forums.fogproject.org/topic/14794/improve-documentation?_=1602258264683](https://forums.fogproject.org/topic/14794/improve-documentation?_=1602258264683)

The documentation is written in restructured text and built with sphinx

# Rst Styling rules for the project

## Headings

Below are examples of how to define the titles and headings and where they should be separated into new pages
Anything defined as a heading or title can be linked to from anywhere else with the following syntax

- If you want to reference a heading within the same section use this syntax

```:rst
`Heading Name`_
```

- if you want to cross-reference a section from a different page/section use this syntax. The below example links to the install instructions for CentOS/Rhel 7
  - See also [Cross-Referencing with Sphinx - Auto label sections](https://docs.readthedocs.io/en/stable/guides/cross-referencing-with-sphinx.html#automatically-label-sections)

```:rst
:ref:`installation/install_fog_server:CentOS 7 or RHEL 7`
```

### Title/heading 1

```:rst
==============
Title/Heading1
==============
```

Titles go with top level title pages that match the root folder structure.
i.e. we have a `Management` folder. The index.rst in that folder contains the title for that section of pages.
The index.rst file for each title should have the title and then `..include:: filename.rst` lines for each file included.

Each of these titles should also be referenced in the root index page.

So for every folder/section of the site there should be an index.rst page formatted like this to include all its child pages

```:rst
.. include:: /includes.rst

==================
Section/Page Title
==================

.. toctree::
   :maxdepth: 4

   index.rst

.. include:: every.rst
.. include:: child-page.rst
.. include:: in-the.rst
.. include:: folder.rst
.. include:: in-the-order.rst
.. include:: you-want.rst
.. include:: them.rst
.. include:: to-appear.rst

```

### SubTitle/Heading 2

```:rst
------------------
SubTitle/Heading 2
------------------
```

For every subtitle/heading 2 you should have a separte index.rst file.
These get included in the index.rst file so they all look like one big page.
This makes editing the pages and finding specific sections much easier.
This also helps to avoid merge conflicts as many will contribute to this documentation.

#### Heading 3

```:rst
Heading 3
=========
```

Heading 3 is where you break up your sub-section into scannable headings.
There are typically a good number of these in your single rst files as they make up the bulk of the layout once you're in a subsection.

#### Heading 4

```:rst
Heading 4
---------
```

These are for when you need another linkable level under a heading 3.

#### Heading 5

```:rst
Heading 5
#########
```

This level of heading is less common, but can be handy when outlining a list with sections that may need to be linked to.

#### Heading 6

```:rst
Heading 6
^^^^^^^^^
```

This heading level should rarely be used, but it is provided so that you have at least 4 levels to traverse through when writing out a section of documentation.

## Including images, css, videos, javascript, etc

At the top of every index.rst we have the line `.. include:: /includes.rst`
This is a file at the root of the project that includes all the indexes in the `_static` directory.
This makes it so you have access to all the shared images, roles (aka css classes), and videos via simple `|labelNames|`
Below is outlined how to create and or view these label names.

### Images

Images are stored and organized by relatable sections at `/_static/img`
For every image you add you should add substitution label for it in the `_static/img/index.rst`

These should look like this referencing the full path

```:rst
.. Comment saying what image folder the file is in (keep things alphabetical)

.. |AllHosts| Image:: /_static/img/management/All_Hosts.png
```

The label name and the image path are case sensitive.

### Roles/Css Classes

There is a single css file located at `/_static/css/custom.css` which allows us to add things like colored text.
It is included in the project build via the conf.py files by these lines

```:python
html_static_path = ['_static']
html_css_files = [
    'css/custom.css',
    'js/custom.js'
]
```

The static path defines the root folder name `_static` (which is the default/standard naming) and the second array defines the relative paths to css and js files. We don't currently have anything in the custom.js file, it's there as a place holder just in case we need it later.

#### Using css roles
  
in the `/_static/css/index.rst` file we can define roles like this

```:rst
`.. role:: red`
```

This role can be referenced inline in rst like this

```:rst
This field is :red:`required` for everyone
```

This would apply the css class `red` to the word 'required'
So we define something for the `red` class in the `custom.css` file like this

```:css
.red {
    color: red;
}
```

Thus resulting in red text for the word 'required'.

We have added classes/roles for red, yellow, and orange

#### Additional CSS Rules

We can also use additional css rules to override things in the built-in theme.
For example, we have this class defined

```:css
/* Override default theme max width of 800px so wide screens can view more content responsively */
.wy-nav-content {
    max-width: 1500px;
    width: auto;
}
```

Which, as the comment states, allows the body of the documentation text to expand more on wider screens.
Additional rules can be added at our leisure.

### Videos

Videos are hosted on our [FogProject youtube channel](https://www.youtube.com/channel/UCrvOQPcm1SDIfIrzWZ9K3bA/videos).
For every video in that channel we should add a substitution label in the video index.rst at `/_static/video/index.rst`
The format of the label is like this

```:rst
.. |videoName-vid| raw:: html

    <div style="text-align: center; margin-bottom: 2em;">
    <iframe width="100%" height="350" src="https://www.youtube-nocookie.com/embed/VIDEOID?rel=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
    </div>
```

Make sure to use the embed video link with the privacy-enhanced mode enabled.

It is also good practice to add the `-vid` to the label name so that we keep images and videos differentiated

# Additional Info

Below are resources for writing in rst and building locally

## Resources for writing in rst

These links are some good references for how to write in rst and how to configure and customize the readthedocs site

- [https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html](https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html)
- [https://www.ericholscher.com/blog/2016/jul/1/sphinx-and-rtd-for-writers/](https://www.ericholscher.com/blog/2016/jul/1/sphinx-and-rtd-for-writers/)
- [https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html](https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html)
- [https://docs.readthedocs.io/en/stable/guides/adding-custom-css.html?highlight=css](https://docs.readthedocs.io/en/stable/guides/adding-custom-css.html?highlight=css)
- [https://docs.readthedocs.io/en/stable/custom_domains.html?highlight=domain](https://docs.readthedocs.io/en/stable/custom_domains.html?highlight=domain)

## Building locally

see also [https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html](https://docs.readthedocs.io/en/stable/intro/getting-started-with-sphinx.html)

To test and build documemtation locally you need the following

- Python 3.7+ (can install from python.org, windows store, apt-get, yum, chocolatey, etc.)
- sphinx (`pip install sphinx`)
- sphinx_rtd_theme (`pip install sphinx_rtd_theme`)

Once you have those pre-reqs installed follow these steps

- Clone the repo
- Add additional .rst documentation following the existing structure
- run `make.ps1` from the root of the repo
  - This will create your `.\_build` directory and run `make html` with the project's settings
  - This is just a powershell version of the autogenerated make.bat file. It has some built-in error handling to help find the sphinx-build.exe if it isn't added to your path
- note: at some point the `make.ps1` may have added functionality such as auto-creating the _static index.rst's from the included files.

You will now have the files for the html site in you `_build` directory (the `_build` directory is excluded via .gitignore)
You can then open the `index.html` file from `.\_build\html` to browse the site locally.

You can edit in whatever you so desire, but if you're on windows it is reccomennded to use microsoft vscode with the [lextudio restructuredtext](https://marketplace.visualstudio.com/items?itemName=lextudio.restructuredtext) extension. This helps with easy rst snippets and a live view.
