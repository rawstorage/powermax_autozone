PowerMax and Brocade Autozone
=========

This role will provision storage on a PowerMax storage array, automatically 
selecting ports based on utilization, the role will also create zones and 
add to the active zoneset.  This role is provided as a sample and can be 
customized by modifying tasks/main.yml.  

All content (e.g. words, scripts) provided on this GitHub is for informational 
purposes only. I make no representations as to the accuracy or completeness of any information on this site or found by following any link on this site. I will not be liable for any errors or omissions in this information nor for the availability of this information. I will not be liable for any losses, injuries, or damages from the display or use of this information. The opinions expressed here are my personal opinions. Content published here is not read or approved in advance by Dell EMC and does not necessarily reflect the views and opinions of Dell EMC; nor does it constitute any official communication of Dell EMC. Always check official documentation hosted by either company for support or verified technical information.

Requirements
------------

dellemc.powermax collection v1.3 or higher

brocade.fos collection v1.2 or higher

Python modules PyU4V 9.2 or higher

Python module PyFOS



Role Variables
--------------

All required variables are defined in tasks/main.yml copy fill in the 
values as below to meet your environment or pass in by any means.

Unisphere connection Variables for PowerMax Management e.g.

    unispherehost: ""
    universion: "92"
    verifycert: False
    user: ""
    password: ""
    serial_no: ""

Required Front End Ports for Port Picker, this defaults to FA Ports for 
Fibre channel.  
    
    number_of_ports_required: 2

Brocade FOS credentials 
    
    brocade_credential:
      fos_ip_addr: ""
      fos_user_name: ""
      fos_password: ""
      https: False

    zone_cfg: """ - name of config on FOS array
    vfid: "" - virtual fabric id - if no virtual fabric set to -1

Storage Details Describing the host being created

    host_name: "Brocade_Test_host"
    initiators:
    sg_name: 
    srp: "SRP_1"
    mv_name: 
    portgroup_name: 
    service_level: "Diamond"

List of volumes to be created, role can be re-run with different values to 
add storage, volume name must be unique e.g.

    volume_list:
      - vol_name: "WLP_1"
        size: 1
        cap_unit: "GB"
      - vol_name: "WLP_2"
        size: 1
        cap_unit: "GB"


Dependencies
------------
Unisphere for PowerMax Version 9.2 or higher

PowerMax or VMAX Storage Array

Brocade FOS 9.0.0.a or higher



Example Playbook
----------------

    ---
    - name: Provision a host and storage on PowerMax
      hosts: localhost
      connection: local
      gather_facts: no
    
    
      tasks:
        - name: Create Cluster
          include_role:
            name: powermax_autozone


License
-------

BSD

Author Information
------------------

Paul Martin - Twitter @rawstorage 
https://rawstorage.wordpress.com
https://github.com/rawstorage

