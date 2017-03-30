.. configure documentation master file, created by
   sphinx-quickstart on Mon Feb 20 18:25:17 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

流量策略
=====================================
ConnetOS支持如下的完善的流量策略，对用户流量进行管理。

 ==========  ====================================================================
 策略         主要功能
 ==========  ====================================================================
 QoS          Priority mapping（DSCP、IEEE 802.1p、Trust-port）
             
              Queue scheduling（SP、WDRR、SP+WDRR）
 
 Firewall     Filter（L2、L3、L4 fields）
 			  
 			  Forwarder（classifying、mirroring、policing、switching、routing）
 ==========  ====================================================================


.. toctree::
   :maxdepth: 2
   
   
   firewall_configuration
   qos_configuration

   
      
