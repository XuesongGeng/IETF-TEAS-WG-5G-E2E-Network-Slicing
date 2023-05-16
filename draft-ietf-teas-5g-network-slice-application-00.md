---
title: "IETF Network Slice Application in 3GPP 5G End-to-End Network Slice"
category: info
docname: draft-ietf-teas-5g-network-slice-application
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: "Routing Area"
workgroup: "TEAS Working Group"
keyword:
- Network Slice 
- Architecture
- Mapping 3GPP

author:
 -
    fullname: Your Name Here
    organization: Your Organization Here
    email: your.email@example.com
 -
    fullname: Xuesong Geng
    organization: Huawei Technologies
    email: gengxuesong@huawei.com
 -
    fullname: Luis M. Contreras
    organization: Telefonica
    email: luismiguel.contrerasmurillo@telefonica.com
 -
    fullname: Reza Rokui
    organization: Ciena
    email: rrokui@ciena.com
 -
    fullname: Jie Dong
    organization: Huawei Technologies
    email: jie.dong@huawei.com
 -
    fullname: Ivan Bykov
    org: Ribbon Communications
    email: Ivan.Bykov@rbbn.com

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
    email: jefftant.ietf@gmail.com
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
   draft-ietf-dmm-tn-aware-mobility:
              title: "Mobility aware Transport Network Slicing for 5G"
              date: 2023-04-19   
              target: https://datatracker.ietf.org/doc/draft-ietf-dmm-tn-aware-mobility/

   TS-23.501:
              title: "3GPP TS 23.501: System architecture for the 5G System (5GS)"
              date: 2022-03-25
              target: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3144
   TS-23.501:
              title: "3GPP TS 23.501: System architecture for the 5G System (5GS)"
              date: 2022-03-25
              target: https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3144
   TS-28.541:
              title: "3GPP TS 28.541 Management and orchestration; 5G Network Resource Model (NRM); Stage 2 and stage 3"
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
   GST:
              title: "GSMA Generic Network Slice Template"
              date: 2019-10-19
              target: https://www.gsma.com/newsroom/all-documents/generic-network-slice-template-v2-0/
   ZSM-003:
              title: "ETSI ZSM003 Zero-touch network and Service Management (ZSM); End-to-end management and orchestration of network slicing"
              date: 2021-06
              target: https://www.etsi.org/deliver/etsi_gs/ZSM/001_099/003/01.01.01_60/gs_ZSM003v010101p.pdf


--- abstract

Network Slicing is one of the core features in 5G, which provides
different network service as independent logical networks. To provide 5G
network slices service, an end-to-end network slice needs to consists of
3 major types of network segments: Radio Access Network (RAN), Mobile
Core Network (CN) and Transport Network (TN). This document describes
the application of IETF network slice in providing 5G end-to-end network
slices, including the network slice identification mapping, network
slice parameter mapping and 5G IETF Network Slice NBI.

--- middle

# Introduction

Driven by the new applications of 5G, the concept of network slicing
is defined to provide a logical network with specific capabilities
and characteristics.  Network slice contains a set of network
functions and allocated resources (e.g. computation, storage and
network resources).
The IETF Network Slice (NS) service is defined in
{{!I-D.ietf-teas-ietf-network-slices}} as a set of connections between a   
number of CEs, with that connections having specific Service Level   
Objectives (SLOs) and Service Level Expectations (SLEs) over a common   
underlay network, with the traffic of one customer being separated   
from another.  The concept of IETF network slice is conceived as
technology agnostic.

The IETF NS service is specified in terms of the set of endpoints
(from CE perspective) connected to the slice, the type ofThe IETF NS service is specified in terms of the set of endpoints
connectivity among them, and a set of SLOs and SLEs for each
connectivity construct.

In {{!I-D.ietf-teas-ietf-network-slice-nbi-yang}}, the endpoints are
described by an identifier, with some metrics associated to the
connections among them as well as certain policies (e.g., rate limits
for incoming and outgoing traffic).

The 5G network slice as defined in {{TS-23.501}} does not take the
transport network slice into consideration.  This document introduces
the concept of 5G end-to-end network slice, which is composed of
three major types network segments: Radio Access Network (RAN),
Transport Network (TN) and Mobile Core Network (CN).  Transport
network is supposed to provide the required connectivity between AN
and CN or inside AN/CN, with specific performance commitment.  For
each end-to-end network slice, the topology and performance
requirement for transport network can be very different, which
requests transport network to have the capability of supporting
multiple different transport network slices.

This document addresses the request of IETF Network Slice services
for 3GPP 5G Network Slices.  The realization of such requested slices
is out of the scope of this document and addressed in other documents
such as {{!I-D.srld-teas-5g-slicing}}.

# Terminologies
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT"
"SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in th
document are to be interpreted as described in {{!RFC2119}}.

Terminologies for IETF Network Slice go along with the definition 
{{!I-D.ietf-teas-ietf-network-slices}}.

The following terms are used in this document:

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


# 5G End-to-End Network Slice
The scope of 5G End-to-End Network Slice discussed in this document
is shown in {{Figure1}}.  Transport network provides connectivity
between and inside RAN and CN.  To support fully automated enablement
an assurance of 5G E2E network slices, multiple controllers are
needed to manage 5G E2E network slices in RAN, Core and Transport
domains.  In addition, an E2E network slice orchestrator is needed to
provide coordination and control of network slices from an E2E
perspective.

~~~
       +-----------------------------------------------------+
       |          +-----------------------------+            |            
 |-----+----------+----------------+            |            | 
 |   ******   +---+---+   ******   | +----+     |            |  
 |  *      *  |       |  *      *  | |    |     |            | 
 | *  RAN   ---  TN   ---  RAN   --|--    |     |            |  
 |  * NFs  *  |       |  * NFs  *  | |    |     |            |  
 |   ******   +-------+   ******   | |    |     |            |
 |---------------------------------+ |    |   +-+--+  +------+------+
                 RAN                 |    |   |IETF|  |   5G E2E    |
                                     |    +---+ NSC+--+Network Slice|
                                     |TN  |   |    |  | Orchestrator|
                                     |    |   +-+--+  +------+------+
 +---------------------------------+ |    |     |            |           
 |   ******   +-------+   ******   | |    |     |            |        
 |  *      *  |       |  *      *  | |    |     |            |        
 | *  CN    ---  TN   ---  CN   ---|--    |     |            |           
 |  * NFs  *  |       |  * NFs  *  | |    |     |            |           
 |   ******   +---+---+   ******   | +----+     |            |           
 +-----+----------+----------------+            |            |          
       |        CN|                             |            |  
       |          +-----------------------------+            |  
       +-----------------------------------------------------+
~~~
{: #Figure1 title="Scope of 5G End to End Network Slice"}

Depends on Radio Access Network (RAN) deployment, one or multiple
   IETF network slice might be needed in 3GPP network.  In the details
   of various IETF network slices for following RAN deployment will be
   discussed:

   *  Distributed RAN

   *  Centralized RAN

   *  Cloud RAN (C-RAN)

  Distributed RAN is the most common deployment of 3GPP RAN networks as
   shown in {{Figure2}}.  The radio acess network (RAN) is connected to
   Core network (CN) using the IETF transport network (TN1).

~~~
      <-------------- 3GPP E2E Network Slice  ------------->
        <---- RS ---->           <-------- CS ---------->
                       <- INS1 ->         <- INS2 ->
      .................          .........................
      : RAN           :          : CN                    :
      :               : ........ :        .......        :
      : |----| |----| : :      : : |----| :     : |----| :
      : | NF1| | NF2| : :  TN1 : : | NF | : TN2 : | NF | :
      : |----| |----| : :      : : |----| :     : |----| :
      :               : :......: :        :.....:        :
      :...............:          :.......................:

      Legend
        INS: IETF Network Slice
        RS: RAN Slice
        CS: Core Slice
        TN: IETF network
        CN: Core Network
        RAN:Access Neetwork (Radio)
~~~
{: #Figure2 title="IETF network slices in distributed RAN deployment"}

## IETF Network Slices in Centralized RAN deployment
   In general the RAN network consists of network functions NF1 and MF2.
   NF1 processes the radio signal and is connected to the transport
   network and NF2 transmits and receives the carrier signal that is
   transmitted over the air to the end user equipment (UE).  In
   Centralized RAN as depicted in {{Figure3}}, network functions NF1 and
   NF2 are separated by a network called fronthaul network (FH).

   In this deployment a 3GPP E2E network slice contains of RAN and Core
   slices and IETF network slices INS1, INS2 and INS3.  INS1 and INS2
   are identical to {{Figure2}} and INS3 is a new IETF network slice across
   access network between NF1 and NF2.

~~~
      <-------------------- 3GPP E2E Network Slice  ----------------->
        <-------- RS --------->           <---------- CS --------->
             <- INS3 ->        <- INS1 ->         <- INS2 ->
      .........................          ...........................
      : RAN                   :          : CN                      :
      :        .......        : ........ :         .......         :
      : |----| :     : |----| : :      : : |-----| :     : |-----| :
      : | NF1| : TN3 : | NF2| : :  TN1 : : | NF  | : TN2 : | NF  | :
      : |----| : (FH): |----| : :      : : |-----| :     : |-----| :
      :        :.....:        : :......: :         :.....:         :
      :.......................:          :.........................:

   Legend
     INS: IETF Network Slice
     RS: RAN Slice
     CS: Core Slice
     FN: Fronthaul IETF network
     TN: IETF network
     CN: Core Network
     RAN:Access Neetwork (Radio)
~~~
{: #Figure3 title="IETF network slices in centralized RAN deployment"}

##  IETF Network Slices in Cloud RAN deployment (C-RAN)

   In Cloud RAN deployment, the network function NF2 is further
   disaggregated into real-time and non-real-time components.  As shown
   in {{Figure4}}, these disaggregated components are called CU (Central
   Unit) and DU (Distributed Unit) where they are connected by a new
   network called Midhaul network (MH).

   In this deployment a single 3GPP E2E network slice contains not only
   RAN and 5G Core slices but IETF network slices INS1, INS2, INS3 and
   INS4.  IETF network slices INs1, INS2 and INS3 are identical to their
   counterparts in centralized RAN deployment case (Refer to {{Figure3}}).
   In this deployment a new IETF network slice INS4 connects the DUs to
   CUs through F1 interfaces.

~~~   
     <---------------------- 3GPP E2E Network Slice  ------------------>
      <-------------- RS -------------->          <------- CS ------>
            <- INS3 ->      <- INS4 ->   <- INS1 ->     <- INS2 ->
     .....................................        .....................
     : RAN                               :        :CN                 :
     :       .......       ......        : ...... :       .....       :
     : |---| :     : |---| :     : |---| : :    : : |---| :   : |---| :
     : |NF1| : TN3 : | DU| : TN4 : | CU| : :TN1 : : | NF| :TN2: | NF| :
     : |---| : (FH): |---| : (MH): |---| : :(BH): : |---| :   : |---| :
     :       :.....:       :.....:       : :....: :       :...:       :
     :...................................:        :...................:

     Legend
      INS: IETF Network Slice
      RS: RAN Slice
      CS: Core Slice
      FN: Fronthaul IETF network
      MN: Midhaul IETF bnetwork
      BH: Backhual IETF network
      TN: IETF network
      DU: Distributed Unit
      CU: Central Unit
      CN: Core Network
      RAN:Access Neetwork (Radio)
~~~
{: #Figure4 title="IETF network slices in cloud RAN deployment (C-RAN)"}

## Relationship between IETF network slice and 3GPP network slice

   For the sake of description, the descriptions below all take the TN
   slice between RAN and CN as an example, and the other cases are
   similar.  {{Figure5}} shows the correspondence between network entities
   in E2E 5G slices and IETF slices respectivel

~~~
       +---------------------+
       |         CSMF        |
       +----------|----------+
                  |                    +------------------------+
       +---------------------+         |  5G E2E Network Slice  |
       |         NSMF        |         |      Orchestrator      |
       +---------------------+         +------------------------+
             /    |    \                            |
            /     |     \                  NSC NBI  |
           /      |      \                          |
  +---------++---------++---------+    +------------------------+
  |    AN   ||    TN   ||   CN    |    |   IETF Network Slice   |
  |   NSSMF ||   NSSMF ||  NSSMF  |    |     Controller (NSC)   |
  |         ||         ||         |    +------------------------+
  +---------++---------++---------+         NSC SBI |
       |          |          |                      |
       |          |          |         +------------------------+
       |          |          |         |    Network Controllers |
       |          |          |         +------------------------+
       |          |          |                      |
       |          |          |                      |
   .─────.    .───────.    .───────.            .─────────.
  ╱  5G   ╲  ╱  IETF   ╲  ╱   5G    ╲          ╱   IETF    ╲
 (   RAN   )(  Network  )(   Core    )        (   Domain    )
  `.     ,'  `.       ,'  `.       ,'          `.         ,'
    `───'      `─────'      `─────'              `───────'
   
~~~
 {: #Figure5 title="Relationship between 3GPP domain controllers and IETF Network Slice Controller"} 

   An example of 5G E2E Network Slice is showed in {{Figure6}}.  Each e2e
   network slice contains AN slice, CN slice and one or more IETF
   network Slices. 3GPP identifies each e2e network slice using an
   integer called S-NSSAI.  In {{Figure4}} there are three instances of e2e
   network slices which are identified by S-NSSAI 01111111, 02222222 and
   02333333, respectively.  Each instance of e2e network slice contains
   AN slice, CN Slice and one or more IETF network slices.  For example,
   e2e network slice 01111111 has AN Slice instance 4, CN Slice instance
   1 and IETF network slice 6.  Note that 3GPP does not cover the IETF
   network slice.  See {{!I-D.ietf-teas-ietf-network-slices}} for details
   of IETF network slice.
   Note that 3GPP uses the terms NSI and NSSI which are a set of network
   function and required resources (e.g. compute, storage and networking
   resources) which corresponds to network slice Instance, whereas
   S-NSSAI is an integer that identifies the e2e network slice.

~~~
               +-----------+ +-----------+  +-----------+
               |  S-NSSAI  | |  S-NSSAI  |  |  S-NSSAI  |
               |  01111111 | |  02222222 |  |  03333333 |
               +---|-------+ +---|---|---+  +----|------+
                   |  +----------+   |           |
                   V  V              V           V
                 *******       ********      ********
   Core         * NSSI 1 *    * NSSI 2 *    * NSSI 3 *
   Network       ********      ********      ********
                     \              \             /
                      \              \           /
                      +-----+       +-----+    +-----+
   Transport          | IETF|       | IETF|    | IETF|
   Network            | NS 6|       | NS 7|    | NS 8|
                      +-----+       +-----+    +-----+
                          \              \   /
                           \              \ /
     Radio                 ********     ********
    Access                * NSSI 4 *   * NSSI 5 *
    Network                ********     ********
~~~
{: #Figure6 title="5G End-to-End Network Slice and its components"} 

   The following network slice related identifiers in management plane,
   control plane and data(user) plane play an important role in end-to-
   end network slice mapping:

   *  Single Network Slice Selection Assistance Information(S-NSSAI):
      The end-to-end network slice identifier, which is defined in
      {{TS-23.501}}; S-NSSAI is used during 3GPP network slice signalling
      process.

   *  IETF Network Slice Identifier: An identifier allocated by IETF
      Neetwork Slice Controller (NSC) in management plane.  In data
      plane, IETF Network Slice Identifier may be instantiated with
      existing data plane identifiers and doesn't necessarily require
      new encapsulation.

   *  IETF Network Slice Interworking Identifier: Data-plane network
      slice identifier which is used for mapping the end-to-end network
      slice traffic to specific IETF network slice.  The IETF Network
      Slice Interworking Identifier is a new concept introduced by this
      draft, which may be instantiated with existing data plane
      identifiers and doesn't necessarily require new encapsulation.

   Note: the term "IETF Network Slice Interworking Identifier" is
   proposed but requires further discussion.

4.  Overview of the mapping between 3GPP and IETF network slices

   Referring to Figure 2-1, 2-2 and 2-3, a 3GPP network slice might have
   one or more IETF network slices.  Figure 7 is a representation of any
   of these networks where the IETF network slice provides the
   connectivity between NF1 and NF2 for specific SLO/SLE.  For example,
   Figure 7 could represent Figure 2-3 where the IETF network slice
   needed between network functions are CU and UPF or it could represent
   the Figure 2-3 where the IETF network slice is between network
   functions DU and CU.
   
   ~~~

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
{: #Figure7 title="Typical IETF Network Slice in 3GPP Network"}

   To provide an overview of various IETF network slice realization
   solutions, we focus on Figure 2-3 where the IETF network slide is
   INS1 and NF1 and NF2 are CU and UPF, respectively.  Figure 8 shows
   Although the realization methods described below is related to INS1,
   they are applicable to other IETF network slices of Figure 2-1, 2-2
   and 2-3.  The result is shown in Figure 5.  Please note that the IETF
   network slice INS1 is between SDP1 and SPD2 which are the N3
   interfaces on CU and UPF, respectively.  As shown in Figure 8(A) and
   Figure 8(B), the SDPs could be the loopback interface or IP
   interface.  For simplicity only case (A) is considered for the rest
   of the section although the various realization methods are
   applicable to both cases.

   ~~~
         SDP1                  INS1                  SDP2
       (N3 I/F)                 |                  (N3 I/F)
          |                 .---|---.                  |
          |               ,'    |    `.                |
          v             ,'      V      `.              V
      --------       -------          -------       --------
      |   o=============================================o  |
      |      |       | PE1 |          | PE2 |       |      |
      | CU   |       |     |          |     |       | UPF  |
      --------       ------- Provider -------       --------
                         `.  Network  ,'
                           `.       ,'
                             -------
                               (A)

            SDP1               INS1                SDP2
          (N3 I/F)              |                (N3 I/F)
             |              .---|---.               |
             |            ,'    |    `.             |
             v          ,'      V      `.           V
      --------       -------          -------       --------
      |      *======================================*      |
      |      |       | PE1 |          | PE2 |       |      |
      | CU   |       |     |          |     |       | UPF  |
      --------       ------- Provider -------       --------
                         `.  Network  ,'
                           `.       ,'
                             -------

                               (B)
    Legend:
      *  SDP (N3 interface as CU IP interface)
      O  SDP (N3 as CU loopback interface)
~~~
{: #Figure8 title="Representation of a Typical IETF Network Slice in 3GPP Network"}

   To realize the INS1 shown in Figure 8(A), the IETF network slice
   controller (NSC) can use the following techniques:

   *  VLAN handoff
   *  MPLS label handoff
   *  SRv6 label handoff
   *  Policy Based Routing (PBR)
   *  GTP source port based

##  VLAN Hand-off

   As shown in Figure 9, the IETF Network slice INS1 is realized between
   network functions CU and UPF using the VLAN handoff.  In this case
   the VLAN is hand-off ID from the 3GPP network slice to provider
   network.  Refer to section 5 for details of this solution.
   
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
~~~
{: #Figure9 title="VLAN hand-off based for IETF Network Slice Realization"}

##  SRv6 Label Hand-off

   Figure 10 depicts the realization of the IETF network slice INS1
   using the SRv6 label handoff method.  In this case, an SRv6 label
   which represents the 3GPP network slice is added by CU or UPF to IP
   traffic.  In this case, network function CU and UPF are the endpoint
   of the realization of IETF network slice INS1 and PE nodes do not
   have any context of the IETF network.
   In this solution the identification of the 3GPP network slice is
   embedded into IPv6 label where the 32-bit 3GPP network slice
   identification is mapped into 128 bit of IPV6 label.  In this case
   the SRv6 SID is hand-off ID from the 3GPP network slice to provider
   network.  Refer to section 5 for details of this solution.

~~~
         <-------------------- INS1 ------------------->

           SRv6 tunnel
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
      * Access points to SRv6 Tunnel. Also the SDP (N3 interface)
      === Realization of the INS1 using SRv6 tunnel
~~~
{: #Figure10 title="SRV6 hand-off based for IETF Network Slice Realization"}


##  MPLS Lable Hand-off

   Similar to section 2.4.2, the MPLS label based method uses an MPLS
   label as identification of the 3GPP network slice.  {{Figure11}} shows
   this solution where the IETF network slice INS1 is relaized by CU and
   UPF using the MPLS label.  In this case, network function CU and UPF
   are the endpoint of the realization of IETF network slice INS1 and PE
   nodes do not have any context of the IETF network.  In this case the
   MPLS is hand-off ID from the 3GPP network slice to provider network.
   Refer to section 5 for details of this solution.

~~~
         <-------------------- INS1 ------------------->

           MPLS label tunnel
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
      * Access points to MPLS Tunnel. Also the SDP (N3 interface)
      === Realization of the INS1 using MPLS lable

~~~
{: #Figure11 title="MPLS hand-off based for IETF Network Slice Realization"}


##  Policy based routing (PBR)

   As shown in Figure 12, in some deployments of the 3GPP network
   slices, it would be possible for provider edge (PE) nodes to infer
   the 3GPP network slice identification from the information in the IP
   packet.  In these cases, the IETF network slice INS1 is identified by
   provider edger (PE) routers by a policy which might use any
   combination of the following attributes of the IP packet.

   *  Source N3 IP address

   *  Destination N3 IP address

   *  Ingress interface

   *  DSCP

   *  Other information in IP packet
   
  ~~~
         <-------------------- INS1 ------------------->

                    PBR  IP/MPLS Services  PBR
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
      +  Access points of IP/MPLS Services when PBR is applied
      === IP/MPLS service
~~~
{: #Figure12 title="Policy based routing (PBR) label hand-off based for IETF Network Slice Realization"}

##  GTP Source Port-Based

   In some deployments of the 3GPP network slices, the IETF network
   slice INS1 might be realized by multiple GTP tunnels.  As shown in
   {{Figure13}}, this solution uses the source UDP port of the GTP tunnel
   to carry the identification of 3GPP network slice.  A mapping table
   between the 3GPP network slice and the source UDP port is needed in
   this solution and needs to be maintained by network functions CU, UPF
   and PE nodes.  Refer to section 2.5 of {{draft-ietf-dmm-tn-aware-mobility}} for details of this solution.

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
      *  SDP (N3 interfaces)
      === Realization of the INS1 using data plane GTP tunnels
~~~
{: #Figure13 title="GTP source port-based for IETF Network Slice Realization"}

## Consideration of the Virtual Network Functions (VNF)

   In some 3GPP network slice deployments, it might be beneficial to
   deploy RAN and Core network functions such as DU, CU, UPF etc as
   virtual network functions (VNF) inside a data center (DC).  As an
   example, consider {{Figure14}} where the CU and UPF have been deployed
   as VNF.  The definition of the IETF network slice INS1 is exactly
   similar to previous use-cases, i.e., INS1 is an IETF network slice to
   provides the connectivity between service demarcation points SDP1 and
   SDP2 to satisfy certain SLO/SLE.  However, the realization of INS1
   might be different from previous use-cases.  Figure 14 shows one
   possible solution for realization of INS1 where a portion of
   realization is inside provider's network and other portion is inside
   data centers.  As an example, L3VPN service technology could be used
   inside the provider network between provider edge routers PE1 and PE2
   and VXLAN could be used inside data centers towards PE1 and PE2.
   Note that the choice of technology during the realization is
   responsibility of IETF network slice controller (NCS) and is out of
   scope of this draft

~~~
         <-------------------- INS1 ------------------->

           Realization of INS1   Realization of INS1
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
      O   SDP (N3 interfaces)
      === Realization of INS1 in Provider Networks
      ... Realization of INS1 in data centers
~~~
{: #Figure14 title="VNF Consideration for IETF Network Slice Realization"}

# 3GPP Network Slice Mapping Parameters

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
   network slice.  The rules for the definition of network slice subnets
   and their composition into network slices are detailed in the 5G
   Network Resource Model (NRM) {{TS-28.541}}, specifically in the Network
   Slice NRM fragment.  This fragment captures the information model of
   5G network slicing, which specifies the relationships between
   different slicing related managed entities, which is represented as
   Information Object Class (IOC).  The IOC that have been defined
   including: NetworkSlice IOC, NetworkSliceSubnet IOC, ManagedFunction
   IOC and EP\_Transport IOC.

   Information Object Class EP\_Transport {{TS-28.541}} Clause 6.3.18
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
                   |  Model defined in IOC TS 28.541  |
                   |          NgU/N3 slices           |
                   +----+--------------------------+--+
      +-----------------|+                         |
      |   3GPP CU-UP /  ||                       +-|---------------+
      | ORAN O-CU-UP #1 ||        .-----.        | |3GPP (i)UPF #1 |
      | +---------------V|      ,'  TN   `.      +-V--------------+|
      | | EP\_NgU link to |     |  domain   |     | EP\_N3 link to  ||
      | |     UPF #1     |    ;             :    |    CU-UP #1    ||
      | |+---------------|    ;  .-------.  :    +---------------+||
      | ||EP\_Transport 10+------(Slice 10 )------|EP\_Transport 10|||
      | |+---------------|   |   `-------'   |   +---------------+||
      | |                |   |               |   |                ||
      | |+---------------|   :   .-------.   ;   +----------------||
      | ||EP\_Transport 20+------(Slice 20 )------|EP\_Transport 20 ||
      | |+---------------|A   :  `-------'  ;   A+----------------||
      | +----------------||    |           |    |+----------------+|
      |            . . . ||     |         |     || . . .           |
      | +----------------||      `.     ,'      |+----------------+|
      | | EP\_NgU link to ||        `---'        || EP\_NgU link to ||
      | |     UPF #N     ||                     ||   CU-UP #N     ||
      | +----------------||                     |+----------------+|
      +------------------+|                     |+-----------------+
                          |                     |
                   +------+---------------------+--------+
                   |    logical transport interfaces     |
                   |     e.g. GTP-U, IPSec endpoint      |
                   +-------------------------------------+
~~~
{: #Figure15 title="Slicing example realization between 3GPP subsystems and TN on the NgU/N3 interface"}

~~~
                    +----------------------------------+
                    |      Slices in 3GPP domain       |
                    |  Model defined in IOC TS 28.541  |
                    |            F1-U slices           |
                    +-+-------------------------+------+
       +--------------|+                       +|-----------------+
       |  3GPP DU /   ||                       ||  3GPP CU-UP /   |
       | ORAN O-DU #1 ||                       ||ORAN O-CU-UP #1  |
       |              ||        .-----.        ||                 |
       |+-------------V|      ,'  TN   `.      +V---------------+ |
       || EP\_F1-U link |     |  domain   |     |EP\_F1-U link to | |
       || to CU-UP #1  |    ;             :    |     DU #1      | |
       |+--------------|    ;   .-----.   :    +--------------+ | |
       ||EP\_Transport 1+-------(Slice 1)-------|EP\_Transport 1| | |
       |+--------------|   |    `-----'    |   +--------------+ | |
       ||              |   |               |   |                | |
       |+--------------|   :    .-----.    ;   +--------------+ | |
       ||EP\_Transport 2+-------(Slice 2)-------|EP\_Transport 2| | |
       |+--------------|A   :   `-----'   ;   A+--------------+ | |
       |+--------------||    |           |    |+----------------+ |
       |         . . . ||     |         |     || . . .            |
       |+--------------||      `.     ,'      |+----------------+ |
       || EP\_F1-U link ||        `---'        ||EP\_F1-U link to | |
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
{: #Figure16 title="Slicing example realization between 3GPP subsystems and TN on the F1-U interface"}


   For the transport (i.e., connectivity) related part of a network
   slice, the key focus is on the EP\_Transport I\_OC.  Instances of this
   IOC serves to instantiate 3GPP interfaces (e.g., N3) which are needed
   to support Network Slicing and to define Network Slice transport
   resources within the 5G NRM.  In a nutshell, the EP\_Transport IOC
   permits to define additional logical interfaces for each slice
   instance of the 3GPP user plane.

   According to {{TS-28.541}}, the EP\_Transport construct on 3GPP side has
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
   coherent Network Slice transport service.  {{Figure17}} illustrates how the
   EP\_Transport parameters can relate to the IETF ones for determining
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
  |||ipAddress = 20.2.2.2 |   |   `.     ,'
  ||+--------------A------|   |     `---'
  |+---------------|------| +-+-------------------+
  +----------------|------+ |   nextHopInfoList   |
                   |        |NextHopInfo = IP/mask|
    +--------------+------+ |       of PE 1       |
    | epApplicationRef =  | | system name = PE 1  |
    |EP_NgU link to UPF#1 | |  port name = Gi1/1  |
    +---------------------+ +---------------------+
~~~
{: #Figure17 title="Example of 3GPP EP\_Transport IOC TS28.541 parameters with correlation to IETF"} 

   Furthermore, that same parameters should be leveraged for
   constituting the connectivity construct allowing endpoint
   interconnection.  That is, there is no additional information that
   could be leveraged at service level that the one provided by
   EP\_Transport, which essentially reflects an endpoint view.  {{Figure18}}
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
{: #Figure18 title="Relationships of the 3GPP parameters with the IETF parameters"} 

   Leveraging on the EP\_Transport information, the IETF NSC should be
   instructed through its NBI on performing the slice connection.  {{Figure19}}
   graphically represents the slice connection (e.g., for Ng-U/N3) as
   expected by 3GPP by using connectivity constructs (of a IETF Network
   Slice service) to be configured by the IETF Network Slice Controller.
   
~~~
     Slices in 3GPP domain                         Slices in 3GPP domain
  Model defined in IOC TS 28.541          Model defined in IOC TS 28.541

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
|||  IP 10.1.1.2   |<--->|    | ;       : |    |<-->|  IP 10.1.1.2   |||
||+----------------|     |    |;         :|    |    +----------------+||
||+----------------|     |    ||         ||    |    +----------------+||
||| EP_Transport   |     |    ||         ||    |    |EP_Transport for|||
|||for S-NSSAI 200 o--------------PDU 2-------------o  S-NSSAI 200   |||
|||   Vlan 200     |     |    ||         ||    |    |    Vlan 200    |||
|||  IP 20.2.2.2   |<--->|    ||   TN    ||    |<-->|  IP 20.2.2.2   |||
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
{: #Figure19 title="Example of CU-UP Slice in the 3GPP domain using an IETF Network Slice service"} 

   From the perspective of IETF Network Slice realization, some of these
   options could be realized in a straightforward manner while other
   could require of advanced features (e.g., PBR, SRv6, FlexE, etc).
   IETF Network Slice service may be a set of techniques and underlaying
   technologies, so multiple models may be used to define slice.

   According to the {{TS-28.541}} attributes in the EP\_Transport, the IETF
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
{: #Figure19_1 title="Variations of Slice implementation options"} 

   From the perspective of IETF Network Slice realization, some of these
   options could be realized in a straightforward manner while other
   could require of advanced features (e.g., PBR, SRv6, FlexE, etc).

   IETF Network Slice service may be a set of techniques and underlaying
   technologies, so multiple models may be used to define slice.


# 5G E2E Network Slice Mapping Procedure

   This section provides a general procedure of network slice mapping:
   
~~~   
                  +-----------------+
                  |       NSMF      |
                  +-----------------+
       +----------|     S-NSSAI     |----------+
       |          |(e.g. 011111111) |          |
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
     |           |                   |           |     -----------------
     |           |                   |           |
     V           V                   V           V     -----------------
    / \      +-----+             +-----+    +-------+        Data
   /RAN\ ----|  PE |-----...-----| PE  |----|  CN   |        Plane
  /-----\    +-----+             +-----+    +-------+
~~~
{: #Figure20 title="Relation between IETF and 3GPP Network Slice management"} 

   1. 3GPP NSMF receives the request from 3GPP CSMF for allocation of a
   network slice instance with certain characteristics.

   2.  Based on the service requirement, 3GPP NSMF acquires requirements
   for the end-to-end network slice instance, which is defined in
   Service Profile ({{TS-28.541}} section 6.3.3).

   3.  Based on Service Profile, 3GPP NSMF identified the network
   function and the required resources in AN, CN and TN networks.  It
   also assigns the unique ID S-NSSAI.

   4. 3GPP NSMF sends a request to AN NSSMF for creation of AN Slice,
   out of the scope of this document.

   5. 3GPP NSMF sends a request to CN NSSMF for creation of CN Slice,
   out of the scope of this document.

   6. 3GPP NSMF sends a request to IETF Network Slice Controller (NSC)
   (acting as an NSSMF for transport connectivity, or TN NSSMF, from the
   perspective of the 3GPP Management System)) for creation of IETF
   Network Slice.  The request contains attributes such as endpoints
   (based on the information from EP\_Transport IOC), required SLA/SLO
   along with other IETF network slice attributes.  It also cotains
   mapping informatin for IETF Network Slice Interworking Identifier.

   Note: term "TN NSSMF" under discussion to ensure consistency with
   3GPP specifications.

   7.  IETF NSC realizes the IETF network slice which satisfies the
   requirements of the IETF network slice service requested between the
   specified endpoints (RAN/ CN edge nodes).  It may assign sliceID and
   send it to 3GPP NSMF.

   Note: Consistency with the YANG NBI model should be ensured on
   parameters being passed between components

   8. 3GPP NSMF mantains the mapping relationship between S-NSSAI and
   IETF Network Slice Service ID;

   9.  When the User Equipment (UE) appears, and during the 5G
   signaling, it requests to be connected to specific e2e network slice
   identified by S-NASSI.  Then a GTP tunnel (which is UDP/IP-based)
   will be created.

   10.  UE starts sending traffic in context of e2e network slice for
   specific S-NASSI.

   11.  The endpoints of the 5G network slice in AN encapsulates the
   packet into a GTP tunnel, adds a Slice Interworking Identifier
   according to the selected S-NSSAI and send it to the transport
   network.

   12.  The transport network edge nodes parse the Slice Interworking
   identifier in the received packet and maps the packet to the
   corresponding IETF network slice.  It may encapsulate the packet with
   slice specific identifiers for enforcing the SLA of IETF Network
   Slice service in the in transport network.

   Note: steps 11 and 12 under discussion since they could depend on
   specific realization mechanisms.
##  5G E2E Network Slice Mapping in Management Plane

   The transport network management Plane maintains the interface
   between 3GPP NSMF and TN NSSMF, which 1) guarantees that IETF network
   slice could connect the AN and CN with specified characteristics that
   satisfy the requirements of communication; 2) builds up the mapping
   relationship between NSI identifier and any other identifier
   potentially used by the IETF NSC; 3) maintains the end-to-end slice
   relevant functions.

   Service Profile defined in {{TS-28.541}} represents the requirement of
   end-to-end network slice instance in 5G network.  Parameters defined
   in Service Profile include Latency, resource sharing level,
   availability and so on.  How to decompose the end-to-end requirement
   to the transport network requirement is one of the key issues in
   Network slice requirement mapping.  GSMA (Global System for Mobile
   Communications Association) defines the {{GST}} to indicate the network
   slice requirement from the view of service provider.
   {{!I-D.ietf-teas-ietf-network-slice-use-cases}} analyzes the parameters
   of GST and categorize the parameters into three classes, including
   the attributes with direct impact on the IETF network slice
   definition.  It is a good start for selecting the transport network
   relevant parameters in order to define Network Slice Profile for
   Transport Network.  Network slice requirement parameters are also
   necessary for the definition of transport network northbound
   interface.

   Inside the IETF NSC (playing the role of TN NSSMF in 3GPP scope), it
   is supposed to be responsible of maintaining the attributes of the
   IETF network slice.  If the attributes of an existing IETF Network
   Slice service could satisfy the requirement from the 3GPP Network
   Slice Profile, an existing IETF network slice could be selected and
   the mapping is then finished.  In case there is no existing IETF
   Network Slice which could satisfy the requirement, a new IETF Network
   Slice is supposed to be created by the IETF NSC with the requested
   attributes.

   IETF Network Slice resource reservation should be considered to avoid
   over allocation from multiple requests from 3GPP NSMF (but the
   detailed mechanism is out of scope of this draft)

   3GPP TN NSSMF will request the IETF Network Slice service adding in
   the IETF Network Slice service request some slice identifier to the
   IETF NSC.  The mapping relationship between NSI identifier and IETF
   Network Slice service identifier could be maintained in both 3GPP
   NSMF and IETF NSC.
   Then, at the time of provisioning a 3GPP slice, it is required to
   provide slice connectivity constructs by means of IETF network
   slices.  Then it is necessary to bind two different endpoints, as
   depicted in Figure 2:

   *  Mapping of EP\_Transport (as defined by {{TS-28.541}}) to the endpoint
      at the CE side o f the IETF network slice.  This is necessary
      because the IETF Network Slice Controller (NSC) will receive as
      input for the IETF network slice service the set of endpoints at
      CE side to be interconnected

   *  Mapping of the endpoints at both CE and PE side.  The endpoint at
      PE side should be elicited by some means by the IETF NSC, in order
      to establish and set up the connectivity construct intended for
      the customer slice request, according to the SLOs and SLEs
      received from the higher level system.

~~~
        3GPP concern

        -----------                                            ---------
                 /                                            /
                /                                            /
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
{: #Figure21 title="conceptual view on 3GPP and TN connectivity meeting points"} 
###  Mapping EP\_transport to IETF NS CE endpoints
   The 3GPP Management system provides the EP\_Transport IOC to extend
   the slice awareness to the transport network.  The EP\_Transport IOC
   contains parameters as IP address, additional identifiers (i.e., vlan
   tag, MPLS label, etc), and associated QoS profile.  This IOC is
   related to the endpoints of the 3GPP managed functions (detailed in
   the EP\_Application IOC).

   The information captured in the EP\_Transport IOC (as part of the 3GPP
   concern) should be translated into the CE related parameters (as part
   of the IETF concern).  There will be cases where such translation is
   straightforward, as for instance, when the 3GPP managed functions run
   on monolithic, purpose-specific network elements, in the way that
   the IP address attribute from the EP\_Transport IOC directly
   corresponds to the IP address of an interface of such network
   element.  In this case, the information on EP\_Transport IOC can be
   directly passed to the IETF NSC through the NBI, even though some
   additional information could be yet required, not being defined yet
   on 3GPP specifications (e.g., the mask applicable to the IP address
   field on EP\_Transport).  Note that information gaps are further
   detailed in a summary section at the end of this document.

   However, there could be other cases where such a relationship is not
   straightforward.  This could be the case of virtualized 3GPP managed
   functions that could be instantiated on a general-purpose bare-metal
   server or in a data center.  In these other cases it is necessary to
   define additional means for eliciting the endpoint at the CE side
   corresponding to the endpoint of the 3GPP-related function.

   With solely EP\_Transport characterization in 3GPP as today (i.e.,
   according to 3GPP Release 16 specifications), we could expect the NS
   CE endpoint being identified by a combination of IP address and some
   additional information such as vlan tag, MPLS label or SR SID that
   could discriminate against a certain logical interface.  The next hop
   router information is related to the next hop view from the
   perspective of the 3GPP entity part of the slice, then providing
   hints for determining the slice endpoint at the other side of the
   slice boundary.  Finally, the QoS profile, if present, helps to
   determine configurations needed at the PE side to respect the SLOs in
   the connection between CEs slice endpoints.
###  Mapping IETF NS CE to PE endpoints
   As described in {{!I-D.ietf-teas-ietf-network-slices}}, there are
   different potential endpoint positions for an IETF NS.
   
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
~~~
{: #Figure22 title="IETF Network Slice endpoints"}  

   The information that is passed to the IETF NSC in terms of endpoints
   is the information relative to the CE side, which is the one known by
   the slice customer (i.e., the 3GPP Management system, that
   corresponds to the 3GPP managed functions).  From that information,
   the IETF NSC needs to infer the corresponding endpoint at the PE
   side, in order to setup the desired connectivity constructs with the
   SLOs indicated in the request.

   Being the IETF slice request a technology-agnostic procedure, the
   identification of the slice endpoints at the PE side should leverage
   on generic information passed through the NBI to the IETF NSC.

##  5G E2E Network Slice Mapping in Control Plane

   There is no explicit interaction between transport network and AN/CN
   in the control plane, but the S-NSSAI defined in {{TS-23.501}} is treated
   as the end-to-end network slice identifier in the control plane of AN
   and CN, which is used in UE registration and PDU session setup.  In
   this draft, it is assumed that there is a correspondence between
   S-NSSAI and the IETF Network Slice service identifier in the
   management plane.

   Note: to ensure consistency with NBI YANG model (i.e., service tag)
##  5G E2E Network Slice Mapping in Data Plane

   If multiple network slices are carried through one physical interface
   between AN/CN and TN, IETF Network Slice Interworking ID in the data
   plane needs to be defined.  If different network slices are
   transported through different physical interfaces, Network Slices
   could be distinguished by the interface directly.  Thus IETF Network
   Slice Interworking ID is not the only option for network slice
   mapping, while it may help in introducing new network slices.

###  Data Plane Mapping Considerations

   The mapping relationship between AN or CN network slice and an IETF
   Network Slice will be based on a IETF Network Slice Interworking
   identifier based on the information provided by the EP\_Transport IOC.
   When the packet of an uplink flow goes from AN to TN, the packet is
   delivered according to the information provided by the EP\_Transport
   IOC (e.g., the information provided in the logicalInterface field);
   then the encapsulation is read by the edge node of transport network,
   which maps the packet to the corresponding IETF network slice.

###  Data Plane Mapping Options

   The following picture shows the end-to-end network slice in data
   plane:
   
~~~
   +--+       +-----+                           +----------------+
   |UE|- - - -|(R)AN|---------------------------|       UPF      |
   +--+       +-----+                           +----------------+
    |<----AN NS---->|<----------TN NS---------->|<----CN NS----->|
~~~
{: #Figure23 title="The mapping between 3GPP slice and transport slice"}  

   The mapping between 3GPP slice and transport slice in user plane
   could happens in:

   (R)AN: User data goes from (radio) access network to transport
   network

   UPF: User data goes from core network functions to transport network

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

####  Layer 3 and Layer 2 Encapsulations

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
   The following field in IP header and Ethernet header could be
   considered :

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

   The following field could be considered to identify a network slice:
      SRH:

   *  SRv6 functions: AN/CN is supposed to support the new function
      extension of SRv6.

   *  Optional TLV: AN/CN is supposed to support the extension of
      optional TLV of SRH.

####  Above Layer 3 Encapsulations

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

   The following field in UDP header could be considered:

   UDP Header:

   *  UDP Source port: The UDP source port is sometimes used for load
      balancing.  Using it for network slice mapping would require to
      disable the load-balancing behavior.

   A similar approach to this is followed in
   {{!I-D.ietf-dmm-tn-aware-mobility}}

####  Summary

   From all the options overviewed, it should be noted that current 3GPP
   Release 16 only supports through EP\_Transport IOC the following slice
   handoff identifier: vlan tag.  MPLS or SID labels.  Thus, the
   consideration of more options as the ones here reported is a gap on
   3GPP specifications.


# Example of IETF Network Slice request through IETF Network Slice NBI

   As discussed in {{!I-D.ietf-teas-ietf-network-slices}}, to fulfill IETF
   network slices and to perform monitoring on them, an entity called
   IETF Network Slice Controller (NSC) is required to take abstract
   requests for IETF network slices and realize them using suitable
   underlying technologies.  An IETF Network Slice Controller is the key
   building block for control and management of the IETF network slice.
   It provides the creation/modification/deletion, monitoring and
   optimization of transport Slices in a multi-domain, a multi-
   technology and multi-vendor environment.

   {{Figure24}} shows the NSC and its NBI interface for 5G.  Draft
   {{!I-D.ietf-teas-ietf-network-slice-nbi-yang}} a addresses the service
   yang model of the NSC NBI interface for all network slicing use-
   cases.
   
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
                                     | NSC NBI
                                     V
                  +------------------------------------------+
                  |    IETF Network Slice Controller (NSC)   |
                  +------------------------------------------+
                                     A
                                     | NSC SBI
                                     V
                  +------------------------------------------+
                  |          Network Controller(s)           |
                  +------------------------------------------+
~~~
{: #Figure24 title="IETF Network Slice Controller NBI for 5G"}  

   As discussed in {{!I-D.ietf-teas-ietf-network-slices}}, the main task of
   the IETF Network Slice Controller is to map abstract IETF network
   slice requirements from NBI to concrete technologies on SBI and
   establish the required connectivity, and ensure that required
   resources are allocated to IETF network slice.  There are a number of
   different technologies that can be used on SBI including physical
   connections, MPLS, TSN, Flex-E, PON etc.  If the undelay technology
   is IP/MPLS/Optics, any IETF models can be used during the realization
   of IETF network slice.

   There are no specific mapping requirements for 5G.  The only
   difference is that in case of 5G, the NBI interface contains
   additional 5G specific attributes such as customer name, mobile
   service type, 5G E2E network slice ID (i.e.  S-NSSAI) and so on (See
   Section 6).  These 5G specific attributes can be employed by IETF
   Network Slice Controller during the realization of 5G IETF network
   slices on how to map NBI to SBI.  They can also be used for assurance
   of 5G IETF network slices.  Figure 9 shows the mapping between NBI to
   SBI for 5G IETF network slices.
   
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
     Figure 9: Relationship between transport slice interface and IETF
                     Service/Tunnels/Path data models
#  Gap Analysis

   The way in which 3GPP is characterizing the slice endpoint (i.e.,
   EP\_Transport) is based on Layer 3 information (e.g., the IP Address).
   However the information provided seems not to be sufficient for
   instructing the IETF Network Slice Controller for the realization of
   the IETF NEtwork Slice.  For instance, some basic information such as
   the mask associated to the IP address of the EP\_Transport is not
   specified, as well as other kind of parameters like the connection
   MTU or the connectivity type (unicast, multicast, etc).  More
   sophisticated information could be required as well, like the level
   of isolation or protection necessary for the intended slice.

   In the case in which the 3GPP managed function runs on a purpose-
   specific network element, the IP address specified in the
   EP\_Transport IOC serves as reference to identify the CE endpoint,
   assuming the endpoint of the CE has been configured with that IP
   address.  With that information (together with the logical interface
   ID) should be sufficient for the IETF NSC to identify the counterpart
   endpoint at the PE side, and configuring it accordingly (e.g., with a
   compatible IP address) for setting up the slice end-to-end.
   Similarly, the next hop information in EP\_Transport can help validate
   the end-to-end slice between PE endpoints.

   In the case in which the 3GPP managed function is instantiated as a
   virtualized network function, the direct association between the IP
   address of EP\_Transport and the actual endpoint mapped at the CE is
   not so clear.  It could be the case, for instance when the
   virtualized network function is instantiated at the internal of a
   data center, that the CE facing the PE is far from the point where
   the function is deployed, being that connectivity extended through
   the internals of the data center (or by some internal configuration
   of a virtual switch in a server).  In these situations additional
   information is needed for accomplishing the end-to-end connection.

   At the same time, {{TS-28.541}} IOC contains useful parameters to be
   used in IETF Network Slice creation mechanism and enreaching IETF
   Network Slice model.  The following parameters may be suggested as a
   candidates to the correlation of the IETF Network Slice parameters
   and IETF Network Slice model enreachments:

   *  For the latency, dLThptPerSliceSubnet, uLThptPerSliceSubnet,
      reliability and delayTolerance attributes, the following NRM apply
      (with reference to the section in that specification):

      -  CNSliceSubnetProfile (section 6.3.22 in {{TS-28.541}})

      -  RANSliceSubnetProfile (section 6.3.23 in {{TS-28.541}})
      -  TopSliceSubnetProfile (section 6.3.24 in {{TS-28.541}})

   *  For the qosProfile attribute, the NRM which applies is
      EP\_Transport (detailed in section 6.3.17 in {{TS-28.541}})

# IANA Considerations

   This document makes no request of IANA.

   Note to RFC Editor: this section may be removed on publication as an
   RFC.
   
# Security Considerations

# Acknowledgments


The work of Luis M.  Contreras has been partially funded by the
European Commission under Horizon 2020 project Int5Gent (grant
agreement 957403.

Thanks to Philip Eardley (philip.eardley@bt.com) for his contribution
to this document.


