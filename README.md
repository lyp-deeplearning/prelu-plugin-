# 基于Prelu层的插件添加方法
## 1、文件说明以及需要修改的地方
（1）修改deploy文件：  将所有的PRELU层修改为relu层

（2）修改Gplugin.cpp文件  ：第137、158/177行，将查找的层的名字修改成”relu" ，所有的自定义插件的类都继承于IPlugin类，这里的createPlugin类有两个创造的方法是因为一个是读原始caffemodel的时候修改层，一个是读序列化以后的数据去修改层

（3）最后在serialize的过程中我们只需要用到PluginFactory这个类，这个类在创建的时候会自动去建立两个插件的类，具体使用过程是见serialize.cpp

```
PluginFactory parserPluginFactory;
parser->setPluginFactory(pluginFactory);

```
在拿到engin文件进行inferenc的时候：

```
PluginFactory parserPluginFactory;
engine_Gender = runtime->deserializeCudaEngine((const void*)engine_data.get(), file_size, &parserPluginFactory);
```
======================================================================
https://blog.csdn.net/qq_35759574/article/details/88415101

出现的函数：
std::transform(strName.begin(),strName.end(),strName.begin(),::tolower);
把层的name全部转换成小写字母，然后利用这个小写字母去查找

×××C++里面的overide的用法，未完待续


 



