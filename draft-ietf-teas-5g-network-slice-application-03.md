---
stand_alone: true
category: info
submissionType: IETF
ipr: trust200902
lang: en

title: IETF Network Slice Application in 3GPP 5G End-to-End Network Slice
docname: draft-ietf-teas-5g-network-slice-application-03
date:

area: Routing Area
workgroup: TEAS Working Group

kw:
- Network Slice
- Architecture
- Mapping 3GPP

author:
 -
    fullname: Xuesong Geng
    organization: Huawei Technologies
    email: gengxuesong@huawei.com
    country: China
 -
    fullname: Luis M. Contreras
    organization: Telefonica
    role: editor
    email: luismiguel.contrerasmurillo@telefonica.com
    country: Spain
 -
    fullname: Reza Rokui
    organization: Ciena
    email: rrokui@ciena.com
    country: Canada
 -
    fullname: Jie Dong
    organization: Huawei Technologies
    email: jie.dong@huawei.com
    country: China
 -
    fullname: Ivan Bykov
    org: Ribbon Communications
    email: Ivan.Bykov@rbbn.com
    country: United States of America

contributor:
 -
    fullname: Jose Ordonez-Lucena
    organization: Telefonica
    email: joseantonio.ordonezlucena@telefonica.com
    street: Ronda de la Comunicacion, s/n Sur-3 building, 3rd floor
    city: Madrid, 28050
    country: Spain
 -
    fullname: Ran Pang
    organization: China Unicom
    email: pangran@chinaunicom.cn
 -
    fullname: Liuyan Han
    organization: China Mobile
    email: hanliuyan@chinamobile.com
 -
    fullname: Jaehwan Jin
    organization: LG U+
    email: daenamu1@lguplus.co.kr
 -
    fullname: Jeff Tantsura
    organization: Microsoft
    email: jefftant.ietf@gmail.com
 -
    fullname: Shunsuke Homma
    organization: NTT
    email: shunsuke.homma.ietf@gmail.com
    street: NTT 3-9-11, Midori-cho Musashino-shi,
    city: Tokyo 180-8585
    country: Japan
 -
    fullname: Xavier de Foy
    organization: InterDigital Inc.
    email: Xavier.Defoy@InterDigital.com
    country: Canada
 -
    fullname: Kiran Makhijani
    organization: Futurewei Networks
    email: kiranm@futurewei.com
    country: US
 -
    fullname: Hannu Flinck
    organization: Nokia
    email: hannu.flinck@nokia-bell-labs.com
    country: Finland
 -
    fullname: Rainer Schatzmayr
    organization: Deutsche Telekom
    email: rainer.schatzmayr@telekom.de
    country: Germany
 -
    fullname: Ali Tizghadam
    organization: TELUS Communications Inc
    email: ali.tizghadam@telus.com
    country: Canada
 -
    fullname: Christopher Janz
    organization: Huawei Canada
    email: christopher.janz@huawei.com
    country: Canada
 -
    fullname: Henry Yu
    organization: Huawei Canada
    email: henry.yu1@huawei.com
    country: Canada

informative:
   I-D.ietf-dmm-tn-aware-mobility:
   I-D.ietf-teas-5g-ns-ip-mpls:

   TS-23.501:
              title: "3GPP TS 23.501: System architecture for the 5G System (5GS)"
              date: 2022-03-25
              target: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3144
   TS-28.541:
              title: "3GPP TS-28.541 Management and orchestration; 5G Network Resource Model (NRM); Stage 2 and stage 3"
              date: 2019-06-07
              target: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3400
   TS-28.530:
              title: "3GPP TS 28.530 Management and orchestration; Concepts, use cases and requirements"
              date: 2022-03-25
              target: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3273
   TS-28.531:
              title: "3GPP TS 28.531 Management and orchestration; Provisioning"
              date: 2022-03-25
              target: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3274
   TS-28.540:
              title: "Management and orchestration; 5G Network Resource Model (NRM); Stage 1"
              date: 2017-12-31
              target: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3399
   TS-28.622:
              title: "Telecommunication management; Generic Network Resource Model (NRM) Integration Reference Point (IRP); Information Service (IS)"
              date: 2015-01-22
              target: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=1541
   TS-38.470:
              title: "NG-RAN; F1 general aspects and principles"
              date: 2022-03-25
              target: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3257
   TS-28.623:
              title: "Generic Network Resource Model (NRM); Integration Reference Point (IRP); Solution Set (SS) definitions"
              date: 2023-06-29
              target: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=1542
   GST:
              title: "GSMA Generic Network Slice Template"
              date: 2023-01-27
              target: https://www.gsma.com/newsroom/wp-content/uploads/NG.116-v8.0-1.pdf
   ZSM-003:
              title: "ETSI ZSM003 Zero-touch network and Service Management (ZSM); End-to-end management and orchestration of network slicing"
              date: 2021-06
              target: https://www.etsi.org/deliver/etsi_gs/ZSM/001_099/003/01.01.01_60/gs_ZSM003v010101p.pdf

--- abstract
Network Slicing is one of the core features of 5G defined in 3GPP, which provides different network service as independent logical
networks.  To provide 5G network slices services, an end-to-end network slice has to span three network segments: Radio Access
Network (RAN), Mobile Core Network (CN) and Transport Network (TN). This document describes the application of the IETF network slice
framework in providing 5G end-to-end network slices, including network slice mapping in the management, control and data planes.

--- middle

# Introduction

Driven by the new applications, 3GPP introduced the concept of network slicing as a feature of its 5G specification. Such a concept is meant to provide a customized connectivity service with specific capabilities and characteristics.  A network slice may include a set of network functions and resources(e.g. computation, storage and network resources). In the context of the IETF, the Network Slice Services are defined in {{!RFC9543}} as a set of connections between a number of Service Demarcation Points (SDPs e.g., CE, PE, or NF), where these connections having specific Service Level Objectives (SLOs) and Service Level Expectations (SLEs) over a common underlay network, with the traffic of one customer being separated from another.  The concept of IETF Network Slice Service is conceived as technology agnostic.

Network Slice Services as defined in {{!RFC9543}} are thus specified in terms of the set of SDPs connected to the slice, the type of connectivity among them, and a set of SLOs and SLEs for each connectivity construct.

In {{!I-D.ietf-teas-ietf-network-slice-nbi-yang}}, the endpoints are identified by an identifier, with some metrics associated to the connections among them as well as certain policies (e.g., rate limits for incoming and outgoing traffic).

The 5G network slice as defined by 3GPP in {{TS-23.501}} does not take the transport network slice into consideration.  3GPP introduces the concept of 5G end-to-end network slice service, which is built on top of three network segments: Radio Access Network (RAN), Transport
Network (TN) and Core Network (CN).  Transport network provides the required connectivity between RAN and CN or inside RAN/CN, with specific performance commitment.  The 5G end-to-end network slice services may have distinct topology and performance requirements on the underlying transport network.  The transport network should have thus capability to support multiple IETF network slices.  The decision about the number of such IETF network slices is deployment specific.

Editor Note - the following two paragraphs can come from different colliding versions, please, check and select one.

This document focuses on the mapping between 5G network slices and the network slices in underlying Transport Networks.  Specifically, the document describes how RFC9543 Network Slice Services can be derived in the context of a 3GPP Network Slice Service in management, control and data planes, including exploring how 3GPP Slice Service parameters are mapped to parameters that are exposed in IETF service data models.  It is out of scope of this document to elaborate on the realization of IETF Network Slices as per {{!RFC9543}}. The realizations of RFC9543 network slices are discussed in {{!I-D.ietf-teas-enhanced-vpn}} {{?I-D.ietf-teas-nrp-scalability}} {{?I-D.ietf-teas-ns-ip-mpls}}, and a realization model for network slicing in IP/MPLS networks for fuifilling 5G slicing connectivity services is discussed in [I-D.ietf-teas-5g-ns-ip-mpls].

# Terminology

## Requirements Language

{::boilerplate bcp14-tagged}

This document uses the terms defined in {{!RFC9543}}.

The following abbreviations are used in this document:

~~~
   NSC: IETF Network Slice Controller

   NSI: Network Slice Instance

   NSSI: Network Slice Subnet Instance

   S-NSSAI: Single Network Slice Selection Assistance Information

   RAN: Radio Access Network

   TN: Transport Network

   CN: Mobile Core Network

   DSCP: Differentiated Services Code Point

   CSMF: Communication Service Management Function

   NSMF: Network Slice Management Function

   NSSMF: Network Slice Subnet Management Function

   IOC: Information Object Class model, defined in 3GPP
~~~

In addition to that, the following terms from 3GPP are also used:

* EP_transport: 3GPP Information Object Class (IOC) defined in {{TS-28.541}} which, represents the logical transport interface of a RAN or CN and includes transport-related information with reference(s) to attachment circuit DM in IETF domain. 

* EP_RP: 3GPP IOC defined in {{TS-28.622}}, provided for sub-classing only. This IOC represents an end point of a link used across a reference point between two network entities. Inherited by EP_NgU, EP_F1U, EP_S1U, EP_X2U, etc. 


# 5G End-to-End Network Slice

The scope of a 5G End-to-End Network Slice service discussed in this document is shown in {{Figure1}}.  The transport networks (TN) provide the connectivity between and within RAN and CN.  To support automated enablement of 5G E2E network slices, multiple controllers are likely to manage 5G E2E network slices across RAN, CN and TN.  In addition, a 5G E2E network slice orchestrator is used to coordinate and control the overall creation and life cycle management of 5G E2E network slices across RAN, TN and CN.

~~~
    <-------------------- 5G E2E Network Slice ------------------->

        |-----------------------------------------------------|
        |           5G E2E Network Slice Orchestrator         |
        |-------|-------------------|-------------------|-----|
                |                  |                   |
                v                  v                   v
        |---------------|     |------------|    |--------------|
        |   RAN Slice   |     |    IETF    |    |   CN Slice   |
        |   Controller  |     |    NSC     |    |   Controller |
        |-------|-------|     |-----|------|    |------|-------|
                |                   |                  |
                v                   v                  v
     ............................        ..........................
     : RAN                      :        : CN                     :
     :                          :        :                        :
     : |-----|  |----|  |-----| : |----| : |----|  |----|  |----| :
     : | RAN |--| TN |--| RAN |---| TN |---| CN |--| TN |--| CN | :
     : | NFs |  |----|  | NFs | : |----| : | NFs|  |----|  | NFs| :
     : |-----|          |-----| :        : |----|          |----| :
     :                          :        :                        :
     :..........................:        :........................:
~~~
{: #Figure1 title="Scope of 5G End to End Network Slice"}

Depending on RAN deployment, a single 5G E2E network slice might have one or more IETF network slices.
Depends on the operator's networks, one or more of the following RAN deployments might be used. With different RAN deployments, the scope of TN slice may be different. These RAN deployments are discussed in the following sections:

   *  Distributed RAN

   *  Centralized RAN

   *  Cloud RAN (C-RAN)

## IETF Network Slices in Distributed RAN Deployment

Distributed RAN is the most common deployment of 3GPP RAN networks as shown in {{Figure2}}.  RAN is connected to CN using a transport network (TN1).

In this deployment a single 5G E2E network slice might have one or more IETF network slices between RAN and CN networks. In addition, one or more IETF network slices might be present inside the CN network to provide the connectivity between CN network functions (e.g., AMF, CMF and UPF).

~~~
   <-------------- 5G E2E Network Slice  ------------>
      <---- RS--->           <---------- CS --------->

                <- INS1 ->         <- INS2 ->
                (1 or more)       (1 or more)

   .............          .........................
   : RAN       :          : CN                    :
   :           : ........ :        .......        :
   :  |-----|  : :      : : |----| :     : |----| :
   :  | NFs |  : :  TN1 : : | NFs| : TN2 : | NFs| :
   :  |-----|  : :      : : |----| :     : |----| :
   :           : :......: :        :.....:        :
   :...........:          :.......................:
Legend
   INS: IETF Network Slice
   RS: RAN Slice
   CS: Core Slice
~~~
{: #Figure2 title="IETF network slices in distributed RAN deployment"}

##IETF Network Slices in Centralized RAN Deployment

In general, the RAN network consists of network functions for processing the radio signal and transmitting/receiving the radio signal. As shown in {{Figure3}}, in Centralized RAN deployment, two groups of network functions exit; NFs1 and NFs2 where NFs2 processes the carrier signal and is connected to the transport network and NFs1 transmit and receive the radio signal that is transmitted over the air from and to the end user equipment (UE). In Centralized RAN, network functions NFs1 and NFs2 are separated by a transport network TN3 called fronthaul network (FH). In this deployment a 5G E2E network slice contain of RAN and CN slices and one or more IETF network slices INS1, INS2 and INS3.  INS1 and INS2 are identical to the IETF network slices shown in {{Figure2}}. However, the IETF network slices INS3 needed across RAN network to provide the connectivity among NFs1 and NFs2.

~~~

        <-------------------- 5G E2E Network Slice  ------------------>
          <-------- RS --------->           <---------- CS --------->

               <- INS3 ->        <- INS1 ->         <- INS2 ->
              (1 or more)       (1 or more)        (1 or more)

        .........................          ...........................
        : RAN                   :          : CN                      :
        :        .......        : ........ :         .......         :
        : |----| :     : |----| : :      : : |-----| :     : |-----| :
        : |NFs1| : TN3 : |NFs2| : : TN1  : : | NFs | : TN2 : | NFs | :
        : |----| :(FH) : |----| : : (BH) : : |-----| :(BH) : |-----| :
        :        :.....:        : :......: :         :.....:         :
        :.......................:          :.........................:
     Legend
       INS: IETF Network Slice
       RS: RAN Slice
       CS: Core Slice
       FN: Fronthaul IETF network
       BH: Backhual IETF network
~~~
{: #Figure3 title="IETF network slices in centralized RAN deployment"}

##  IETF Network Slices in Cloud RAN deployment (C-RAN)

In a Cloud RAN deployment, the network function NF2 is further disaggregated into real-time and non-real-time components.  As shown
in {{Figure4}}, these disaggregated components are called CU (Central Unit) and DU (Distributed Unit) where they are connected by a new
network called Midhaul network (MH).

In this deployment 3GPP network slice contains not only RAN and Core slices but IETF network slices INS1, INS2, INS3 and INS4.  IETF
network slices INS1, INS2 and INS3 are similar to those in {{Figure3}}. An additional IETF network slice INS4 is used to connect the DUs to CUs through F1 interfaces.


~~~
     <---------------------- 5G E2E Network Slice  -------------------->
       <-------------- RS -------------->          <------- CS ------>

            <- INS3 ->      <- INS4 ->   <- INS1 ->     <- INS2 ->
            (1 or more)    (1 or more)  (1 or more)    (1 or more)

     ......................................        .....................
     : RAN                                :        :CN                 :
     :       .......       ......         : ...... :       .....       :
     : |----| :     : |---| :     : |---| : :    : : |---| :   : |---| :
     : |NFs1| : TN3 : |DU | : TN4 : |CU | : : TN1: : |NFs| :TN2: |NFs| :
     : |----| :(FH) : |---| : (MH): |---| : :(BH): : |---| :   : |---| :
     :        :.....:       :.....:       : :....: :       :...:       :
     :....................................:        :...................:
  Legend
    INS: IETF Network Slice
    RS: RAN Slice
    CS: Core Slice
    FN: Fronthaul IETF network
    MN: Midhaul IETF network
    BH: Backhual IETF network
    DU: Distributed Unit
    CU: Central Unit
~~~
{: #Figure4 title="IETF network slices in cloud RAN deployment (C-RAN)"}

For the sake of illustration, the following sections in this document all consider the TN slice between RAN and CN. Other IETF network slice cases are similar.


## Relationship Between IETF Network Slices and 3GPP Network Slices

Based on the Architecture of an IETF Network Slice and Interface of IETF Network Slice Management Architecture defined in {{!RFC9543}}, {{Figure6}} shows the relationship between 3GPP controllers and IETF Network Slice Controller.

~~~
       +---------------------+
       |         CSMF        |
       +----------|----------+
                  |                    +------------------------+
       +---------------------+         |  5G E2E Network Slice  |
       |         NSMF        |         |      Orchestrator      |
       +---------------------+         +------------------------+
             /    |    \                            |
            /     |     \           IETF Network Slice Service Interface
           /      |      \                          |
  +---------++---------++---------+    +------------------------+
  |    AN   ||    TN   ||   CN    |    |   IETF Network Slice   |
  |   NSSMF ||   NSSMF ||  NSSMF  |    |     Controller (NSC)   |
  |         ||         ||         |    +------------------------+
  +---------++---------++---------+   Network configuration interface
       |          |          |                      |
       |          |          |         +------------------------+
       |          |          |         |    Network Controllers |
       |          |          |         +------------------------+
       |          |          |                      |
       |          |          |                      |
   .?????.    .???????.    .???????.            .?????????.
  ?  5G   ?  ?  IETF   ?  ?   5G    ?          ?   IETF    ?
 (   RAN   )(  Network  )(   Core    )        (   Network   )
  `.     ,'  `.       ,'  `.       ,'          `.         ,'
    `???'      `?????'      `?????'              `???????'

~~~
{: #Figure5 title="Relationship between 3GPP domain controllers and IETF Network Slice Controller"}

An example of 5G E2E Network Slice is showed in {{Figure6}}.  Each E2E network slice contains RAN slice, CN slice and one or more IETF
network Slices. 3GPP identifies each E2E network slice using an integer called S-NSSAI.  In {{Figure6}} there are three instances of E2E
network slices which are identified by S-NSSAI 01111111, 02222222 and 03333333, respectively.  Each instance of E2E network slice contains
AN slice, CN Slice and one or more IETF network slices.  For example, E2E network slice 01111111 has AN Slice instance 4, CN Slice instance 1 and IETF network slice 6.  Note that 3GPP does not cover the IETF network slice.  Details of IETF network slice could be found in {{!RFC9543}}.

Note that 3GPP uses the terms NSI and NSSI which are a set of network function and required resources (e.g. compute, storage and networking resources) which corresponds to network slice Instance, whereas S-NSSAI is an integer that identifies the E2E network slice.

~~~
               +-----------+ +-----------+  +-----------+
               |  S-NSSAI  | |  S-NSSAI  |  |  S-NSSAI  |
               |  01111111 | |  02222222 |  |  03333333 |
               +---|-------+ +---|---|---+  +----|------+
                   |  +----------+   |           |
                   V  V              V           V
                **********    **********    **********
   Core         * NSSI 1 *    * NSSI 2 *    * NSSI 3 *
   Network      **********    **********    **********
                     \              \             /
                      \              \           /
                      +-----+       +-----+    +-----+
   Transport          | IETF|       | IETF|    | IETF|
   Network            | NS 6|       | NS 7|    | NS 8|
                      +-----+       +-----+    +-----+
                          \              \   /
                           \              \ /
     Radio                **********   **********
    Access                * NSSI 4 *   * NSSI 5 *
    Network               **********   **********
~~~
{: #Figure6 title="5G End-to-End Network Slice and its components"}



# 5G E2E Network Slice Mapping Procedure


## 5G E2E Network Slice Mapping Identifier

The following network slice related identifiers in management, control and data planes play an important role in the end-to-   end network slice mapping:

* Single Network Slice Selection Assistance Information (S-NSSAI): the end-to-end network slice identifier, which is defined in      {{TS-23.501}}; S-NSSAI is used during 3GPP network slice signaling process.

* Network Slice Service identifier : An identifier allocated by IETF Network Slice Controller (NSC) in the management plane.  See {{!I-D.ietf-teas-ietf-network-slice-nbi-yang}}.



## 5G E2E Network Slice Mapping Procedure

This section provides a general procedure of network slice mapping:

~~~
                  +-----------------+
                  |       NSMF      |
                  +-----------------+
       +----------|     S-NSSAI     |----------+
       |          |(e.g., 011111111)|          |
       |          +-----------------+          |
       |                   |                   |
       V                   V                   V
+-------------+ +---------------------+ +-------------+
|  RAN NSSMF  | |       IETF NSC      | |   CN NSSMF  |
+-------------+ +---------------------+ +-------------+
|   RAN Slice | | IETF Network Slice  | |   CN Slice  |
| Identifier  | |     Identifier      | |  Identifier |
| (e.g., 4)   | |     (e.g., 6)       | |  (e.g., 1)  |    Management
+-------------+ +---------------------+ +-------------+      Plane
     |           |                   |          |     -----------------
     |           |                   |          |
     V           V                   V          V     -----------------
  +-----+   +-----+             +-----+    +------+        Data
  | RAN |---|  PE |-----...-----| PE  |----|  CN  |        Plane
  +-----+   +-----+             +-----+    +------+
~~~
{: #Figure7 title="Relationship between IETF and 3GPP Network Slice Management"}

1. 3GPP NSMF receives the request from 3GPP CSMF for allocation of a network slice instance with certain characteristics.

2.  Based on the service requirement, 3GPP NSMF acquires requirements for the end-to-end network slice instance, which is defined in
Service Profile (section 6.3.3 of {{TS-28.541}}).

3.  Based on Service Profile, 3GPP NSMF determines the network function and the required resources in AN, CN and TN networks.  It
also assigns the unique S-NSSAI ID.

4. 3GPP NSMF sends a request to AN NSSMF for creation of AN Slice, which is out of the scope of this document.

5. 3GPP NSMF sends a request to CN NSSMF for creation of CN Slice, which is out of the scope of this document.

6. 3GPP NSMF sends a request to an IETF NSC (acting as an NSSMF for transport network, from the perspective of the 3GPP Management System)) for creation of a RFC9543 Network Slice service. The request contains attributes such as endpoints (based on the information from EP_Transport), required SLA along with other IETF network slice attributes. 

7. The IETF NSC realizes the IETF Network Slice which satisfies the requirements of the  {{!RFC9543}} Network Slice Service requested between the specified endpoints (RAN/CN edge nodes). The IETF NSC might assign an IETF Network Slice Service ID and send it to 3GPP NSMF.

8. The 3GPP NSMF could maintain the mapping relationship between S-NSSAI and IETF Network Slice Service ID.

#  5G E2E Network Slice Mapping in Management and Control Planes

The transport network management Plane maintains the interface between 3GPP NSMF and TN NSSMF. It is supposed to satisfy the following requirements:

1. Build up mapping relationship between NSI identifier and RFC9543 Network Slice Services;

2. Guarantee that IETF network slice could satisfy the SLA requirements with the transport network connection between AN and CN;

3. The requirements for 5G E2E network slice could be specified in IETF network slice northbound interface.

In order to provide slice connectivity constructed by means of IETF network slices it is necessary to build up mapping relationship between two different endpoints, as depicted in {{Figure8}}:

 * Mapping from EP_Transport of 3GPP network slice side (as defined by {{TS-28.541}}) to the CE endpoint from IETF network slice side (as defined in {{!RFC9543}}). IETF Network Slice Controller (NSC) will receive the set of CE endpoints to be interconnected as input for network slice services defined in {{!RFC9543}}.
    

 * Mapping from CE endpoints to PE endpoints. The endpoint at PE side should be elicited by the IETF NSC, in order to establish connectivity which could satisfy the customer request, according to the SLOs and SLEs received from the higher level system.

~~~
        3GPP concern

       EP_RP_left                                           EP_RP_right
          |                                                       |
        --|--------                                            ---|-----
          |      /                                            /   |
          x     /                                            /    x
               O EP_Transport_left       EP_Transport_right O
              /A                                           /A
             / |                                          / |
        -----  |                                         ---|-------
               |                                            |
               |                                            |
        .......|............................................|..........
               |                                            |
               |                                            |
               |                                            |
        -------|--       ----------            ----------   |  -------
               | /      /        /  ____      /        /    | /
               V/      /        /  (    )    /        /     V/
               O<---->O        0==(      )==0        O<---->O
              /      /        /    (____)  /        /      /
             /      /        /            /        /      /
        -----      ----------            ----------      ----------
        CE_left     PE_left               PE_right       CE_right

        IETF concern
~~~
{: #Figure8 title="conceptual view on 3GPP and TN end-points"}

The examples in Section 7 will show how the connection between network slice from endpoints at both 3GPP and IETF side can be established.

##  Mapping EP_transport to IETF NS CE Endpoints

The 3GPP Management system provides the EP_Transport Information Object Class (IOC) to extend slice awareness to the transport network. This IOC carries parameters that describe the transport endpoints associated with the 3GPP-managed functions (detailed in the EP_Application IOC). These parameters include:

- IP Address: The IP address of the transport endpoint.

- Additional Identifiers: Optional identifiers that further define the logical interface, such as VLAN tag, MPLS label, Segment Routing (SR) SID, etc.

- QoS Profile (Optional): A set of parameters specifying the Quality of Service (QoS) requirements for the slice.

The parameters from the EP_Transport IOC (representing the 3GPP domain) needs to be translated into the corresponding parameters for the CE within the IETF network slice. This translation process can be straightforward in certain scenarios. In such cases, the information from the EP_Transport IOC can be directly passed to the IETF Network Slice Subsystem (NSS) through the standardized Network Slice Services Interface defined in RFC9543. However, additional information might be required which have not been specified in 3GPP standards, e.g., subnet mask for the IP address). 

For example, when 3GPP-managed functions reside on dedicated monolithic network elements, the IP address in the EP_Transport IOC could directly map to the IP address of the corresponding interface.

The mapping process becomes more complex when dealing with virtualized 3GPP-managed functions. These functions can be instantiated on general-purpose servers or within data centers. In these scenarios, additional information are needed to identify the corresponding CE endpoint for example with other parameters defined in EP_transport, including:

* Combined Identification: The NS CE endpoint might be identified by a combination of the IP address and additional information like VLAN tag, MPLS label, or SR SID. This combination helps distinguish specific logical interfaces.

* Next Hop Information: The next hop router information, as viewed by the 3GPP entity within the slice, could provide hints for determining the slice endpoint at the other side of the slice boundary.

* QoS Profile: The QoS profile, if present, helps configure the PE endpoint to meet the Service Level Objectives (SLOs) for the connection between the CE slice endpoints.


##  Mapping IETF NS CE to PE Endpoints

As outlined in {{!RFC9543}}, an IETF Network Slice can have various potential endpoint positions, as reflected in {{Figure9}}. The information passed to the IETF Network Slice Controller (NSC) regarding endpoints is relative to the CE side, which is the perspective of the slice customer (i.e., the 3GPP Management System managing the 3GPP-managed functions). Based on this information, the IETF NSC needs to infer the corresponding endpoint on the Provider Edge (PE) side. This inference is crucial for establishing the desired connectivity constructs with the specified Service Level Objectives (SLOs) in the request.

Since the IETF slice request process is technology-agnostic, the identification of PE side endpoints should rely on generic information passed through the standardized Network Slice Services Interface {{!I-D.ietf-teas-ietf-network-slice-nbi-yang}}. This generic information, combined with the knowledge of the network topology and available resources, will allow the IETF NSC to determine the appropriate PE endpoint for each CE endpoint, ensuring a successful network slice instantiation.


~~~
              |<---------------------- (1) ---------------------->|
              |                                                   |
              | |<-------------------- (2) -------------------->| |
              | |                                               | |
              | |        |<----------- (3) ----------->|        | |
              | |        |                             |        | |
              | |        |  |<-------- (4) -------->|  |        | |
              | |        |  |                       |  |        | |
              V V   AC   V  V                       V  V   AC   V V
          +-----+   |    +-----+                 +-----+    |   +-----+
          |     |--------|     |                 |     |--------|     |
          | CE1 |   |    | PE1 |. . . . . . . . .| PE2 |    |   | CE2 |
          |     |--------|     |                 |     |--------|     |
          +-----+   |    +-----+                 +-----+    |   +-----+
             ^              ^                       ^              ^
             |              |                       |              |
             |              |                       |              |
          Customer       Provider                Provider       Customer
          Edge 1         Edge 1                  Edge 2         Edge 2
	
	(1) SDPs within the CE (e.g. buffers or queues on the outgoing interfaces)
	(2) SDPs at the Attachment Circuit
	(3) SDPs at the customer-facing ports on the PEs
	(4) SDPs within the PE (e.g. destination IP addresses, port numbers)

~~~
{: #Figure9 title="IETF Service Demarcation Points"}





{::comment}


##  5G E2E Network Slice Mapping in Control Plane

The S-NSSAI defined in {{TS-23.501}} is treated
as the end-to-end network slice identifier in the control plane of AN
and CN, which is used in UE registration and PDU session setup. It is assumed that there is a correspondence between
S-NSSAI and the IETF Network Slice service identifier in the
management plane. But there is no explicit interaction between transport network and AN/CN
in the 3GPP control plane signalling.

On the other hand, between the adjacent transport node and RAN/CN nodes, control plane interaction (such as routing information exchange) for building the connectivity between the endpoints in 5G network slices may be needed. 

ToDo: there is no direct relationship between 3GPP control plane signalling and IETF control plane.
Add sentence on this respect to provide some description here (Xuesong).

Note: to ensure consistency with NBI YANG model (i.e., service tag)

Jie's note: modified/added some text about the control plane interaction.

#  5G E2E Network Slice Mapping in Data Plane

If multiple 5G E2E network slices data flows are carried from one physical interface
between AN/CN and TN, there should be a mechanism for provider edge (PE) nodes to distinguish between these flows in order to apply and to enforce the different SLO/SLE policy to each flow. In other words, a solution needed in order to define an IETF Network Slice Interworking in the data plane.

If different network slices are
transported through different physical interfaces, 5G E2E network slices
could be distinguished by the interface directly.  However if all flows from different 5G network slice flows are transported through same interface, the PE nodes needs to be able to distingush each flows.




## Data Plane Mapping Considerations

The following picture shows the end-to-end network slice in data
plane?taking the IETF network slice between RAN and UPF as an example:

   The mapping relationship between AN or CN network slice and an IETF
   Network Slice will be based on a IETF Network Slice Interworking
   identifier based on the information provided by the EP_Transport IOC.
   When the packet of an uplink flow goes from AN to TN, the packet is
   delivered according to the information provided by the EP_Transport
   IOC (e.g., the information provided in the logicalInterface field);
   then the encapsulation is read by the edge node of transport network,
   which maps the packet to the corresponding IETF network slice.

~~~
   <-----AN NS----> <----------TN NS-----------> <---- CN NS----->

   +--+       +-----+                           +----------------+
   |UE|- - - -|(R)AN|---------------------------|       UPF      |
   +--+       +-----+                           +----------------+
~~~
{: #Figure10 title="The mapping between 3GPP slice and transport slice"}

The mapping between 3GPP slice and transport slice in user plane
could happens in:
(R)AN: User data goes from (radio) access network to transport
network

UPF: User data goes from core network functions to transport network

The following picture shows the user plane protocol stack in end-to-
end 5G system.

~~~
  +-----------+                    |                  |               |
  |Application+--------------------|------------------|---------------|
  +-----------+                    |                  | +-----------+ |
  | PDU Layer +--------------------|------------------|-| PDU Layer | |
  +-----------+   +-------------+  |  +-------------+ | +-----------+ |
  |           |   | ___Relay___ |--|--| ___Relay___ |-|-|           | |
  |           |   |     \/ GTP-U|--|--|GTP-U\/ GTP-U|-|-|   GTP-U   | |
  |   5G-AN   |   |5G-AN +------+  |  +------+------+ | +-----------+ |
  |  Protocol |   |Protoc|UDP/IP|--|--|UDP/IP|UDP/IP|-|-|   UDP/IP  | |
  |   Layers  |   |Layers+------+  |  +------+------+ | +-----------+ |
  |           |   |      |  L2  |--|--|  L2  |  L2  |-|-|     L2    | |
  |           |   |      +------+  |  +------+------+ | +-----------+ |
  |           |   |      |  L1  |--|--|  L1  |  L1  |-|-|     L1    | |
  +-----------+   +-------------+  |  +-------------+ | +-----------+ |
       UE               RAN        |        UPF       |      UPF      |
                                   N3                 N9              N6
~~~
{: #Figure11 title="Packet encapsulation in UE/RAN/UPF"}

The following figure shows the typical encapsulation in N3 interface.

~~~
   +------------------------+
   | Application Protocols  |
   +------------------------+
   |       IP (User)        |
   +------------------------+
   |          GTP           |
   +------------------------+
   |          UDP           |
   +------------------------+
   |          IP            |
   +------------------------+
   |       Ethernet         |
   +------------------------+
~~~
{: #Figure12 title="Typical packet encapsulation in N3 interface "}


There are several options in the encapsulation that could be used in
data plane of network slice mapping.

{:/comment}

# Methods for Mapping Between 3GPP E2E Network Slice and IETF Network Slice

Referring to {{Figure2}}, {{Figure3}} and {{Figure4}}, an end-to-end network slice might have one or more IETF network slices. {{Figure13}} is a general representation of any of transport networks in 5G end-to-end network slice where the IETF network slice INS_a provides the connectivity between network functions NF1 and NF2 to satisfy the specific SLO/ SLE.  For example, {{Figure13}} could represent IETF network slice INS1 of {{Figure4}} where connectivity needed between network functions CU and UPF or it could represent IETF network slice INS4 between network functions DU and CU.

Suppose the network function NF1 sends the traffic to NF2.  The data plane mapping is mainly addresses how the identification of 3GPP network slice is conveyed and represented on data path, and how the provider network PE nodes map the traffic from context of 5G end-to-end network slice to the {{!RFC9543}} network slice services. It is crucial for PE nodes to be able to map the traffic to the appropriate IETF network slice so as to enforce the SLO/SLE policy.

~~~
          <------ IETF Network Slice Service INS_a ------>

                 AC         .-------.           AC
                 |        ,'         `.         |
                 |      ,'             `.       |
      --------   V   -------          -------   V   --------
      |      |       |     |          |     |       |      |
      | NF1  |-------| PE1 |          | PE2 |-------| NF2  |
      |      |-------|     |          |     |       |      |
      --------       ------- Provider -------       --------
                         `.  Network  ,'
                           `.       ,'
                             -------

~~~
{: #Figure13 title="Typical IETF Network Slice in 3GPP Network between NF1 and NF2"}

To provide an overview of various mechanisms of mapping 5G E2E network slice to IETF network slices, we focus on IETF network slice INS1 in {{Figure4}} where IETF network slice INS1 provides the connectivity between network functions CU and UPF. {{Figure14}} shows this scenario.  Although the various mapping techniques considered in this section is for IETF network slice INS1, they are all applicable to other IETF network slices of {{Figure2}}, {{Figure3}} and {{Figure4}}, i.e., INS2, INS3 and INS4.

The IETF network slice INS1 provides the connectivity between service demarcation points SDP1 and SPD2.  These SDPs are the N3 interfaces on CU and UPF, respectively.  As shown in {{Figure14}}(A) and {{Figure14}}(B), the SDPs could be either loopback interfaces or a physical interfaces on CU and UPF network functions.  For simplicity case (A) is considered in this section although the various mapping methods are identically applicable to both cases (A) and (B).

~~~
          <-------------------- INS1 ------------------>

         SDP1                                        SDP2
       (N3 I/F)                                    (N3 I/F)
          |                 .-------.                  |
          |               ,'         `.                |
          v             ,'             `.              V
      --------       -------          -------       --------
      |   O  |       |     |          |     |       |  O   |
      |      |       | PE1 |          | PE2 |       |      |
      |  CU  |       |     |          |     |       |  UPF |
      --------       ------- Provider -------       --------
                         `.  Network  ,'
                           `.       ,'
                             -------
                               (A)


             <----------------- INS1 --------------->

            SDP1                                  SDP2
          (N3 I/F)                               (N3 I/F)
             |              .-------.               |
             |            ,'         `.             |
             v          ,'             `.           V
      --------       -------          -------       --------
      |      *       |     |          |     |       *      |
      |      |       | PE1 |          | PE2 |       |      |
      |  CU  |       |     |          |     |       |  UPF |
      --------       ------- Provider -------       --------
                         `.  Network  ,'
                           `.       ,'
                             -------
                               (B)
    Legend:
     <---> IETF Network Slice Service between SDP1 and SDP2
      *  SDP (N3 interface as CU IP interface)
      O  SDP (N3 as CU loopback interface)
~~~
{: #Figure14 title="Representation of a Typical IETF Network Slice between CU and UPF"}

Various techniques can be used to map the IETF network slice to 5G E2E network slice. The section covers the following techniques which can be used for mapping between 5G E2E network slice and {{!RFC9543}} network slice services. Note that these techniques might also be used by IETF network slice controller (NSC) to influence the realization of the IETF network slice services as well.  The latter case is out of scope of the current draft:

*  Mapping based on VLAN

*  Mapping based on MPLS label or SR-MPLS SID

*  Mapping based on SRv6 SID

*  Mapping based on Policy Based Routing (PBR)

*  Mapping based on UDP source port

It should be noted that the first three mapping mechanisms are briefly mentioned in {{TS-28.541}}.

## Mapping based on VLAN ID

In some scenarios, it would be possible for provider edge (PE) nodes to infer the identification of the 5G E2E network slices from the
VLAN ID carried in the data path traffic, and map the traffic to the corresponding IETF network slice.  As shown in {{Figure15}}, the IETF
Network slice INS1 between network functions CU and UPF can be mapped using the VLAN ID.  In this scenario, the VLANs assigned by network
functions CU and UPF are used for the handoff to the provider network.

Refer to section 4.1 of {{?I-D.ietf-teas-5g-ns-ip-mpls}} for details of this solution and how it is realized by provider network.

~~~
         <-------------------- INS1 ------------------->

           VLAN Handoff  IP/MPLS Services
                 |              |
                 |              |
        N3 I/F   |          .---|---.                N3 I/F
          |      |        ,'    |    `.                |
          V      V      ,'      V      `.              V
      --------       -------          -------       --------
      |   O..........+======================+...........O  |
      |      |       | PE1 |          | PE2 |       |      |
      | CU   |       |     |          |     |       | UPF  |
      --------       ------- Provider -------       --------
                         `.  Network  ,'
                           `.       ,'
                             -------

                               (A)
    Legend:
      O  SDP (N3 interface)
      +  Access points to provider network
      ... VLAN hand-off
      === IP/MPLS transport service in provider network
          (i.e., realization of INS1)
~~~
{: #Figure15 title="VLAN based IETF Network Slice Mapping"}

## Mapping based on MPLS Label or SR-MPLS SID

This section describes another solution for mapping the 5G E2E network slice traffic to IETF network slices based on MPLS/SR-MPLS labels/SIDs. The labels/SIDs carried in the packets sent from CU to UPF can be used by the provider edge (PE) nodes to infer the identification of the 5G E2E network slices and map the packet to the corresponding IETF network slice. {{Figure16}} shows an example where the 5G E2E network slice is mapped to IETF network slice INS1 using the MPLS label or SR-MPLS SID. In this case, the MPLS label or SR-MPLS SID is used for the handoff to the provider network.

Refer to section 4.3 of {{?I-D.ietf-teas-5g-ns-ip-mpls}} for details of this solution and how it is realized by provider network.

~~~
         <-------------------- INS1 ------------------->

          tunnel (represented by MPLS label or SR-MPLS SID)
                 |
                 |
        N3 I/F   |          .-------.                N3 I/F
          |      |        ,'         `.                |
          V      V      ,'             `.              V
      --------       -------          -------       --------
      |   *=============================================*  |
      |      |       | PE1 |          | PE2 |       |      |
      | CU   |       |     |          |     |       | UPF  |
      --------       ------- Provider -------       --------
                         `.  Network  ,'
                           `.       ,'
                             -------
                               (A)
    Legend:
         * SDP1 and SPD2 (N3 Address)
         === tunnel between SDP1 and SDP2 (MPLS or SR-MPLS)
~~~
{: #Figure16 title=" MPLS label or SR-MPLS SID based IETF Network Slice Mapping"}

## Mapping based on SRv6 SID

This section describes a solution for mapping the 5G  E2E network slice traffic to IETF network slices based on SRv6 SIDs.  This solution is similar to the mapping based on MPLS label or SR-MPLS SID but using  SRv6 tunnels.  As shown in {{Figure17}}, the SRv6 SIDs is added by CU or UPF to the data path traffic between SDP1 and SPD2.  The SRv6 SIDs can be used by the provider edge (PE) nodes to infer the identification of the 5G E2E network slices and map the traffic to the corresponding IETF network slice.

In this solution, the identification of the 5G E2E network slice may be embedded into IPv6 SIDs, where the 32-bit 3GPP network slice identification is mapped into the 128-bit IPv6 SID, thus the SRv6 SID is used for the handoff to the provider network.

Refer to section 4.2 of {{?I-D.ietf-teas-5g-ns-ip-mpls}} for details of this solution and how it is realized by the provider network.

~~~
         <-------------------- INS1 ------------------->

            SRv6 tunnel (represented by SRv6 SID)
                 |
                 |
        N3 I/F   |          .-------.                N3 I/F
          |      |        ,'         `.                |
          V      V      ,'             `.              V
      --------       -------          -------       --------
      |   *=============================================*  |
      |      |       | PE1 |          | PE2 |       |      |
      | CU   |       |     |          |     |       | UPF  |
      --------       ------- Provider -------       --------
                         `.  Network  ,'
                           `.       ,'
                             -------

                               (A)
    Legend:
         * SDP1 and SPD2 (N3 address)
         === SRv6 tunnel between SDP1 and SDP2
~~~
{: #Figure17 title="SRv6 SID based IETF Network Slice Mapping"}

## Mapping based on Policy Based Routing (PBR)

This section provides a solution for mapping the 3GPP E2E network slice traffic to IETF network slices.  As shown in {{Figure18}},
in some deployments of the 5G network slices, it would be possible for provider edge (PE) nodes to infer the identification of the 3GPP
E2E network slice from the content of the IP data packet sent between CU and UPF.  In these cases, the PE nodes can identify the 5G E2E
network slice using any combination of the following attributes and then map them to RFC9543 network slice services:

*  Source N3 IP address

*  Destination N3 IP address

*  Ingress interface

*  DSCP

*  Other information in the packet (at IP/MPLS layer or upper layers such as UDP/TCP)

Once the PE nodes receives the IP packets, it may apply infer the context of the 5G E2E network slice and then apply a policy-based routing (PBR) to the packet to map the traffic of specific 5G E2E network slice to the corresponding IETF network slices in the provider network.  The details of this solution is beyond scope of this draft.

~~~
         <-------------------- INS1 ------------------->

                    PBR        INS1        PBR
             enforcement    realization    enforcement
                     |          |           |
                     |          |           |
        N3 I/F       |      .---|---.       |        N3 I/F
          |          |    ,'    |    `.     |          |
          V          V  ,'      V      `.   V          V
      --------       -------          -------       --------
      |   O..........+======================+..........O   |
      |      |       | PE1 |          | PE2 |       |      |
      | CU   |       |     |          |     |       | UPF  |
      --------       ------- Provider -------       --------
                         `.  Network  ,'
                           `.       ,'
                             -------
    Legend:
      O  SDP ((N3 interface)
      +  Access points of IP/MPLS Services when PBR is enforced
      === IP/MPLS realization of the IETF network slice
~~~
{: #Figure18 title="Policy Based Routing (PBR) based IETF Network Slice Mapping"}

## Mapping based on UDP Source Port

This section provides another solution for mapping the 5G E2E network slice traffic to IETF network slices.  In some deployments of the 5G E2E network slices, it might be possible for PE nodes to infer the identification of the 3GPP E2E network slice based on the information of the GTP tunnels.  As shown in {{Figure19}}, the source UDP port of the data packet may be used to infer the identification
of 5G E2E network slices.  In this case, a mapping table between the identification of 5G network slice and the source UDP port needs to
be maintained by network functions CU, UPF and the PE nodes. 

The details of this solution is described in {{?I-D.ietf-dmm-tn-aware-mobility}}.

~~~
        <-------------------- INS1 ------------------->
         GTP tunnels
                 |
                 |
        N3 I/F   |          .-------.                N3 I/F
          |      |        ,'         `.                |
          V      V      ,'             `.              V
      --------       -------          -------       --------
      |   *=============================================*  |
      |   *=============================================*  |
      |      |       | PE1 |          | PE2 |       |      |
      | CU   |       |     |          |     |       | UPF  |
      --------       ------- Provider -------       --------
                         `.  Network  ,'
                           `.       ,'
                             -------
    Legend:
      *  SDP (N3 address)
         === GTP tunnels in context of IETF network slice INS1
~~~
{: #Figure19 title="UDP source port solution for IETF Network Slice Mapping"}


# IETF Network Slice request through IETF Network Slice NBI

As discussed in {{!RFC9543}}, to fulfill IETF network slices and to perform monitoring on them, an entity called IETF Network Slice Controller (NSC) is required to take abstract requests for IETF network slices and realize them using suitable underlying technologies.  An IETF Network Slice Controller is the key building block for control and management of the IETF network slice. It provides the creation/modification/deletion, monitoring and optimization of transport Slices in a multi-domain, a multi-technology and multi-vendor environment.

{{Figure20}} shows the NSC and its NBI interface for 5G, defined as IETF Network Slice Service Interface in {{!RFC9543}}.  Draft {{!I-D.ietf-teas-ietf-network-slice-nbi-yang}} a addresses the service yang model of such NSC NBI interface for all network slicing use-cases.

~~~
                  +------------------------------------------+
                  |            5G Customer (Tenant)          |
                  +------------------------------------------+
                                     A
                                     |
                                     V
                  +------------------------------------------+
                  |    5G E2E Network Slice Orchestrator     |
                  +------------------------------------------+
                                     A
                                     | IETF Network Slice Service Interface
                                     V
                  +------------------------------------------+
                  |    IETF Network Slice Controller (NSC)   |
                  +------------------------------------------+
                                     A
                                     | Network Configuration Interface
                                     V
                  +------------------------------------------+
                  |          Network Controller(s)           |
                  +------------------------------------------+
~~~
{: #Figure20 title="Interfaces of the IETF Network Slice Controller"}

As discussed in {{!RFC9543}}, the main task of the IETF Network Slice Controller is to map abstract IETF network slice requirements from NBI to concrete technologies on SBI and establish the required connectivity, and ensure that required resources are allocated to IETF network slice.  There are a number of different technologies that can be used on SBI including physical connections, MPLS, TSN, Flex-E, PON etc.  If the underlay technology is IP/MPLS/Optics, any IETF models can be used during the realization of the IETF network slice.

There are no specific mapping requirements for 5G.  The only difference is that in case of 5G, the NBI interface contains additional 5G specific attributes such as customer name, mobile service type, 5G E2E network slice ID (i.e.  S-NSSAI) and so on (See Section 6).  These 5G specific attributes can be employed by IETF Network Slice Controller during the realization of 5G IETF network slices on how to map NBI to SBI.  They can also be used for assurance of 5G IETF network slices.  {{Figure21}} shows the mapping between NBI to SBI for 5G IETF network slices.

~~~
                        | (1) NBI: Request to create/modify/delete
                        |          5G IETF Network Slice
                        V
             +----------------------+
             |  IETF Network Slice  | (2) Mapping between technology
             |    Controller (NSC)  |     agnostics NBI to technology
             +----------------------+     specific SBI
                       ^ ^ ^
                       | | |
                   |---| | |---|  (3) SBI: Realize 5G IETF Network Slice
                   |     |     |      by using various IETF models for
                   V     V     V      services, tunnels and paths
             +----------------------+
             |       Network        |-+
             |     Controller(s)    | |-+
             +----------------------+ | |
               +----------------------+ |
                 +----------------------+
~~~
{: #Figure21 title="Relationship between transport slice interface and IETF Service/Tunnels/Path data models"}


The following figure illustrates the relationship between 3GPP or ORAN subsystems connected through IETF TN domain. After the analysis
of 3GPP Generic Network Resource Models (NRM) of {{TS-28.540}} Rel 17, {{TS-28.541}} Rel 17 and {{TS-28.622}} Rel 16 the following objects have
been identified as entities on which the decision of mapping to IETF TN slices can be made. These available delineators of network
slices, represented by the arrows in the figure, are accessible in IETF domain and possible to be treated as triggers for decision of
mapping 3GPP slice to IETF TN slice.

Option (1) - the object class of 3GPP/ORAN subsystem is EP_Transport, {{TS-28.541}} clause 6.3.18, representing a list of attributes
including IETF-related parameters, directly exposed to transport network domain:

* ipAddress -- an IP address assigned on the 3GPP/ORAN subsystem side of the link to TN.

* logicInterfaceType and logicInterfaceId -- in current release it is an ID of the VLAN and encapsulation type is 802.1Q

These parameters can program the slice separation and be mapped to an IETF slice.

By instantiating EP_Transport per slice on 3GPP/ORAN subsystem the slicing may be implemented and mapped on slices in IETF TN domain.
In this case EP_Transport parameters may be mapped to draft-ietf-teas-ietf-network-slice-nbi-yang data model objects. This option is
described in the following example in current document.

Option (2) - the object class is EP_RP ({{TS-28.622}} clause 4.3.11), EP_F1U ({{TS-28.541}} clause 4.3.13), EP_NgU ({{TS-28.541}} clause 4.3.11), EP_N3 ( {{TS-28.541}} clause 5.3.20), representing the 3GPP link and association between 3GPP/ORAN subsystems. These attributes are not exposed directly to IETF TN domain and can be treated as loopbacks behind the link, defined in EP_Transport object class. Instantiation  and manipulation of EP_RPs per slice may be mapped on slices in IETF TN domain, while link defined by parameters of EP_Transport may remain the same. This delineation by loopbacks is adding secondary axis of flexibility to network slicing and needs to be mapped to {{!I-D.ietf-teas-ietf-network-slice-nbi-yang}} data model with different logic that delineation in option (1).


~~~
+------------------------+                   +------------------------+
||3GPP or ORAN subsystem |Provider Provider  |3GPP or ORAN subsystem  |
|(e.g. (O)-DU)           |Edge 1   Edge 2    |(e.g. (O)-CU-UP)        |
|+----------------------+|    +--+   +--+    |+----------------------+|
||Bearer                ||    |  |   |  |    ||Bearer                ||
||    +------+ +-------+||  | |  =====  | |  ||+-------+ +------+    ||
||    ?EP_RP ? ?EP_Tran?||  | |PE|   |PE| |  |||EP_Tran| |EP_RP |    ||
||    ?EP_F1U|-| sport X++--+-|  =====  |-+--|X  sport |-|EP_F1U|    ||
||    +---A--+ +---A---+||  | |  |   |  | |  |+----A---+ +-A----+    ||
|+--------+--------+----+|  | +--+   +--+ |  |+----+-------+-------- +|
+---------+--------+-----+  |             |  +-----+-------+----------+
           |        |        |             |        |       |
          (2)      (1)       AC            AC      (1)     (2)
     Customer Edge 1                               Customer Edge 2
~~~
{: #Figure22 title="Slice mapping options analysis based on 3GPP NRM"}

These basic options represent possible implementation options of objects and parameters Operator may use to instantiate slices and
correlate them with network slices in IETF TN domain to ensure SLA and SLO per slice.

Since 3GPP Generic Network Resource Models are not limiting use of these object classes and not mandating roles and mapping procedures,
 any combination of (1), (2) and (3) may be implemented in real slicing scenario.


(1) The use of slicing based on EP_Transport instantiation may be favorable due to direct exposure of connectivity parameters to IETF
TN domain. However, there are currently gaps in the NRM that may affect this option:

* The NRM Rel. 17 lacks definitions and object class structures for DC or DC-fabric implementations of RAN or CN instances.
* The attribute in EP_Transport qosProfile has no relation to clauses 5.3.84 QoSData and 5.3.79 FiveQiDscpMapping and cannot be
extracted or mapped to SLO/SLE constructs as the information is not available in the IETF domain.
* The destination of the traffic may potentially be extracted from EP_RP ({{TS-28.622}} clause 4.3.11), but this information is not
accessible in the IETF domain, so it cannot be extracted or mapped to communication type and connectivity constructs.
* Redundancy of EP_Transports is an open topic for failover and protection mechanisms

(2) The option of using a common EP_Transport and multiple EP_RP with unique IP addresses may be suitable for DC and DC-Fabric
implementations where EP_Transport establishes connectivity to the IETF TN domain and EP_RPs serve as virtual instance loopbacks.
However, the lack of direct exposure of IP addresses and slice demand parameters in the IETF domain may make this slicing option
challenging to implement. Currently, the following gaps have been identified:

* EP_Transport object class does not define a mechanism for active communication of EP_RP loopbacks to the IETF ingress PE device
(e.g., no PE-CE protocols)

* Redundancy for EP_Transports is still an open topic for failover and protection mechanisms, with the added complexity of EP_RP
loopback switchover

* Pre-installed policies in the IETF TN domain for pre-defined EP_RP loopbacks may result in network overprovisioning (e.g., PBR,
policies, service-match-criteria)

* The absence of a common toolset for monitoring the existence and activity of EP_RP loopbacks may hinder root cause analysis and
troubleshooting.

Following subsections present several examples for illustrating the mapping of 3GPP objects to IETF NBI YANG model.

Editorial note: further examples will be added in future versions of this document.

## Example according to CE-mode (OPTION 1)

This example considers the request of a slice for realizing the F1-U [3GPP {{TS-38.470}} interface between a DU and a CU-UP elements
(i.e., INS4 in previous {{Figure4}}). Note that the example is equally valid for the realization of any other case.

The example follows the CE-mode as described in {{Figure23}}.

~~~
  +-----+        Association between X and Y              +-----+
  |     |    according to 3GPP (i.e., NgU/N3 interface)   |     |
  | gNB |<----------------------------------------------->| UPF |
  |     |                                                 |     |
  +-----+                                                 +-----+

  +-----+       Association between DU and CU-UP          +-----+
  |     |    according to O-RAN (i.e., F1-U interface)    |     |
  |  DU |<----------------------------------------------->|CU-UP|
  |     |                                                 |     |
  +-----+                                                 +-----+
                     \__________  __________/
                                \/
    SDP1                                                  SDP2
 (with CE1 parameters)                       (with CE2 parameters)
    o<----------------- IETF Network Slice ---------------->o
    +                                                       +
    +|<------------------------- S1 ---------------------->|+
    +|                                                     |+
    +|                 |<------- T1 ----->|                |+
    +|                 v                  v                |+
    +v            +----+                  +----+           v+
 +--+--+    |     | PE1|==================| PE2|     |    +-+---+
 |  +  |    |     |    |                  |    |     |    | +   |
 |  o  X----------X    |                  |    X----------X o   |
 |     |    |     |    |                  |    |     |    |     |
 +-----+    |     |    |==================|    |     |    +-----+
            AC    +----+                  +----+     AC
 Customer         Provider                Provider         Customer
 Edge 1           Edge 1                  Edge 2           Edge 2


Legend:
O: Representation of the IETF network slice endpoints (SDP)
loopback interface in this example
+: Mapping of SDP to CE
X: Physical interfaces used for realization of IETF network slice
S1: L0/L1/L2/L3 services used for realization of IETF network slice
T1: Tunnels used for realization of IETF network slice
~~~
{: #Figure23 title="CE-mode slice realization example between DU and CU-UP OPTION"}


The 3GPP Management System is expected to handle different IOCs for both DU and CU-UP. For each of those 3GPP network entities, one of
the IOCs is the EP_RP, which describes each of the end-points in the association between 3GPP core entities, and the other IOC is the
EP_Transport, which provides information attributes about the point of attachment of each 3GPP core entity to the transport network.
Both objects are cross-referenced, so it is possible to get the information of one of them from the other.

{{Figure24}} shows the information provided at the DU side corresponding to the intended association with the CU-UP at the other end.

~~~
  +---------------------------------+
  |          EP_F1U CU-UP1          |<---+
  +---------------------------------+    |
  |   Parameter    |      Value     |    |
  +---------------------------------+    |
  |  localAddress  |     192.0.2.2  |    |
  +---------------------------------+    |
  | remoteipaddress|   198.51.100.2 |    |
  +---------------------------------+    |
  | epTransportRef |EP_Transport 100|    |
  +---------------------------------+    |
                  A                      |
                  |                      |
                  |                      |
                  V                      |
 +-----------------------------------+   |
 |         EP_Transport 100          |   |
 +-----------------------------------+   |
 |    Parameter     |      Value     |   |
 +-----------------------------------+   |
 |    ipAddress     |    192.0.2.1   |   |
 +-----------------------------------+   |
 |logicInterfaceType|      vlan      |   |
 +-----------------------------------+   |
 | logicInterfaceId |      100       |   |
 +-----------------------------------+   |
 |   NextHopInfo    |   192.0.2.254  |   |
 +-----------------------------------+   |
 |    qosProfile    |     5QI100     |   |
 +-----------------------------------+   |
 | epApplicationRef | EP_F1U CU-UP1  |<--+
 +-----------------------------------+
~~~
{: #Figure24 title="3GPP IOCs at DU side for the DU1 CU-UP1 connection
"}

Similarly, at CU-UP side the following objects are provided for setting up the network slice service towards DU, as represented in
{{Figure25}}.

~~~
  +---------------------------------+
  |            EP_F1U DU1           |<---+
  +---------------------------------+    |
  |   Parameter    |      Value     |    |
  +---------------------------------+    |
  |  localAddress  |  198.51.100.2  |    |
  +---------------------------------+    |
  | remoteipaddress|   192.0.2.2    |    |
  +---------------------------------+    |
  | epTransportRef |EP_Transport 100|    |
  +---------------------------------+    |
                  A                      |
                  |                      |
                  |                      |
                  V                      |
 +-----------------------------------+   |
 |         EP_Transport 100          |   |
 +-----------------------------------+   |
 |    Parameter     |      Value     |   |
 +-----------------------------------+   |
 |    ipAddress     |  198.51.100.1  |   |
 +-----------------------------------+   |
 |logicInterfaceType|      vlan      |   |
 +-----------------------------------+   |
 | logicInterfaceId |      100       |   |
 +-----------------------------------+   |
 |   NextHopInfo    | 198.51.100.254 |   |
 +-----------------------------------+   |
 |    qosProfile    |     5QI100     |   |
 +-----------------------------------+   |
 | epApplicationRef |   EP_F1U DU1   |<--+
 +-----------------------------------+
~~~
{: #Figure25 title="3GPP IOCs at CU-UP side for the DU1 CU-UP1 connection
"}

This is the basic information from where deriving the set of parameters feeding the NS NBI model.

According to this example, the following mapping could be performed.

 * SDPs: the SDPs in this example correspond to the IP addresses of the 3GPP core entities, thus 192.0.2.2 at the DU1 side and 198.51.100.2
 at the CU-UP1 side, both contained in the EP_RP object.
 * SLO / SLE policy: the SLO policy can be derived from  the QoS profile indicated in the EP_Transport object. SLE information are not
 directly expressed in 3GPP IOCs, then, if needed, SLE information should be complemented by other means (e.g., the 3GPP Slice Profile
 could provide indication of high reliability which could be translated to SLE values in the NBI YANG model internally to the NSC).
 * Peer SAP: the Next Hop info parameter in EP_Transport object can provide information about the SAP at the PE side, based on the IP
 address provided.
* AC: the conjugation of the IP address in the EP_Transport object, plus the information of the logical interface type and its
 identifier also in EP_Transport, can assist on determining the specific AC used for the network slice.

The resulting mapping is summarized in {{Figure26}}.

~~~
     SDP1                                                  SDP2
  (192.0.2.2)                                        (198.51.100.2)
     o<----------------- IETF Network Slice ---------------->o
     +                                                       +
     +|<------------------------- S1 ---------------------->|+
     +|                                                     |+
     +|  EP_Transport                         EP_Transport  |+
     +|   (192.0.2.1)    |<------ T1 ---->|  (198.51.100.1) |+
     +|     /            v                v            \    |+
     +v    /       +-----+                +-----+       \   v+
  +--+--+ /        | PE1 |================| PE2 |        \ +-+---+
  |  +  |/ |       |     |                |     |     |   \| +   |
  |  o  X----------X     |                |     X----------X o   |
  |     |  |       |\    |                |    /|     |    |     |
  |     |  |       | \   |                |   / |     |    |     |
  |     |  |     Peer SAP|                | Peer SAP  |    |     |
  |     |  |(192.0.2.254)|================|(198.51.100.254)|     |
  |     |  |       |     |                |     |     |    |     |
  +-----+  |       +-----+                +-----+     |    +-----+
  Customer |       Provider               Provider    |    Customer
  Edge 1   |       Edge 1                 Edge 2      |    Edge 2
           |                                          |
     AC (vlan 100)                               AC (vlan 100)
~~~
{: #Figure26 title="CE-mode slice realization example between DU and CU-UP with values"}

Further parameters can be filled in the NS NBI YANG model from the information provided. For instance, since there is one single pair
of EP_Transport objects, one on each end of the intended slice service, the connectivity construct can be requested as p2p. Since the
ranges of IP address of both DU1 and CU-UP1 could pertain to different block of prefixes, the NSC can take the decision of realizing
the network slice as a routed service. Here is important to remark that the IOCs from 3GPP do not provide any information regarding the
 mask applied to each prefix, so this can produce inconsistencies in the interpretation of the information received. Clearly this is a
gap necessary to be solved.

In addition to that, the logical interface type and its identifier can be used as match criteria for mapping traffic between DU1 and
CU-UP1 on the intended slice service.

As such, the NBI YANG model can result in something like:

~~~
{
  "data": {
    "ietf-network-slice-service:network-slice-services": {
      "slo-sle-templates": {
        "slo-sle-template": [
          {
            "id": "5QI100", /* QoS profile  as in EP_Transport*/
            "template-description": "5QI100 description"
          },
        ]
      },
      "slice-service": [
        {
          "service-id": "5GSliceMapping",
          "service-description": "example 5G Slice mapping",
          "slo-sle-template": "5QI100",
          "status": {
          },
          "sdps": {
            "sdp": [
              {
                "sdp-id": "01",
                "node-id": "DU1",
                "sdp-ip": "192.0.2.2",
                "service-match-criteria": {
                  "match-criterion": [
                    {
                      "index": 1,
                      "match-type": "vlan-match",
                      "target-connection-group-id": "DU-CU"
                    }
                  ]
                },
                "attachment-circuits": {
                  "attachment-circuit": [
                    {
                      "ac-id": "100",
                      "ac-ip-address": "192.0.2.1",
                      "ac-ip-prefix-length": ?,
                      "peer-sap-id": "192.0.2.254"
                    }
                  ]
                },
                "status": {
                }
              },
              {
                "sdp-id": "02",
                "node-id": "CU-UP1",
                "sdp-ip": "198.51.100.2",
                "service-match-criteria": {
                  "match-criterion": [
                    {
                      "index": 1,
                      "match-type": "vlan-match",
                      "target-connection-group-id": "DU-CU",
                      "target-connectivity-construct-id": 1
                    }
                  ]
                },
                "attachment-circuits": {
                  "attachment-circuit": [
                    {
                      "ac-id": "100",
                      "ac-ip-address": "198.51.100.1",
                      "ac-ip-prefix-length": ?,
                      "peer-sap-id": "198.51.100.254"
                    },
                  ]
                },
                "status": {
                }
              },
            ]
          },
          "connection-groups": {
            "connection-group": [
              {
                "connection-group-id": "DU-CU",
                "connectivity-type": "ietf-vpn-common:any-to-any",
                "connectivity-construct": [
                  {
                    "cc-id": 1,
                    "a2a-sdp": [
                      {
                        "sdp-id": "01"
                      },
                      {
                        "sdp-id": "02"
                      },
                    ]
                  }
                ]
              }
            ]
          }
        }
      ]
    }
  }
}

~~~

## Example according to PE-mode (OPTION 2)
This example considers the request of a slice for realizing the F1-U {{TS-38.470}} interface between a DU and a CU-UP elements (i.e.,
INS4 in previous {{Figure4}}). Note that the example is equally valid for the realization of any other case.

The example follows the PE-mode as described in {{Figure27}}.

~~~
+-----+        Association between X and Y              +-----+
|     |    according to 3GPP (i.e., NgU/N3 interface)   |     |
| gNB |<----------------------------------------------->| UPF |
|     |                                                 |     |
+-----+                                                 +-----+

+-----+        Association between DU and CU-UP         +-----+
|     |    according to O-RAN (i.e., F1-U interface)    |     |
|  DU |<----------------------------------------------->|CU-UP|
|     |                                                 |     |
+-----+                                                 +-----+
                   \__________  __________/
                               \/
             SDP1                                     SDP2
      (With PE1 parameters)                       (with PE2 parameters)
              o<--------- IETF Network Slice 1 ------->o
              +     |                            |     +
              +     |<----------- S1 ----------->|     +
              +     |                            |     +
              +     |    |<------ T1 ------>|    |     +
                +   v    v                  v    v   +
                  + +----+                  +----+ +
   +-----+    |     | PE1|==================| PE2|          +-----+
   |     |    |     |    |                  |    |     |    |     |
   |     |----------X    |                  |    X----------|     |
   |     |    |     |    |                  |    |     |    |     |
   +-----+    |     |    |==================|    |     |    +-----+
              AC    +----+                  +----+     AC
   Customer         Provider                Provider        Customer
   Edge 1           Edge 1                  Edge 2           Edge 2



Legend:
  O: Representation of the IETF network slice endpoints (SDP)
  +: Mapping of SDP to customer-facing ports on the PE
  X: Physical interfaces used for realization of IETF
network slice service
  S1: L0/L1/L2/L3 services used for realization of IETF
network slice service
  T1: Tunnels used for realization of IETF network slice service
~~~
{: #Figure27 title="PE-mode slice realization OPTION 2"}

The resulting mapping is summarized in {{Figure28}}.

~~~
              SDP1                                     SDP2
       (With PE1 parameters)                       (with PE2 parameters)
          (192.0.2.254)                             (198.51.100.254)
               o<--------- IETF Network Slice 1 ------->o
               +     |                            |     +
               +     |<----------- S1 ----------->|     +
               +     |                            |     +
               +     |    |<------ T1 ------>|    |     +
                 +   v    v                  v    v   +
                   + +----+                  +----+ +
    +-----+    |     | PE1|==================| PE2|          +-----+
    |     |----------X    |                  |    |     |    |     |
    |     |    |     |    |                  |    X----------|     |
    |     |    |     |    |                  |    |     |    |     |
    +-----+    |     |    |==================|    |     |    +-----+
               |     +----+                  +----+     |
    Customer   |     Provider                Provider   |    Customer
    Edge 1     |     Edge 1                  Edge 2     |     Edge 2
               |                                        |
          AC (vlan 100)                            AC (vlan 100)
~~~
{: #Figure28 title="PE-mode slice realization OPTION 2"}

From NBI YANG: The IETF network slice controller (NSC) uses 'node-id' (PE device ID), 'attachment circuit' ( ACs ) to map SDPs to the
customer-facing ports on the PEs

Gap: no info received in regards PE device ID. However we can retrieve the PE port IP address from NextHopInfo parameter, as sdp-ip

~~~
{
  "data": {
    "ietf-network-slice-service:network-slice-services": {
      "slo-sle-templates": {
        "slo-sle-template": [
          {
            "id": "5QI100", /* QoS profile  as in EP_Transport*/
            "template-description": "5QI100 description"
          },
        ]
      },
      "slice-service": [
        {
          "service-id": "5GSliceMapping-PE-mode",
          "service-description": "example 5G Slice mapping
following PE mode",
          "slo-sle-template": "5QI100", /* QoS profile  as
in EP_Transport*/
          "status": {
          },
          "sdps": {
            "sdp": [
              {
                "sdp-id": "01",
                "node-id": "PE1",
                "sdp-ip": "192.0.2.254", /* NextHopInfo IP
address in EP_Transport */
                "service-match-criteria": {
                  "match-criterion": [
                    {
                      "index": 1,
                      "match-type": "vlan-match", /*logicInterfaceType*/
                      "target-connection-group-id": "DU-CU"
                    }
                  ]
                },
                "attachment-circuits": {
                  "attachment-circuit": [
                    {
                      "ac-id": "100", /*logicInterfaceId*/
                      "ac-ip-address": "192.0.2.254", /* Next
HopInfo IP address in EP_Transport, redundant, can be removed */
                      "ac-ip-prefix-length": ?, /* not available */
                      "peer-sap-id": "192.0.2.254"
                    }
                  ]
                },
                "status": {
                }
              },
              {
                "sdp-id": "02",
                "node-id": "PE2",
                "sdp-ip": "198.51.100.254", /* NextHopInfo IP address
in EP_Transport */
                "service-match-criteria": {
                  "match-criterion": [
                    {
                      "index": 1,
                      "match-type": "vlan-match", /*logicInterfaceType*/
                      "target-connection-group-id": "DU-CU",
                      "target-connectivity-construct-id": 1
                    }
                  ]
                },
                "attachment-circuits": {
                  "attachment-circuit": [
                    {
                      "ac-id": "100", /*logicInterfaceId*/
                      "ac-ip-address": "198.51.100.254", /* NextHopInfo
IP address in EP_Transport, redundant, can be removed */
                      "ac-ip-prefix-length": ?, /* not available */
                      "peer-sap-id": "198.51.100.254"
                    },
                  ]
                },
                "status": {
                }
              },
            ]
          },
          "connection-groups": {
            "connection-group": [
              {
                "connection-group-id": "DU-CU",
                "connectivity-type": "ietf-vpn-common:any-to-any",
** Note: there is a hint from NRM on {{TS-28.541}} Clause 4.3.11, 4.3.13, 5.3.20 relationsip between 3GPP elements on the logical link connection with attributes localAddress and remoteAddress. This information may be correlated with the connectivity and analyzed to make a decision on the connectivity type.**
                "connectivity-construct": [
                  {
                    "cc-id": 1,
                    "a2a-sdp": [
                      {
                        "sdp-id": "01"
                      },
                      {
                        "sdp-id": "02"
                      },
                    ]
                  }
                ]
              }
            ]
          }
        }
      ]
    }
  }
}
~~~

## Example According to PE-mode with Meeting Point Extension of ACaaS (OPTION 3)

This example is based on the Option 2 when SDP is located on the PE and utilizing the same approach for the data model of the Network Slice Service, but "attachment-circuits" section of the model is referring to the identifiers that are created using the data models specified in {{!I-D.draft-ietf-opsawg-teas-attachment-circuit}}

This example following the overall conception in {{ZSM-003}} of confederated data model approach and SDO Data Model cross-referencing in order to get quicker Service and Slice provisioning in multiple domains under various SDO areas of focus, fueling closed-loop automation direction in the Management lifecycle of Slices and Services.

3GPP NRM Rel 18 LogicalInterfaceInfo (Section 6.3.35 of {{TS-28.541}}) represents 3GPP IOC with TN-related parameters of the 3GPP subsystem interpreted in this example (Option 3) as CE network configuration of current model and may be referenced as a 'peer-sap-id' remote endpoint of the attachment circuit with parameters as 'nf-termination-ip' and 'nf-termination-vlan' (see more on SAPs at {{!RFC9408}}; and parameters related to the physical connection and associated with Bearer Service "ietf-ac-svc:attachment-circuits:ietf-bearer-svc".

3GPP NRM ConnectionPointInfo (Section 6.3 of {{TS-28.541}}) represents 3GPP IOC with link to the external IETF data model {{!I-D.draft-ietf-opsawg-teas-attachment-circuit}} in order to link the corresponding 3GPP subsystem Transport Network-related slice Meeting Point (Clause 6.3.18 of {{TS-28.541}}, EP_Transport) to the IETF Network Slice attachment circuit.

As the {{!I-D.ietf-teas-ietf-network-slices}} has flexibility of Network-Specific abstraction, a need for more attention to connectivity parameters was identified during collaboration activity in O-RAN Alliance Working Group 9 between the 3GPP SA5 representatives and IETF contributors.

{{!I-D.draft-ietf-opsawg-teas-attachment-circuit}} is used jointly to the Network Slice Service YANG model  to capture and reflect IETF PE connectivity to 3GPP subsystem parameters such as:

- Physical parameters of the bearer, captured in the "ietf-bearer-svc" YANG Module of {{!I-D.draft-ietf-opsawg-teas-attachment-circuit}}, contains the physical connectivity parameters that the link is utilizing, site location, (3GPP) device information, the IETF PE is connected to, and administrative operational parameters as status and activation time constraints.
- Location information, correlated with NRM {{TS-28.623}} in corresponding 3GPP element id in Clause A 2.2.2 IOC ManagedElement.locationName attribute.
- Logical connectivity parameters: e.g., VLAN, IPv4, and IPv6.
- Routing protocols

While 3GPP NRM Rel 17 (Section 6.3.18 of {{TS-28.541}})  EP_Transport Attribute "nextHopInfoList" from Clause 6.3.18.2 is associated with "ietf-network-slice-service:network-slice-services:slice-service:sdp:sdp-ip" value, in 3GPP NRM Rel 18 {{TS-28.541}} Clause 6.3.18 EP_Transport Attribute list no longer contains IP address of TN element, but a link to IETF meeting point with connectionPointId value of "ietf-ac-svc:attachment-circuits:ac:name".

Provisioning procedures of the 3GPP Elements are captured in {{TS-28.531}} where relationship between NRM leaf and IETF AC "ietf-ac-svc:attachment-circuits:ac:name" is depicted.

Note: Possible values of the attribute, specifying the type of the connection point identifier "connectionPointIdType" are VLAN, MPLS, Segment, IPv4, IPv6, and Attachment Circuit (AC). In current example Option 3 "Attachment Circuit (AC)" is used.



{{Figure29}} captures Transport-related parameters.

~~~
              SDP1                                     SDP2
       (With PE1 parameters)                       (with PE2 parameters)
          (192.0.2.254)                             (198.51.100.254)
               o<--------- IETF Network Slice 1 ------->o
               +     |                            |     +
               +     |<----------- S1 ----------->|     +
               +     |                            |     +
               +     |    |<------ T1 ------>|    |     +
                 +   v    v                  v    v   +
  (192.0.2.1)        + +----+                  +----+ +      (198.51.100.1)
    +-----+    |     | PE1|==================| PE2|          +------+
    |     |----------X    |                  |    |     |    |      |
    | DU1 |    |     |    |                  |    X----------|CU-UP1|
    |     |    |     |    |                  |    |     |    |      |
    +-----+    |     |    |==================|    |     |    +------+
               |     +----+                  +----+     |
    Customer   |     Provider                Provider   |    Customer
    Edge 1     |     Edge 1                  Edge 2     |     Edge 2
               |                                        |
          AC-ID (vlan 100)                          AC-ID (vlan 100)
~~~
{: #Figure29 PE-mode Slice Realization Option 2"}

The following attributes mapping is assumed in this example:

~~~
---DU1---
3GPP NRM {{TS-28.541}} Clause 6.3.18 EP_Transport
         ipAddress: '192.0.2.1/24'
         localLogicalInterfaceInfo: "DU1_LogicalInterfaceInfo"
         qosProfile: '5QI100'
         connectionPointRefList: "DU1_Meeting_point"
3GPP NRM Rel 18 {{TS-28.541}} Clause 6.3.35 LogicalInterfaceInfo: "DU1_LogicalInterfaceInfo"
         logicalInterfaceType: 'VLAN'
         logicalInterfaceId: '100'
         systemName: 'DU1'
         portName: 'XE'
         routingProtocol: 'Static'

** Note: LogicalInterfaceInfo.routingProtocol has Allowed values:  RIP, IGMP, OSPF, EGP, EIGRP, BGP, IS-IS.**
** Identified gap: No Static or Direct_connect value is available.**

3GPP NRM {{TS-28.541}} Clause 6.3.41   ConnectionPointInfo: "DU1_Meeting_point"
         connectionPointId: 'ac01-DU1'
         connectionPointIdType: 'Attachment_Circuit'

** Note: connectionPointIdType has Allowed values: VLAN, MPLS, Segment, IPV4, IPV6, Attachment Circuit (AC) with multiplicity: 1

3GPP NRM {{TS-28.623}} Clause A 2.2.2 IOC ManagedElement
         id: 'DU1'
         locationName: 'Site1.AAA1.ZIP1'
** Note: The physical location (e.g., an address) of an 3GPP entity. It may contain no information to support the case where the derivative of ManagedElement needs to represent a distributed multi-location NE."**

---CU-UP1---
3GPP NRM {{TS-28.541}} Clause 6.3.18 EP_Transport
         ipAddress: '198.51.100.1/24'
         localLogicalInterfaceInfo: "CU-UP1_LogicalInterfaceInfo"
         qosProfile: '5QI100'
         connectionPointRefList: "CU-UP1_Meeting_point"

3GPP NRM Rel 18 {{TS-28.541}} Clause 6.3.35 LogicalInterfaceInfo: "CU-UP1_LogicalInterfaceInfo"
         logicalInterfaceType: 'VLAN'
         logicalInterfaceId: '100'
         systemName: 'CU-UP1'
         portName: 'XE'
         routingProtocol: 'Static'

3GPP NRM {{TS-28.541}} Clause 6.3.41   ConnectionPointInfo: "CU-UP1_Meeting_point"
         connectionPointId: 'ac01-CU-UP1'
         connectionPointIdType: 'Attachment_Circuit'

3GPP NRM {{TS-28.623}} Clause A 2.2.2 IOC ManagedElement
         id: 'CU-UP1'
         locationName: 'Site1.AAA2.ZIP2'
----
{
  "data": {
    "ietf-network-slice-service:network-slice-services": {
      "slo-sle-templates": {
        "slo-sle-template": [
          {
            "id": "5QI100", /* QoS profile  as in EP_Transport*/
            "template-description": "5QI100 description"
          },
        ]
      },
      "slice-service": [
        {
          "service-id": "5GSliceMapping-PE-mode",
          "service-description": "example 5G Slice mapping
following PE mode",
          "slo-sle-template": "5QI100", /* QoS profile  as
in EP_Transport*/
          "status": "active"
          "sdps": {
            "sdp": [
              {
                "sdp-id": "01",
                "node-id": "PE1",
                "ac-svc-name:ac-ref": [
                 "ac01-DU1"
** 3GPP NRM {{TS-28.541}} DU1.ConnectionPointInfo."DU1_Meeting_point".connectionPointId **
                 ]
                "status": "active"
              {
                "sdp-id": "02",
                "node-id": "PE2",
                "ac-svc-name:ac-ref": [
                 "ac01-CU-UP1" **3GPP NRM {{TS-28.541}} CU-UP1.ConnectionPointInfo.
"CU-UP1_Meeting_point".connectionPointId**
                 ]
                "status": "active"
              },
              ]
              },
          },
          "connection-groups": {
            "connection-group": [
              {
                "connection-group-id": "DU-CU",
                "connectivity-type": "ietf-vpn-common:any-to-any",
                "connectivity-construct": [
                  {
                    "cc-id": 1,
                    "a2a-sdp": [
                      {
                        "sdp-id": "01"
                      },
                      {
                        "sdp-id": "02"
                      },
                    ]
                  }
                ]
              }
            ]
          }
        }
      ]
    }
  }

"ietf-ac-svc:attachment-circuits": {
       "ac": [
         {
           "name": "ac01-DU1",
** 3GPP NRM {{TS-28.541}} Clause 6.3.41   ConnectionPointInfo.connectionPointId **
           "description": "meeting point DU1-PE1",
           "l2-connection": {
             "encapsulation": {
               "type": "ietf-vpn-common:dot1q",
** 3GPP NRM Rel 18 {{TS-28.541}} Clause 6.3.35 LogicalInterfaceInfo.logicalInterfaceType **
         logicalInterfaceType: 'VLAN'
               "dot1q": {
                 "cvlan-id": 100
** 3GPP NRM Rel 18 {{TS-28.541}} Clause 6.3.35 LogicalInterfaceInfo.logicalInterfaceId **
               }
             },
             "bearer-reference": "line-156"
           },
           "ip-connection": {
             "ipv4": {
               "local-address": "192.0.2.254",
               "prefix-length": 24,
               "address": [
                 {
                   "address-id": "1",
                   "customer-address": "192.0.2.1"
**3GPP NRM {{TS-28.541}} Clause 6.3.18 DU1.EP_Transport.ipAddress**
                 }
               ]
             },
           "routing-protocols": {
             "routing-protocol": [
               {
                 "id": "1",
                 "type": "ietf-vpn-common:direct-routing"
** 3GPP NRM Rel 18 {{TS-28.541}} Clause 6.3.35 LogicalInterfaceInfo.routingProtocol **
               }
             ]
           }
           "name": "ac01-CU-UP1",
** 3GPP NRM {{TS-28.541}} Clause 6.3.41   ConnectionPointInfo.connectionPointId **
           "description": "meeting point CU-UP1-PE2",
           "l2-connection": {
             "encapsulation": {
               "type": "ietf-vpn-common:dot1q",
** 3GPP NRM Rel 18 {{TS-28.541}} Clause 6.3.35 LogicalInterfaceInfo.logicalInterfaceType **
               "dot1q": {
                 "cvlan-id": 100
** 3GPP NRM Rel 18 {{TS-28.541}} Clause 6.3.35 LogicalInterfaceInfo.logicalInterfaceId **
               }
             },
             "bearer-reference": "line-345"
           },
           "ip-connection": {
             "ipv4": {
               "local-address": "198.51.100.254",
               "prefix-length": 24,
               "address": [
                 {
                   "address-id": "1",
                   "customer-address": "198.51.100.1"
**3GPP NRM {{TS-28.541}} Clause 6.3.18 CU-UP1.EP_Transport.ipAddress**
                 }
               ]
             },
           "routing-protocols": {
             "routing-protocol": [
               {
                 "id": "1",
                 "type": "ietf-vpn-common:direct-routing"
** 3GPP NRM Rel 18 {{TS-28.541}} Clause 6.3.35 LogicalInterfaceInfo.routingProtocol **
               }
             ]
           }
         }

"ietf-ac-svc:ietf-bearer-svc":{
   "bearers": [
         {
           "id": "line-156" //Note that bearer-reference is returned in the response
           "description": "link DU1-PE1"
           "customer-point": {
             "identified-by": "ietf-bearer-svc:site-and-device-id",
               "device": {
                 "device-id": "DU1"
** Either 3GPP NRM Rel 18 {{TS-28.541}} Clause 6.3.35 LogicalInterfaceInfo: "DU1_LogicalInterfaceInfo".
systemName or 3GPP NRM {{TS-28.623}} Clause A 2.2.2 IOC ManagedElement.DU1.id **
                 "site": {
                   "site-id": "Site1.AAA1.ZIP1"
** 3GPP NRM {{TS-28.623}} Clause A 2.2.2 IOC ManagedElement.DU1.locationName**
           }
          }
         }
           "id": "line-345"
           "description": "link CU-UP1-PE2"
           "customer-point": {
             "identified-by": "ietf-bearer-svc:site-and-device-id",
             "device": {
                 "device-id": "CU-UP1"
** Either 3GPP NRM Rel 18 {{TS-28.541}} Clause 6.3.35 LogicalInterfaceInfo: "CU-UP1_LogicalInterfaceInfo".
systemName or 3GPP NRM {{TS-28.623}} Clause A 2.2.2 IOC ManagedElement.CU-UP1.id **
                 "site": {
                   "site-id": "Site1.AAA2.ZIP2"
** 3GPP NRM {{TS-28.623}} Clause A 2.2.2 IOC ManagedElement.CU-UP1.locationName**
        }
       }
      }
     }
    }
  ]
 }
}

~~~

# Gap Analysis
The way in which 3GPP is characterizing the slice endpoint (i.e.,
EP_Transport) is based on Layer 3 information (e.g., the IP Address).
However the information provided seems not to be sufficient for
instructing the IETF Network Slice Controller for the realization of
the IETF NEtwork Slice.  For instance, some basic information such as
the mask associated to the IP address of the EP_Transport is not
specified, as well as other kind of parameters like the connection
MTU or the connectivity type (unicast, multicast, etc).  More
sophisticated information could be required as well, like the level
of isolation or protection necessary for the intended slice.

In the case in which the 3GPP managed function runs on a purpose-
specific network element, the IP address specified in the
EP_Transport IOC serves as reference to identify the CE endpoint,
assuming the endpoint of the CE has been configured with that IP
address.  With that information (together with the logical interface
ID) should be sufficient for the IETF NSC to identify the counterpart
endpoint at the PE side, and configuring it accordingly (e.g., with a
compatible IP address) for setting up the slice end-to-end.
Similarly, the next hop information in EP_Transport can help validate
the end-to-end slice between PE endpoints.

In the case in which the 3GPP managed function is instantiated as a
virtualized network function, the direct association between the IP
address of EP_Transport and the actual endpoint mapped at the CE is
not so clear.  It could be the case, for instance when the
virtualized network function is instantiated at the internal of a
data center, that the CE facing the PE is far from the point where
the function is deployed, being that connectivity extended through
the internals of the data center (or by some internal configuration
of a virtual switch in a server).  In these situations additional
information is needed for accomplishing the end-to-end connection.

At the same time, {{TS-28.541}} IOC contains useful parameters to be
used in IETF Network Slice creation mechanism and enriching IETF
Network Slice model.  The following parameters may be suggested as a
candidates to the correlation of the IETF Network Slice parameters
and IETF Network Slice model enrichments:

*  For the latency, dLThptPerSliceSubnet, uLThptPerSliceSubnet,
   reliability and delayTolerance attributes, the following NRM apply
   (with reference to the section in that specification):

   -  CNSliceSubnetProfile (section 6.3.22 in {{TS-28.541}})

   -  RANSliceSubnetProfile (section 6.3.23 in {{TS-28.541}})

   -  TopSliceSubnetProfile (section 6.3.24 in {{TS-28.541}})

*  For the qosProfile attribute, the NRM which applies is
   EP_Transport (detailed in section 6.3.18 in {{TS-28.541}})

# IANA Considerations
This document makes no request of IANA.

   Note to RFC Editor: this section may be removed on publication as an
   RFC.

# Security Considerations
To be completed.

# Evolution Considerations

 3GPP NRM evolution of the data model approach is considered for Rel. 18.

{: numbered="false"}
# Acknowledgments
The work of Luis M.  Contreras has been partially funded by the
European Commission under Horizon 2020 project Int5Gent (grant
agreement 957403.

Thanks to Philip Eardley (philip.eardley@bt.com) for his contribution
to this document.

{: numbered="false"}
# Annex 1: 3GPP Network Slice Mapping Parameters

The network slice concept was introduced in 3GPP specifications from
the first 5G release, corresponding to Release 15.  As captured in
{{TS-23.501}}, a network slice represents a logical network providing
specific network capabilities and network characteristics.

To make slicing a reality, every technical domain is split into one
or more logical network partitions, each referred to as a network
slice subnet.  The definition of multiple slice subnets on a single
domain allows each segment to provide differentiated behaviors, in
terms of functionality and/or performance, tailored to some specific
needs.  The stitching of slice subnets across the RAN, CN and TN
results in the definition of 5G network slices in 3GPP.

From a management viewpoint, the concept of network slice subnet
represents an independently manageable yet composable portion of a
network slice.  The rules for the definition of network slice subnet
and their composition into network slices are detailed in the 5G
Network Resource Model (NRM) {{TS-28.541}}, specifically in the Network
Slice NRM fragment.  This fragment captures the information model of
5G network slicing, which specifies the relationships between
different slicing related managed entities, which is represented as
Information Object Class (IOC).  The IOC that have been defined
including: NetworkSlice IOC, NetworkSliceSubnet IOC, ManagedFunction
IOC and EP_Transport IOC.

Information Object Class EP_Transport {{TS-28.541}} Clause 6.3.18
represents logical interface parameters of 3GPP subsystems, providing
specific network capabilities and network characteristics.
Relationships of Transport slicing-related 3GPP IOCs and IETF domain
represented on the Figure X for NgU/N3 slices with traffic between
3GPP CU-UP (or ORAN) CU-UP and 3GPP UPF, while the Figure Y similarly
represents F1-U slices with traffic between 3GPP (or ORAN) DU and
3GPP (or ORAN) CU-UP.


~~~
             +----------------------------------+
             |      Slices in 3GPP domain       |
             |  Model defined in IOC TS-28.541  |
             |          NgU/N3 slices           |
             +----+--------------------------+--+
+-----------------|+                         |
|   3GPP CU-UP /  ||                       +-|---------------+
| ORAN O-CU-UP #1 ||        .-----.        | |3GPP (i)UPF #1 |
| +---------------V|      ,'  TN   `.      +-V--------------+|
| | EP_NgU link to |     |  domain   |     | EP_N3 link to  ||
| |     UPF #1     |    ;             :    |    CU-UP #1    ||
| |+---------------|    ;  .-------.  :    +---------------+||
| ||EP_Transport 10+------(Slice 10 )------|EP_Transport 10|||
| |+---------------|   |   `-------'   |   +---------------+||
| |                |   |               |   |                ||
| |+---------------|   :   .-------.   ;   +----------------||
| ||EP_Transport 20+------(Slice 20 )------|EP_Transport 20 ||
| |+---------------|A   :  `-------'  ;   A+----------------||
| +----------------||    |           |    |+----------------+|
|            . . . ||     |         |     || . . .           |
| +----------------||      `.     ,'      |+----------------+|
| | EP_NgU link to ||        `---'        || EP_NgU link to ||
| |     UPF #N     ||                     ||   CU-UP #N     ||
| +----------------||                     |+----------------+|
+------------------+|                     |+-----------------+
                    |                     |
             +------+---------------------+--------+
             |    logical transport interfaces     |
             |     e.g. GTP-U, IPSec endpoint      |
             +-------------------------------------+

~~~
{: #Figure30 title="Slicing example realization between 3GPP subsystems and TN on the NgU/N3 interface"}

~~~
             +----------------------------------+
             |      Slices in 3GPP domain       |
             |  Model defined in IOC TS-28.541  |
             |            F1-U slices           |
             +-+-------------------------+------+
+--------------|+                       +|-----------------+
|  3GPP DU /   ||                       ||  3GPP CU-UP /   |
| ORAN O-DU #1 ||                       ||ORAN O-CU-UP #1  |
|              ||        .-----.        ||                 |
|+-------------V|      ,'  TN   `.      +V---------------+ |
|| EP_F1-U link |     |  domain   |     |EP_F1-U link to | |
|| to CU-UP #1  |    ;             :    |     DU #1      | |
|+--------------|    ;   .-----.   :    +--------------+ | |
||EP_Transport 1+-------(Slice 1)-------|EP_Transport 1| | |
|+--------------|   |    `-----'    |   +--------------+ | |
||              |   |               |   |                | |
|+--------------|   :    .-----.    ;   +--------------+ | |
||EP_Transport 2+-------(Slice 2)-------|EP_Transport 2| | |
|+--------------|A   :   `-----'   ;   A+--------------+ | |
|+--------------||    |           |    |+----------------+ |
|         . . . ||     |         |     || . . .            |
|+--------------||      `.     ,'      |+----------------+ |
|| EP_F1-U link ||        `---'        ||EP_F1-U link to | |
|| to CU-UP #N  ||                     ||     DU #N      | |
|+--------------||                     |+----------------+ |
+---------------+|                     |+------------------+
                 |                     |
                 |                     |
          +------+---------------------+--------+
          |    logical transport interfaces     |
          |     e.g. GTP-U, IPSec endpoint      |
          +-------------------------------------+
~~~
{: #Figure31 title="Slicing example realization between 3GPP subsystems and TN on the F1-U interface"}

For the transport (i.e., connectivity) related part of a network
slice, the key focus is on the EP_Transport IOC.  Instances of this
IOC serves to instantiate 3GPP interfaces (e.g., N3) which are needed
to support Network Slicing and to define Network Slice transport
resources within the 5G NRM.  In a nutshell, the EP_Transport IOC
permits to define additional logical interfaces for each slice
instance of the 3GPP user plane.

According to {{TS-28.541}}, the EP_Transport construct on 3GPP side has
the following attributes: ipAddress, logicaInterfaceInfo,
nextHopInfo, qosProfile and epApplicationRef In which, nextHopInfo
could be used for choosing PE node in transport network and
LogicalInterfaceInfo could be used for Transport Network Slice
mapping.

nextHopInfo (optional): identifies the ingress transport node.  Each
node can be identified by any combination of IP address of next-hop
router of transport network, system name, port name and IP management
addresses of transport nodes.

logicInterfaceInfo (mandatory): a set of parameters, which includes
logicInterfaceType and logicInterfaceId.  It specifies the type and
identifier of a logical interface.  It could be a VLAN ID, MPLS Tag
or Segment ID.  This is assigned uniquely per slice.

From the Transport Network domain side, these parameters assist on
the definition of the CE transport interface configuration and shall
be taken as an input to the transport service model to create
coherent Network Slice transport service.  {{Figure32}} illustrates how the
EP_Transport parameters can relate to the IETF ones for determining
the endpoint connectivity.


~~~
+-----------------------+        .-----.        +-----------------+
|     3GPP CU-UP /      |      ,'  TN   `.      | 3GPP (i)UPF #1  |
|    ORAN O-CU-UP #1    |     |  domain   |     |                 |
|+----------------------|  +-----------+   :    +----------------+|
||EP_NgU link to UPF #1 |  |   PE 1    |   :    | EP_N3 link to  ||
||                      |  |           |    :   |    CU-UP #1    ||
||+---------------------|  | .-------. |    |   +---------------+||
|||  EP_Transport for   +--+(Slice 10 )+----+---| EP_Transport  |||
|||     S-NSSAI FWA     |  |A`-------' |    ;   +---------------+||
|||logicInterfaceType = |  +|----------+   ;    +----------------+|
|||       Vlan ID       |   |:             ;    +-----------------+
||| logicInterfaceId =  |   | |           |
|||      Vlan 200       |   |  |         |
|||ipAddress = 192.0.2.1|   |   `.     ,'
||+--------------A------|   |     `---'
|+---------------|------| +-+-------------------+
+----------------|------+ |   nextHopInfoList   |
                 |        |NextHopInfo = IP/mask|
  +--------------+------+ |       of PE 1       |
  | epApplicationRef =  | | system name = PE 1  |
  |EP_NgU link to UPF#1 | |  port name = Gi1/1  |
  +---------------------+ +---------------------+
~~~
{: #Figure32 title="Example of 3GPP EP_Transport IOC TS-28.541 parameters with correlation to IETF"}

Furthermore, that same parameters should be leveraged for
constituting the connectivity construct allowing endpoint
interconnection.  That is, there is no additional information that
could be leveraged at service level that the one provided by
EP_Transport, which essentially reflects an endpoint view. {{Figure18}}
represents this relationship between 3GPP and IETF parameters.


~~~
   3GPP subsystem - CE                   Transport Network node - PE
 +----------------------+                 +----------------------+
 |InformationObjectClass|                 |   IETF Slice Model   |
 |                      <----------------->                      |
 |     EP_Transport     |                 |  LxSM + extensions   |
 +----------------------+                 +----------------------+

 Representation of connectivity:
 EP_NgU/N3, link between (O)-CU-UP and UPF
 F1-U, link between (O)-DU and (O)-CU-UP
~~~
{: #Figure33 title="Relationships of the 3GPP parameters with the IETF parameters"}

   Leveraging on the EP_Transport information, the IETF NSC should be
   instructed through its NBI on performing the slice connection.  {{Figure34}}
   graphically represents the slice connection (e.g., for Ng-U/N3) as
   expected by 3GPP by using connectivity constructs (of a IETF Network
   Slice service) to be configured by the IETF Network Slice Controller.

~~~
     Slices in 3GPP domain                         Slices in 3GPP domain
  Model defined in IOC TS-28.541          Model defined in IOC TS-28.541

+------------------+                                +------------------+
|3GPP CU-UP / ORAN |                                |   3GPP UPF #1    |
|   O-CU-UP #1     |      Slices in IETF domain     |                  |
|                  |                                |                  |
|+-----------------|     +----+           +----+    +-----------------+|
|| EP_NgU link to  |     |PE 1|           |PE 2|    |  EP_N3 link to  ||
||     UPF #1      |     |    |    .-.    |    |    |    CU-UP #1     ||
||+----------------|     |    |   |   |   |    |    +----------------+||
||| EP_Transport   |     |    |  |     |  |    |    |EP_Transport for|||
|||for S-NSSAI 100 o--------------PDU 1-------------o  S-NSSAI 100   |||
|||   Vlan 100     |     |    | |       | |    |    |    Vlan 100    |||
|||  IP 192.0.2.1  |<--->|    | ;       : |    |<-->|IP 198.51.100.1 |||
||+----------------|     |    |;         :|    |    +----------------+||
||+----------------|     |    ||         ||    |    +----------------+||
||| EP_Transport   |     |    ||         ||    |    |EP_Transport for|||
|||for S-NSSAI 200 o--------------PDU 2-------------o  S-NSSAI 200   |||
|||   Vlan 200     |     |    ||         ||    |    |    Vlan 200    |||
|||  IP 192.0.2.2  |<--->|    ||   TN    ||    |<-->|IP 198.51.100.2 |||
||+----------------|     |    ||         ||    |    +----------------+||
||                 |     |    ||         |+----+    +-----------------+|
|+-----------------|     |    ||         |          +------------------+
|+-----------------|     |    |:         ;+----+    +------------------+
|| EP_NgU link to  |     |    | :       ; |PE 3|    |   3GPP UPF #2    |
||     UPF #2      |     |    | |       | |    |    +-----------------+|
||Serving S-NSSAI  o--------------PDU 3-------------o  EP_N3 link to  ||
||      100        |<--->|    |  :     ;  |    |<-->|    CU-UP #1     ||
|+-----------------|     |    |  :     ;  |    |    | Serving S-NSSAI ||
+------------------+     +----+   `. ,'   +----+    |       100       ||
                                   '                +-----------------+|
                                                    +------------------+
~~~
{: #Figure34 title="Example of CU-UP Slice in the 3GPP domain using an IETF Network Slice service"}

From the perspective of IETF Network Slice realization, some of these
   options could be realized in a straightforward manner while other
   could require of advanced features (e.g., PBR, SRv6, FlexE, etc).
   IETF Network Slice service may be a set of techniques and underlaying
   technologies, so multiple models may be used to define slice.

   According to the {{TS-28.541}} attributes in the EP_Transport, the IETF
   Network Slice may be defined by the following combination of the
   parameters:

~~~
    +------------------------------------------------------------------+
    |                   EP_Transport attribute name                    |
    |                                                                  |
    +---------------+----------------+----------------+----------------+
    |   ipAddress   |logicInterfaceId|   nextHopInfo  | qosProfile     |
    +---------------+----------------+----------------+----------------+
    |                   Different                     |  Same for all  |
    |                   per slice                     |    slices      |
    +---------------+---------------------------------+----------------+
    |  Same for all |           Different             |  Same for all  |
    |    slices     |           per slice             |    slices      |
    +---------------+----------------+----------------+----------------+
    |   Different   |  Same for all  |   Different    |  Same for all  |
    |   per slice   |    slices      |   per slice    |    slices      |
    +---------------+----------------+----------------+----------------+
    |         Same for all           |   Different    |  Same for all  |
    |           slices               |   per slice    |    slices      |
    +--------------------------------+----------------+----------------+
    |                            Different                             |
    |                            per slice                             |
    +---------------+--------------------------------------------------+
    |  Same for all |                    Different                     |
    |    slices     |                    per slice                     |
    +---------------+--------------------------------------------------+
~~~
{: #Figure35 title="Variations of Slice implementation options"}

From the perspective of IETF Network Slice realization, some of these
   options could be realized in a straightforward manner while other
   could require of advanced features (e.g., PBR, SRv6, FlexE, etc).

   IETF Network Slice service may be a set of techniques and underlaying
   technologies, so multiple models may be used to define slice.

{: numbered="false"}
# Annex 2: Data Plane Mapping Options

The following picture shows the end-to-end network slice in data
plane:

~~~
+--+       +-----+                           +----------------+
|UE|- - - -|(R)AN|---------------------------|       UPF      |
+--+       +-----+                           +----------------+
 |<----AN NS---->|<----------TN NS---------->|<----CN NS----->|
~~~
{: #Figure36 title="End-to-end network slice in data plane"}

The mapping between 3GPP slice and transport slice in user plane
could happens in:

(R)AN: User data goes from (radio) access network to transport
network

   Editor's Note: As figure 4.7.1. in {{TS-28.530}} describes, TN NS will
   not only exist between AN and CN but may also within AN NS and CN NS.
   However, here we just show the TN between AN and CN as an example to
   avoid unnecessary complexity.

   The following picture shows the user plane protocol stack in end-to-
   end 5G system.

~~~
  +-----------+                    |                  |               |
  |Application+--------------------|------------------|---------------|
  +-----------+                    |                  | +-----------+ |
  | PDU Layer +--------------------|------------------|-| PDU Layer | |
  +-----------+   +-------------+  |  +-------------+ | +-----------+ |
  |           |   | ___Relay___ |--|--| ___Relay___ |-|-|           | |
  |           |   |     \/ GTP-U|--|--|GTP-U\/ GTP-U|-|-|   GTP-U   | |
  |   5G-AN   |   |5G-AN +------+  |  +------+------+ | +-----------+ |
  |  Protocol |   |Protoc|UDP/IP|--|--|UDP/IP|UDP/IP|-|-|   UDP/IP  | |
  |   Layers  |   |Layers+------+  |  +------+------+ | +-----------+ |
  |           |   |      |  L2  |--|--|  L2  |  L2  |-|-|     L2    | |
  |           |   |      +------+  |  +------+------+ | +-----------+ |
  |           |   |      |  L1  |--|--|  L1  |  L1  |-|-|     L1    | |
  +-----------+   +-------------+  |  +-------------+ | +-----------+ |
       UE              5G-AN       |        UPF       |      UPF      |
                                   N3                 N9              N6
~~~
{: #Figure37 title="User plane protocol stack in end-to-end 5G system"}

The following figure shows the typical encapsulation in N3 interface.

~~~
   +------------------------+
   | Application Protocols  |
   +------------------------+
   |       IP (User)        |
   +------------------------+
   |          GTP           |
   +------------------------+
   |          UDP           |
   +------------------------+
   |          IP            |
   +------------------------+
   |       Ethernet         |
   +------------------------+
~~~
{: #Figure38 title="Typical encapsulation in N3 interface"}

## Layer 3 and Layer 2 Encapsulations
   If the encapsulation above IP layer is not visible to Transport
   Network, it is not able to be used for network slice interworking
   with transport network.  In this case, IP header and Ethernet header
   could be considered to provide information of network slice
   interworking from AN or CN to TN.

~~~
   +------------------------+-----------
   | Application Protocols  |      ^
   +------------------------+      |
   |       IP (User)        |  Invisible
   +------------------------+     for
   |          GTP           |     TN
   +------------------------+      |
   |          UDP           |      V
   +------------------------+------------
   |          IP            |
   +------------------------+
   |       Ethernet         |
   +------------------------+
~~~
{: #Figure39 title="IP header for network slice interworking "}

The following field in IP header and Ethernet header could be considered:

   IP Header:

   *  DSCP: It is traditionally used for the mapping of QoS identifier
      between AN/CN and TN network.  Although some values (e.g.  The
      unassigned code points) may be borrowed for the network slice
      interworking, it may cause confusion between QoS mapping and
      network slicing mapping.;

   *  Destination Address: It is possible to allocate different IP
      addresses for entities in different network slice, then the
      destination IP address could be used as the network slice
      interworking identifier.  However, it brings additional
      requirement to IP address planning.  In addition, in some cases
      some AN or CN network slices may use duplicated IP addresses.

   *  Option fields/headers: It requires that both AN and CN nodes can
      support the encapsulation and decapsulation of the options.

   Ethernet header

   *  VLAN ID: It is widely used for the interconnection between AN/CN
      nodes and the edge nodes of transport network for the access to
      different VPNs.  One possible problem is that the number of VLAN
      ID can be supported by AN nodes is typically limited, which
      effects the number of IETF network slices a AN node can attach to.
      Another problem is the total amount of VLAN ID (4K) may not
      provide a comparable space as the network slice identifiers of
      mobile networks.
   Two or more options described above may also be used together as the
   IETF Network Slice Interworking ID, while it would make the mapping
   relationship more complex to maintain.

   In some other case, when AN or CN could support more layer 3
   encapsulations, more options are available as follows:

   If the AN or CN could support MPLS, the protocol stack could be as
   follows:

~~~
   +------------------------+-----------
   | Application Protocols  |      ^
   +------------------------+      |
   |       IP (User)        |  Invisible
   +------------------------+     for
   |          GTP           |     TN
   +------------------------+      |
   |          UDP           |      V
   +------------------------+------------
   |         MPLS           |
   +------------------------+
   |          IP            |
   +------------------------+
   |       Ethernet         |
   +------------------------+
~~~
{: #Figure40 title="MPLS label for network slice interworking "}

A specified MPLS label could be used to as a IETF Network Slice
Interworking ID.

If the AN or CN could support SRv6, the protocol stack is as follows:

~~~
   +------------------------+-----------
   | Application Protocols  |      ^
   +------------------------+      |
   |       IP (User)        |  Invisible
   +------------------------+     for
   |          GTP           |     TN
   +------------------------+      |
   |          UDP           |      V
   +------------------------+------------
   |          SRH           |
   +------------------------+
   |         IPv6           |
   +------------------------+
   |       Ethernet         |
   +------------------------+
~~~
{: #Figure41 title="SRH for network slice interworking "}

The following field could be considered to identify a network slice:
SRH:

   *  SRv6 functions: AN/CN is supposed to support the new function
      extension of SRv6.

   *  Optional TLV: AN/CN is supposed to support the extension of
      optional TLV of SRH.
###  Above Layer 3 Encapsulations
If the encapsulation above IP layer is visible to Transport Network,
it is able to be used to identify a network slice.  In this case, UPD
and GTP-U could be considered to provide information of network slice
interworking between AN or CN and TN.

~~~
   +------------------------+----------
   | Application Protocols  |     |
   +------------------------+ Invisible
   |       IP (User)        |     for
   +------------------------+     TN
   |          GTP           |     |
   +------------------------+------------
   |          UDP           |
   +------------------------+
   |          IP            |
   +------------------------+
   |       Ethernet         |
   +------------------------+
~~~
{: #Figure42 title="UDP Header for network slice interworking "}

The following field in UDP header could be considered:

   UDP Header:

   *  UDP Source port: The UDP source port is sometimes used for load
      balancing.  Using it for network slice mapping would require to
      disable the load-balancing behavior.

   A similar approach to this is followed in
   {{?I-D.ietf-dmm-tn-aware-mobility}}

### Consideration of the Virtual Network Functions (VNF)
In some 5G network slice deployments, it might be beneficial to
deploy RAN and Core network functions such as DU, CU and UPF as
virtual network functions (VNF) inside a data center (DC).  As an
example, consider Figure 40 where the CU and UPF have been deployed
as VNF.  The definition of the IETF network slice service INS1 stays
identical to its PNF counterpart (physical network function) which
are discussed in sections 7.2.1 to 7.2.5, i.e., INS1 is an IETF
network slice service which provides the connectivity between SDP1
and SDP2 to satisfy certain SLO/SLE.

However, the mapping of INS1 might be different from previous use
cases.  Figure 40 shows one possible solution for mapping of INS1
where the 5G E2E network slice is first mapped inside the data center
and then mapped to provider network PE nodes.  One potential mapping
in the data center is to use VxLAN ID to infer the identification of
5G E2E network slice inside the data center, and any of the options
described in 7.2.1 to 7.2.5 in the provider network PE1 and PE2.

~~~
         <-------------------- INS1 ------------------->
           Mapping of INS1       Mapping of INS1
           in data center        in provider network
                   |              |
          SDP1     |              |                     SDP2
           |       |          .---|---.                  |
           V       V        ,'    |    `.                V
    |------------|        ,'      V      `.        |------------|
    |  --------  |     -------          -------    |  --------  |
    |  |   O...........+======================+..........O   |  |
    |  |      |  |     | PE1 |          | PE2 |    |  |      |  |
    |  | CU   |  |     |     |          |     |    |  | UPF  |  |
    |  --------  |     ------- Provider -------    |  -------   |
    |            |         `.  Network  ,'         |            |
    |------------|           `.       ,'           |------------|
         DC1                   -------                   DC2
    Legend:
         DC  Data Center
         O   SDP (N3 address)
         === Mapping of INS1 on Provider Network PE nodes
         ... Mapping of INS1 in data centers
~~~
{: #Figure43 title="VNF Consideration for IETF Network Slice Mapping"}

#  Summary

   From all the options overviewed, it should be noted that current 3GPP
   Release 16 only supports through EP_Transport IOC the following slice
   handoff identifier: vlan tag.  MPLS or SID labels.  Thus, the
   consideration of more options as the ones here reported is a gap on
   3GPP specifications.
