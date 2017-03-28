.. configure documentation master file, created by
   sphinx-quickstart on Mon Feb 20 18:25:17 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

网络监控和诊断
=====================================
ConnetOS针对网络运维的常见问题，提供如下的功能：

 * 对转发平面所有数据包（转发的或丢弃的）进行监视和分析；
 * 实时捕获被设备丢弃的数据包，并记录丢包原因；
 * 根据五元组实时计算网络转发路径；
 * 具备端口拥塞感知和实时上报能力；
 * 高精度端口统计，最高精度1秒。


.. toctree::
   :maxdepth: 2
   
  
   
   port-mirror_configuration
   sflow_configuration
   sdrop_configuration
   navmesh_configuration

   
       