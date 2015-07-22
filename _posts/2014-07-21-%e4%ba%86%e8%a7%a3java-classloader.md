---
layout: post
title: 了解JAVA classloader
date: 2014-07-21 11:58
author: VERYYOUNG
comments: true
categories: [Java]
---
（1）ClassLoader基本概念 　
与C或C++编写的程序不同，Java程序并不是一个可执行文件，而是由许多独立的类文件组成的，每一个文件对应一个Java类。此外，这些类文件并非全部装入内存，而是根据程序需要逐渐载入。ClassLoader是JVM实现的一部分，ClassLoader包括bootstrapclassloader（启动类加载器），ClassLoader在JVM运行的时候加载Java核心的API，以满足Java程序最基本的需求，其中就包括用户定义的ClassLoader，这里所谓的用户定义，是指通过Java程序实现的两个ClassLoader：一个是ExtClassLoader，它的作用是用来加载Java的扩展API，也就是/lib/ext中的类；第二个是AppClassLoader，它是用来加载用户机器上CLASSPATH设置目录中的Class的，通常在没有指定ClassLoader的情况下，程序员自定义的类就由该ClassLoader进行加载。 
（2）ClassLoader加载流程 　　当运行一个程序的时候，JVM启动，运行bootstrapclassloader，该ClassLoader加载Java核心API（ExtClassLoader和AppClassLoader也在此时被加载），然后调用ExtClassLoader加载扩展API，最后AppClassLoader加载CLASSPATH目录下定义的Class，这就是一个程序最基本的加载流程。 　　
下面来看一下ClassLoader中的一段代码： 　　
[java]
    protected synchronized ClassloadClass(Stringname, booleanresolve) throws ClassNotFoundException {
   //首先检查该name指定的class是否有被加载 　　
        Classc = findLoadedClass(name);
        if (c == null) {
            try {
                if (parent != null) { //如果parent不为null，则调用parent的loadClass进行加载 　
                    c = parent.loadClass(name, false);
                } else { //parent为null，则调用BootstrapClassLoader进行加载 　 
                    c = findBootstrapClass0(name);
                }
            } catch (ClassNotFoundExceptione) { //如果仍然无法加载成功，则调用自身的findClass进行加载 　
                
                c = findClass(name);
            }
        }
        if (resolve) {
            resolveClass(c);
        }
        returnc;
    }
[/java]　　

从上面一段代码中可以看出，一个类加载的过程使用了一种父类委托模式。为什么要使用这种父类委托模式呢？ 
　　第1个原因就是这样可以避免重复加载，当父类已经加载了该类的时候，就没有必要子ClassLoader再加载一次。 　　
    第2个原因就是考虑到安全因素，如果不使用这种委托模式，那么可以随时使用自定义的String来动态替代Java核心API中定义的类型，这样会存在非常大的安全隐患，而父类委托的方式就可以避免这种情况，因为String已经在启动时被加载，所以，用户自定义类是无法加载一个自定义的ClassLoader。 　　
（3）一些重要的方法 　
  　1）loadClass方法。 
　　ClassLoader.loadClass()是ClassLoader的入口点。
    该方法的定义如下：
    　　ClassloadClass(Stringname,booleanresolve); 
 　　name是指JVM需要的类的名称，如Foo或java.lang.Object。resolve参数告诉方法是否需要解析类。在准备执行类之前，应考虑类解析。注意：并不总是需要解析，如果JVM只需要知道该类是否存在或找出该类的超类，那么就不需要解析。 　
 　2）defineClass方法。 
　　defineClass方法接受由原始字节组成的数组，并把它转换成Class对象。原始数组包含如从文件系统或网络装入的数据。defineClass管理JVM的许多复杂的实现层面——它把字节码分析成运行时数据结构、校验有效性等。因为defineClass方法被标记成final的，所以也不能覆盖它。 　　3）findSystemClass方法。 　
　findSystemClass方法从本地文件系统装入文件。它在本地文件系统中寻找类文件，如果存在，就使用defineClass将原始字节转换成Class对象，以将该文件转换成类。当运行Java应用程序时，这是JVM正常装入类的默认机制。对于定制的ClassLoader，只有在尝试其他方法装入类之后，再使用findSystemClass。这是因为ClassLoader是负责执行装入类的相关步骤，不负责所有类的所有信息。例如，即使ClassLoader从远程的Web站点装入了某些类，仍然需要在本地机器上装入大量的基本Java库。而这些类库不是我们所关心的，所以要JVM以默认方式从本地文件系统装入它们，这就是findSystemClass的用途。 　　
4）resolveClass方法。 　　
 正如前面所提到的，可以不完全地（不带解析）装入类，也可以完全地（带解析）装入类。当编写我们自己的loadClass时，可以调用resolveClass，这取决于loadClass的resolve参数的值。 　
　5）findLoadedClass方法。 　　
findLoadedClass充当一个缓存：当请求loadClass装入类时，它调用该方法来查看ClassLoader是否已装入这个类，这样可以避免重新装入已存在类所造成的麻烦。 　
　6）findClass方法。 　　
loadClass默认实现调用这个新方法。findClass的用途包含ClassLoader的所有特殊代码，而无须复制其他代码（例如，当专门的方法失败时，调用系统ClassLoader）。
 　　目的是从本地文件系统使用实现的类装载器装载一个类。为了创建自己的类装载器，应该扩展ClassLoader类，这是一个抽象类。可以创建一个FileClassLoaderextendsClassLoader，然后覆盖ClassLoader中的findClass(Stringname)方法，这个方法通过类的名字得到一个Class对象。 　　
 [java]
  public Class findClass(Stringname) 　　{ 　
   　byte[]data=loadClassData(name); 　　
     returndefineClass(name,data,0,data.length); 　　
} 　

[/java]
　7）getSystemClassLoader方法。 　
　如果覆盖findClass或loadClass，getSystemClassLoader能以实际的ClassLoader对象来访问系统ClassLoader（而不是固定地从findSystemClass调用它）。为了将类请求委托给父类ClassLoader，这个新方法允许ClassLoader获取它的父类ClassLoader。当使用特殊方法，定制的ClassLoader不能找到类时，可以使用这种方法。 
　　父类ClassLoader被定义成创建该ClassLoader所包含代码的对象的ClassLoader。 　　
8）forName方法。 
　　Class类中有一个静态方法forName，这个方法和ClassLoader中的loadClass方法的目的一样，都是用来加载class的，但是两者在作用上却有所区别。 　
    [java]　Classclazz=Class.forName(&quot;&quot;something&quot;&quot;); 　　 [/java]　
      或者 　
 [java]
   ClassLoadercl = Thread.currentThread().getContextClassLoader(); 
　　Classclazz=cl.loadClass(&quot;&quot;something&quot;&quot;); 　
   [/java]
　Class.forName()调用Class.forName(name,initialize,loader)；
  也就是Class.forName(""something"")；
 等同于Class.forName(""something"",true,CALLCLASS.class.getClassLoader())； 　
　第二个参数“true”是用于设置加载类的时候是否连接该类，true就连接，否则就不连接。
  关于连接，在此解释一下，在JVM加载类的时候，需要经过三个步骤：装载、连接、初始化。装载就是找到相应的class文件，读入JVM；初始化就是class文件初始化。
  这里详述一下连接，连接分三步。 　　
  第一步是验证class是否符合规格。 　
　第二步是准备，就是为类变量分配内存的同时设置默认初始值。 　　
  第三步就是解释，而这步是可选的，根据上面loadClass方法的第二个参数来判定是否需要解释，这里的解释是指根据类中的符号引用查找相应的实体，再把符号引用替换成一个直接引用的过程。 　

　在JavaAPI文档中，loadClass方法的定义是protected，也就是说，该方法是被保护的，而用户使用的方法是一个参数，一个参数的loadClass方法实际上就是调用了两个参数，第二个参数默认为false。因此，在这里可以看出通过loadClass加载类实际上就是加载的时候并不对该类进行解释，因此不会初始化该类。而Class类的forName方法则相反，使用forName加载的时候就会将Class进行解释和初始化。 　　
