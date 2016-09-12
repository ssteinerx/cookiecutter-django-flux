# cookiecutter-django-mixin
Implementation of the cookiecutter-django mixin specification.

The idea for the `cookiecutter-django-mixin` project came about during the Django 1.10 update to the [cookiecutter-django](https://github.com/pydanny/cookiecutter-django) project.  We had a checklist of things that needed to support Django 1.10 before we could proceed and a couple of them were lagging and looked like they might not ever be updated.

During this time period there was also a proposed integration of [Webpack](https://webpack.github.io/), [React](https://facebook.github.io/react/), and various other heavy-weight and often unnecessary external packages.

As I disentangled the React/Webpack files from [cookiecutter-django][ccd], I noticed that the way it was done was actually quite nice.  Instead of being a modification to the core files of [cookiecutter-django][ccd], it was a completely separate repository that simply *added files to the directory structure* of [cookiecutter-django][ccd] itself.




from a natural evolution would  carry all the way through to being able to be updated after creation instead of being a one off generated boilerplate.  

For example, a _Docker Deploy_ mixin could reserve `project_dir/.docker` as its home, clone itself there, then be `mixed in` when the user wants to deploy the app while remaining completely independent of the main project, updatable separately, and only *mixed in* when its *role* is required.

A _React_ mixin could reserve `project_dir/.react`and could *mix in* the required JavaScript files via a Gulp/Grunt/Webpack/whatever task during e.g. `manage.py collectstatic`.

*Mixins* are *not* installed until they are *mixed in* to a runtime.  This means that they can be there, updated separately, until they're *mixed in* to a *runtime image*.  They are not static things, one-off'd into the app to grow increasingly staler, it's more like a `pip install` at deployment/run time.

The point is to make these *mixins* completely autonomous with an installed component that supports and enforces the *mixin's* contract with the rest of the system.

This leaves the *mixins* themselves being very loosely coupled to any particular directory layout etc., and only required to fulfill the contract in the specification which I have yet to write.

[ccd]: https://github.com/pydanny/cookiecutter-django "Cookiecutter Django"
