---
title: "C++"
layout: single
author_profile: true
excerpt: "I note book of C++"
header:
  overlay_color: "#333"
  overlay_image: ml2.jpg
---

# move and forwarding

[Microsoft tutorial on l-values](https://msdn.microsoft.com/en-us/library/f90831hc.aspx)

[A review on l-values in c++](http://thbecker.net/articles/rvalue_references/section_01.html)


* What does std::move do ?
* When and for whate would you use it for ?
* What is rvalue and lvalue references ?

* [Scott Meyers talk](https://www.youtube.com/watch?v=BezbcQIuCsY) on std::move and
std::forward

std::move is an **unconditional** cast to an rvalue.
std::forward is a **conditional** cost to an rvalue.

```cpp

template<typename T>
typename remove_reference<T>::type&&
move(T&& param)
{
  unsing ReturnType = typename remove_reference<T>::type&&;
  return static_cast<ReturnType>(param);
}

```
std::move simply takes the argument and cast's it to an rvalue. You can think
of it as cast_rvalue, it does not do any move but is done prior to implementing an
efficient move.

std::forward a conditional cast to an rvalue.
