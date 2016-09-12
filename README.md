# cookiecutter-django-mixin
Implementation of the cookiecutter-django mixin specification.

NOTES:

For example, a _Docker Deploy_ mixin could reserve `project_dir/.docker` as its home, clone itself there, then be `mixed in` when the user wants to deploy the app while remaining completely independent of the main project, updatable separately, and only *mixed in* when its *role* is required.

A _React_ mixin could reserve `project_dir/.react`and could *mix in* the required JavaScript files via a Gulp/Grunt/Webpack/whatever task during e.g. `manage.py collectstatic`.

*Mixins* are *not* installed until they are *mixed in* to a runtime.  This means that they can be there, updated separately, until they're *mixed in* to a *runtime image*.  They are not static things, one-off'd into the app to grow increasingly staler, it's more like a `pip install` at deployment/run time.

The point is to make these *mixins* completely autonomous with an installed component that supports and enforces the *mixin's* contract with the rest of the system.

This leaves the *mixins* themselves being very loosely coupled to any particular directory layout etc., and only required to fulfill the contract in the specification which I have yet to write.
