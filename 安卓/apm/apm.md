# 自己整理的有关apm的一些链接使用

## ANR相关

* [ANR 详解](https://xfhy666.blog.csdn.net/article/details/128113820?spm=1001.2014.3001.5502)

  产生的2种方式：1、Service、Broadcast、Provider 触发 ANR（watchDog 机制） 
               2、input 的超时检测机制  （处理后续上报事件的过程才会去检测是否该爆炸，所以更像是扫雷的过程）

  监控思路：1、不管是怎么发生的 ANR，最后都会走到 appNotResponding 
          2、当一个进程发生 ANR 时，则会收到 SIGQUIT 信号 （可能有误报，需要继续判断）
  