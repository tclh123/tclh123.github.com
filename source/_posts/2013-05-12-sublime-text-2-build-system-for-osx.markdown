---
layout: post
title: "sublime text 2 build system for OSX"
date: 2013-05-12 23:15
comments: true
categories: sublime text 2
---

##Cpp

``` json
{
    "cmd": ["bash", "-c", "g++ '${file}' -o '${file_path}/${file_base_name}' && open '${file_path}/${file_base_name}'"],
    "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$",
    "working_dir": "${file_path}",
    "selector": "source.c, source.c++",

    "variants":
    [
        {
            "name": "Run",
            "cmd": ["bash", "-c", "g++ '${file}' -o '${file_path}/${file_base_name}' && '${file_path}/${file_base_name}'<'${file_path}/${file_base_name}.in'>'${file_path}/${file_base_name}.out'"]
        }
    ]
}
```

##Python
``` json
{
    "cmd": ["bash", "-c", "python -u '${file}' && chmod a+x '${file}' && open -a terminal '${file}'"],
    "selector": "source.python",

    "variants":
    [
        {
            "name": "Run",
            "cmd": ["bash", "-c", "python -u '${file}' && chmod a+x '${file}' && '${file}'<'${file_path}/${file_base_name}.in'>'${file_path}/${file_base_name}.out'"]
        }
    ]
}
```

##Java
``` json
{
    "cmd": ["bash", "-c", "javac '${file}' && java '${file_base_name}'"],
    "file_regex": "^(...*?):([0-9]*):?([0-9]*)",
    "selector": "source.java, source.java"
}
```

##Conclusion

For cpp & python, the build-system can open a new terminal window, so I can interact(ep. input) with my program easily.

For java, I don't know how to do that, only can show the outputs yet.

