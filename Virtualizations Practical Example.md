k[[Virtualization]] is technology that lets you create useful IT services using resources that are traditionally bound to hardware. It allows you to use a physical machine’s full capacity by distributing its capabilities among many users or environments.


Imagine you have 3 physical servers with individual dedicated purposes. One is a mail server, another is a web server, and the last one runs internal legacy applications. Each server is being used at about 30% capacity—just a fraction of their running potential. 

![[server usage - without virutalization.png]]
Traditionally It was often easier and more reliable to run individual tasks on individual servers: 1 server, 1 operating system, 1 task. 

It wasn’t easy to give 1 server multiple brains. But with virtualization, you can split the mail server into 2 unique ones that can handle independent tasks so the legacy apps can be migrated. It’s the same hardware, you’re just using more of it more efficiently.

![[server usage - with virtualization.png]]

Keeping security in mind, you could split the first server again so it could handle another task—increasing its use from 30%, to 60%, to 90%. 

sOnce you do that, the now empty servers could be reused for other tasks or retired altogether to reduce cooling and maintenance costs.