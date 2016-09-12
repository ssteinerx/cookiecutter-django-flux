# cookiecutter-django-mixin
Implementation of the cookiecutter-django mixin specification.

NOTE: This is a preliminary document -- I'm still thinking about/working out the details.

The idea for the `cookiecutter-django-mixin` project came about during the Django 1.10 update to the [cookiecutter-django][ccd] project.  

We had a checklist of things that needed to support Django 1.10 before we could proceed and a couple of them were lagging and looked like they might not ever be updated.

During this time period there was also a proposed integration of [Webpack](https://webpack.github.io/), [React](https://facebook.github.io/react/), and various other heavy-weight and often unneeded/wanted external packages.

As I disentangled the React/Webpack files from [cookiecutter-django][ccd], I noticed that the way it was done was actually quite nice.  Instead of being a modification to the core files of cookiecutter-django, it was a completely separate repository that simply *added files to the directory structure* of cookiecutter-django itself.  The way it was done did, in fact, add the contents of the separate repository to the main cookiecutter-django repository *but it didn't have to be that way!*

So, I thought to myself, "Self... why couldn't we formalize this methodology and create a mixin specification that allowed the addition of substantial external dependencies without making cookiecutter-django itself become bloated by including packages that not every user would need in their Django application?"

This will require some runtime support in cookiecutter-django (or maybe cookiecutter itself), but will not require it to contain any of the mixins in the base distribution.  You *mix in* what you need for your particular application.

For example, a _Docker Deploy_ mixin could reserve `project_dir/.mixins/docker` as its home, clone itself there, then be *mixed in* when the user wants to deploy or test the app while remaining completely independent of the main project, updatable separately, and only *mixed in* when its *role* is required.

A _React_ mixin could reserve `project_dir/.mixins/react`and could *mix in* the required JavaScript files via a Gulp/Grunt/Webpack/whatever task during e.g. `manage.py collectstatic`.

*Mixins* are *not* "installed" until they are *mixed in* to a runtime.  This means that they can be there, updated separately, until they're *mixed in* to a *runtime image*.  They are not static things, one-off'd into the app to grow increasingly staler, it's more like a `pip install` at deployment/run time.

The point is to make these *mixins* completely autonomous with an installed component that supports and enforces the *mixin's* contract with the rest of the system.

This leaves the *mixins* themselves being very loosely coupled to any particular directory layout etc., and only required to fulfill the contract in the specification which I have yet to write.

[ccd]: https://github.com/pydanny/cookiecutter-django "Cookiecutter Django"
