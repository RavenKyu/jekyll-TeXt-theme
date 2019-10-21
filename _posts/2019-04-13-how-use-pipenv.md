---
layout: article
title: Pipenv
aside:
  toc: true
tags: ["Python",]
mathjax: true
---

## Pipenv


## 트러블 슈팅
{% highlight bash linenos %}
Traceback (most recent call last):
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/pythonfinder/models/python.py", line 112, in get_versions
    version = PythonVersion.parse(p.name)
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/pythonfinder/models/python.py", line 359, in parse
    version_dict = parse_python_version(str(version))
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/pythonfinder/utils.py", line 86, in parse_python_version
    raise InvalidPythonVersion("%s is not a python version" % version_str)
pipenv.vendor.pythonfinder.exceptions.InvalidPythonVersion: rps-commons is not a python version

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/usr/local/bin/pipenv", line 10, in <module>
    sys.exit(cli())
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/click/core.py", line 764, in __call__
    return self.main(*args, **kwargs)
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/click/core.py", line 717, in main
    rv = self.invoke(ctx)
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/click/core.py", line 1137, in invoke
    return _process_result(sub_ctx.command.invoke(sub_ctx))
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/click/core.py", line 956, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/click/core.py", line 555, in invoke
    return callback(*args, **kwargs)
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/click/decorators.py", line 64, in new_func
    return ctx.invoke(f, obj, *args, **kwargs)
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/click/core.py", line 555, in invoke
    return callback(*args, **kwargs)
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/cli/command.py", line 390, in shell
    pypi_mirror=state.pypi_mirror,
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/core.py", line 2156, in do_shell
    three=three, python=python, validate=False, pypi_mirror=pypi_mirror,
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/core.py", line 609, in ensure_project
    validate=validate, skip_requirements=skip_requirements, system=system
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/core.py", line 320, in ensure_pipfile
    project.create_pipfile(python=python)
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/project.py", line 726, in create_pipfile
    required_python = self.which("python", self.virtualenv_location)
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/project.py", line 1083, in which
    result = next(iter(filter(None, (find(finder) for finder in self.finders))), None)
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/project.py", line 1083, in <genexpr>
    result = next(iter(filter(None, (find(finder) for finder in self.finders))), None)
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/pythonfinder/pythonfinder.py", line 67, in which
    return self.system_path.which(exe)
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/pythonfinder/pythonfinder.py", line 54, in system_path
    ignore_unsupported=self.ignore_unsupported,
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/pythonfinder/models/path.py", line 451, in create
    ignore_unsupported=ignore_unsupported,
  File "<attrs generated init 75e45f144e3d5510d54dd5fca6730b98fa0220a9>", line 38, in __init__
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/pythonfinder/models/path.py", line 116, in __attrs_post_init__
    self._setup_pyenv()
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/pythonfinder/models/path.py", line 196, in _setup_pyenv
    version_glob_path="versions/*", ignore_unsupported=self.ignore_unsupported
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/pythonfinder/models/python.py", line 156, in create
    sort_function=sort_function, version_glob_path=version_glob_path)
  File "<attrs generated init 024d8eb5bd88365dd041a88c977b58459ce5336d>", line 17, in __init__
  File "/Users/limdeokyu/Library/Python/3.7/lib/python/site-packages/pipenv/vendor/pythonfinder/models/python.py", line 114, in get_versions
    entry = next(iter(version_path.find_all_python_versions()), None)
AttributeError: 'NoneType' object has no attribute 'find_all_python_versions'

{% endhighlight %}

{% highlight bash linenos %}
$ pipenv install --python ~/.pyenv/versions/3.7.3/bin/python
Virtualenv already exists!
Removing existing virtualenv…
Creating a virtualenv for this project…
Pipfile: /Users/limdeokyu/Works/plugin/plugin-demo/Pipfile
Using /Users/limdeokyu/.pyenv/versions/3.7.3/bin/python (3.7.3) to create virtualenv…
⠇ Creating virtual environment...Using base prefix '/Users/limdeokyu/.pyenv/versions/3.7.3'
New python executable in /Users/limdeokyu/.local/share/virtualenvs/plugin-demo-sx0uwjx8/bin/python
Installing setuptools, pip, wheel...
done.
Running virtualenv with interpreter /Users/limdeokyu/.pyenv/versions/3.7.3/bin/python

✔ Successfully created virtual environment!
Virtualenv location: /Users/limdeokyu/.local/share/virtualenvs/plugin-demo-sx0uwjx8
Creating a Pipfile for this project…
Pipfile.lock not found, creating…
Locking [dev-packages] dependencies…
Locking [packages] dependencies…
Updated Pipfile.lock (a65489)!
Installing dependencies from Pipfile.lock (a65489)…
  🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 0/0 — 00:00:00
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
{% endhighlight %}

## 플랫폼 별 설치 패키지 설정 

패키지를 특정 환경에서만 설치하려고 한다면 `sys_platform`을 이용하여 해당 플랫폼 명시

```
[[source]]
url = "https://pypi.python.org/simple"
verify_ssl = true
name = "pypi"

[packages]
requests = "*"
pywinusb = {version = "*", sys_platform = "== 'win32'"}
```


### 다양한 플래그를 이용하여 패키지 설치 유무 결정

```
[[source]]
url = "https://pypi.python.org/simple"
verify_ssl = true

[packages]
unittest2 = {version = ">=1.0,<3.0", markers="python_version < '2.7.9' or (python_version >= '3.0' and python_version < '3.4')"}
```

## 실행 스크립트 작성
```
[scripts]
printspam = "python -c \"print('I am a silly example, no one would need to do this')\""
And then in your terminal:
```

```bash
$ pipenv run printspam
I am a silly example, no one would need to do this
```

인자(arguments)를 줄 수 있다.

```
[scripts]
echospam = "echo I am really a very silly example"
```

```bash
$ pipenv run echospam "indeed"
I am really a very silly example indeed
```

