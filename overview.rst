..
      Copyright 2015 Huawei Technologies Co. Ltd. All Rights Reserved.

      Licensed under the Apache License, Version 2.0 (the "License"); you may
      not use this file except in compliance with the License. You may obtain
      a copy of the License at

          http://www.apache.org/licenses/LICENSE-2.0

      Unless required by applicable law or agreed to in writing, software
      distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
      WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
      License for the specific language governing permissions and limitations
      under the License.

Overview
==============

**TerraCotta** is an extension to OpenStack implementing **dynamic consolidation** of instances using live migration. The major objective of dynamic instance consolidation is to improve the utilization of physical resources and reduce energy consumption by re-allocating instancess using live migration according to their real-time resource demand and switching idle hosts to the sleep mode.

For example, assume that two instances are placed on two different hosts, but the combined resource capacity required by the instances to serve the current load can be provided by just one of the hosts. Then, one of the VMs can be migrated to the host serving the other instance, and the idle host can be switched to a low power mode to save energy. When the resource demand of either of the instances increases, they get deconsolidated to avoid performance degradation. This process is dynamically managed by OpenStack Neat.

In general, the problem of dynamic instance consolidation can be split into 4 sub-problems:

      1. Deciding when a host is considered to be underloaded, so that all the instances should be migrated from it, and the host should be switched to a low power mode, such as the sleep mode.
      
      2. Deciding when a host is considered to be overloaded, so that some instances should be migrated from the host to other hosts to avoid performance degradation.

      3. Selecting instances to migrate from an overloaded host out of the full set of the VMs currently served by the host.

      4. Placing instances selected for migration to other active or re-activated hosts.
      
The aim of the OpenStack Terracotta project is to provide an extensible framework for dynamic consolidation of instances based on the OpenStack platform. The framework provides an infrastructure enabling the interaction of components implementing the 4 decision-making algorithms listed above. The framework allows configuration-driven switching of different implementations of the decision-making algorithms. 
