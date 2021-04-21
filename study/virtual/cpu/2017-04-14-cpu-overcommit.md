
## CPU过载使用 ##

关于 CPU的过载使用，最不推荐的做法是让某一个客户机的 vCPU 数量超过物理系统上存在的CPU数量。比如，在拥有4个逻辑CPU的宿主机中，同时运行一个或多个客户机，其中每个客户机的 vCPU 数量多于4个。推荐的做法是对多个单CPU的客户机使用 over-commit，比如，在拥有4个逻辑CPU的宿主机中，同事运行多于4个客户机。