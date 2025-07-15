# JVM_Architecture
->after compiling the .java program all the classes in the file will be compiled to .class files(for each class in the .java a .class file is created when it is compiled) , this .class files are the input to the JVM
The JVM architecture can be broadly divided into three main subsystems:
1) Class Loader
2) Runtime Data Areas
3) Execution Engine

--------------Class Loader----------
-->When the JVM needs a class, it doesn't load it immediately; it loads it only when it's first referenced.
-->Three building blocks of class loader

1)Loading
2)Linking
3)Initializing class files

1)Loading:
-->The Classloader loads the .class file from the disk.
-->It reads the binary data of the .class file and generates a java.lang.Class object in the heap for each .class file
-->This Class object contains information like the fully qualified name of the class, its superclass, interfaces it implements, fields, methods, and constructors
-->There are three built in class loaders

i)Bootstrap ClassLoader:
--> It loads core Java API classes (e.g., java.lang.*, java.util.*) from the rt.jar (runtime JAR) file located in the <JAVA_HOME>/jre/lib directory. 

ii)Extension Classloader:
-->It loads classes from the extensions directory <JAVA_HOME>/jre/lib/ext. These are usually classes that extend the Java platform. Its parent is the Bootstrap Classloader
-->Any JAR files you manually placed there: If you wanted a specific JAR file (containing your own classes or a third-party library) to be automatically available to all Java applications running on that JRE, without explicitly adding it to the classpath for each application, you could place it in the ext directory. The Extension Classloader would automatically pick it up.
-->if we want sql connector jar file (before 8th version) we can use extention classloader(but version above 8) ,we should place sql jar file manually

iii)Application/System Classloader: 
-->This classloader loads classes from the application's classpath. This is the classloader that loads your own application classes. Its parent is the Extension Classloader

2)Linking:
-->Verification: This phase checks the correctness of the .class file. It ensures that the bytecode adheres to the JVM specification and doesn't pose any security threats (e.g., ensures proper stack manipulation, correct data types, valid opcodes). If verification fails, a java.lang.VerifyError is thrown.

-->Preparation: This phase allocates memory for static variables and initializes them to their default values (e.g., 0 for integers, null for objects, false for booleans). It does not execute any static initializers (like static { ... } blocks); that happens in the initialization phase.

-->Resolution: This is the process of replacing symbolic references from the type with direct references. For example, if your code refers to a method by its symbolic name, resolution finds the actual memory address of that method. This can be done lazily (at the first use) or eagerly (at the time of linking).

3)Initialization:
-->This is the final phase of class loading.
-->In this phase, all static variables are initialized with their actual values (as defined in the source code), and static blocks (static { ... }) are executed.
-->This happens only once for a class.



----------------Runtime Data Areas--------------
-->Gemini chat 
