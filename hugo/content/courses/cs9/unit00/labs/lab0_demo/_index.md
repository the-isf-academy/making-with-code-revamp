---
title: -1. Hugo Markdown Demo
type: lab
draft: true
resources:
- name: GitHub
  src: images/courses/cs9/unit00/00_git_github.png

---

# Set Up and Our First Turtle Program

In this lab, we are going to practice using the Terminal.

{{< expand "Setup" >}}

This is inside the accordion.
```shell
>>> 1+1
2
>>> 123456 + 654321
777777
>>> number = 5
>>> number * number
25
>>> "I am " + "a robot"
'I am a robot'
>>> exit()
~/Desktop/cs9$
```

```python
print("hi") # python
```
{{< /expand >}}

This is outside the accordion.


{{< devnote >}}
This is a devnote
{{< /devnote >}}

{{< checkpoint >}}{{< /checkpoint >}}

{{< checkpoint >}}
This is a custom checkpoint.
{{< /checkpoint >}}

{{< aside >}}
Notice how something different happened when you `cd`'d into the `cs9` directory? A piece of
software the install script installed called `direnv` just activated a virtual environment
for you Terminal session. Basically, it keeps the things you do or the software you install
for the class from affecting other parts of your computer.
{{< /aside >}}

{{< figure src="images/courses/cs9/unit00/00_git_github.png" width="400px" title="GitHub" >}}

{{< include_resource "resource_loops">}}

{{< ref_resource "resource_loops">}}

{{< ref_lab "lab4_functions">}}

{{< youtube id="https://www.youtube.com/embed/sTLi5unrY6I" autoplay="true" >}}
