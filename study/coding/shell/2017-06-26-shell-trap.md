# 1. trap 介绍
trap是一个shell内建命令，它用来在脚本中指定信号如何处理。trap命令用于指定在接收到信号后将要采取的动作，常见的用途是在脚本程序被中断时完成清理工作。当shell接收到sigspec指定的信号时，arg参数（命令）将会被读取，并被执行。例如：



## 1.1 语法

	trap [-lp] [[arg] sigspec ...]

## 1.2 例子

	trap "exit 1" HUP INT PIPE QUIT TERM 
表示当shell收到HUP INT PIPE QUIT TERM这几个命令时，当前执行的程序会读取参数“exit 1”，并将它作为命令执行。 

## 1.3 基本功能

    trap -p   // 把当前的trap设置打印出来
	 



# 2. 信号

信号是一种进程间通信机制，它给应用程序提供一种异步的软件中断，使应用程序有机会接受其他程序活终端发送的命令(即信号)。应用程序收到信号后，有三种处理方式：忽略，默认，或捕捉。进程收到一个信号后，会检查对该信号的处理机制。如果是SIG_IGN，就忽略该信号；如果是SIG_DFT，则会采用系统默认的处理动作，通常是终止进程或忽略该信号；如果给该信号指定了一个处理函数(捕捉)，则会中断当前进程正在执行的任务，转而去执行该信号的处理函数，返回后再继续执行被中断的任务。 在有些情况下，我们不希望自己的shell脚本在运行时刻被中断，比如说我们写得shell脚本设为某一用户的默认shell，使这一用户进入系统后只能作某一项工作，如数据库备份， 我们可不希望用户使用Ctrl c之类便进入到shell状态，做我们不希望做的事情。这便用到了信号处理。 

## 2.1 捕获信号

	$ trap commands signals

## 2.2 常用信号

	trap -l   //	把所有信号打印出来

以下是一些你可能会遇到的，要在程序中使用的更常见的信号：
 
SIGHUP	1	

本信号在用户终端连接(正常或非正常)结束时发出, 通常是在终端的控制进程结束时, 通知同一session内的各个作业, 这时它们与控制终端不再关联。 登录Linux时，系统会分配给登录用户一个终端(Session)。在这个终端运行的所有程序，包括前台进程组和后台进程组，一般都属于这个Session。当用户退出Linux登录时，前台进程组和后台有对终端输出的进程将会收到SIGHUP信号。这个信号的默认操作为终止进程，因此前台进程组和后台有终端输出的进程就会中止。对于与终端脱离关系的守护进程，这个信号用于通知它重新读取配置文件。 
	
SIGINT	2
程序终止(interrupt)信号, 在用户键入INTR字符(通常是Ctrl C)时发出。 

SIGQUIT	3
和SIGINT类似, 但由QUIT字符(通常是Ctrl /)来控制. 进程在因收到SIGQUIT退出时会产生core文件, 在这个意义上类似于一个程序错误信号。 

SIGFPE	8
在发生致命的算术运算错误时发出. 不仅包括浮点运算错误, 还包括溢出及除数为0等其它所有的算术的错误。 

SIGKILL	9	用来立即结束程序的运行. 本信号不能被阻塞, 处理和忽略。 

SIGALRM	14	时钟定时信号, 计算的是实际的时间或时钟时间. alarm函数使用该信号。 

SIGTERM	15	程序结束(terminate)信号, 与SIGKILL不同的是该信号可以被阻塞和处理. 通常用来要求程序自己正常退出. shell命令kill缺省产生这个信号。

## 2.3 型号设置与恢复

设置信号为空

	$ trap '' 2
	
恢复信号设置

	$ trap 2

# Reference
http://man.linuxde.net/trap
