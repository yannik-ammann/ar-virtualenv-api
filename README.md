virtualenv-api - an API for virtualenv
======================================

[virtualenv](http://www.virtualenv.org/) is a tool to create isolated Python
environments.  Unfortunately, it does not expose a native Python API. This
package aims to provide an API in the form of a wrapper around virtualenv.

It can be used to create and delete environments and perform package management
inside the environment.

Examples
--------

* To begin managing an environment (it will be created if it does not exist):

```python
from virtualenvapi.manage import VirtualEnvironment
env = VirtualEnvironment('/path/to/environment/name')
```

* Check if the `mezzanine` package is installed:

```python
>>> env.is_installed('mezzanine')
False
```

* Check if a list of packages is installed (tuples with the syntax ('appname','3.1.version') are also valid inputs:

```python
>>> env.is_installed(['mezzanine',('django','1.4.16')])
False
```


* Install the latest version of the `mezzanine` package:

```python
>>> env.install('mezzanine')
```

* Install version 1.4 of the `django` package (this is pip's syntax):

```python
>>> env.install('django==1.4')
```

* Install a list of packages (tuples with the syntax ('appname','3.1.version') are also valid inputs:

```python
>>> env.install(['mezzanine','Pillow==2.2.1',('django','1.4.16')])
```

* Upgrade the `django` package to the latest version:

```python
>>> env.upgrade('django')
```

* Uninstall the `mezzanine` package:

```python
>>> env.uninstall('mezzanine')
```

* Uninstall a list of packages (tuples with the syntax ('appname','3.1.version') are also valid inputs:

```python
>>> env.uninstall(['mezzanine','Pillow==2.2.1',('django','1.4.16')])
```

* A package may be installed directly from a git repository (must end with `.git`):

```python
>>> env.install('git+git://github.com/sjkingo/cartridge-payments.git')
```

* Instances of the environment provide an `installed_packages` property:

```python
>>> env.installed_packages
[('django', '1.5'), ('wsgiref', '0.1.2')]
```

* A list of package names is also available in the same manner:

```python
>>> env.installed_package_names
['django', 'wsgiref']
```

* Search for a package on PyPI:

```python
>>> env.search('requests')[0]
('requests', 'Python HTTP for Humans.')
```

Verbose output from each command is available in the environment's `build.log`
file, which is appended to with each operation. Any errors are logged to `build.err`.


# Credits
virtualenv-api was initally developed by Sam Kingston, adopted and adapted by arteria GmbH. The current fork has backwards compatibility and comes with a lot of new features that builds the base for [virtualenv-mgr](https://github.com/arteria/virtualenv-mgr).
