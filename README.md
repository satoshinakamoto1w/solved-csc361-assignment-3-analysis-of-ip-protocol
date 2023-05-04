Download Link: https://assignmentchef.com/product/solved-csc361-assignment-3-analysis-of-ip-protocol
<br>
The purpose of this assignment is to learn about the IP protocol. You are required to write a 8 python program to analyze a trace of IP datagrams.

Introduction

10 In this assignment, we will investigate the IP protocol, focusing on the IP datagram. Well do so 11 by analyzing a trace of IP datagrams sent and received by an execution of the <em>traceroute </em>program. 12 We will investigate the various fields in the IP datagram, and study IP fragmentation in detail.

13 A background of the <em>traceroute </em>program is summarized as follows. The <em>traceroute </em>program 14 operates by first sending one or more datagrams with the time-to-live (TTL) field in the IP header 15 set to 1; it then sends a series of one or more datagrams towards the same destination with a TTL 16 value of 2; it then sends a series of datagrams towards the same destination with a TTL value of 3; 17 and so on. Recall that a router must decrement the TTL in each received datagram by 1 (actually, 18 RFC 791 says that the router must decrement the TTL by at least one). If the TTL reaches 0, the 19 router returns an ICMP message (type 11 TTL-exceeded) to the sending host. As a result of this 20 behavior, a datagram with a TTL of 1 (sent by the host executing traceroute) will cause the router 21 one hop away from the sender to send an ICMP TTL-exceeded message back to the sender; the 22 datagram sent with a TTL of 2 will cause the router two hops away to send an ICMP message back 23 to the sender; the datagram sent with a TTL of 3 will cause the router three hops away to send an 24 ICMP message back to the sender; and so on. In this manner, the host executing <em>traceroute </em>can 25 learn the identities of the routers between itself and a chosen destination by looking at the source 26 IP addresses in the datagrams containing the ICMP TTL-exceeded messages. You will be provided 27 with a trace file created by <em>traceroute</em>.

28 Of course, you can create a trace file by yourself. Note that when you create the trace file, 29 you need to use different datagram sizes (e.g., 2500 bytes) so that the captured trace file includes 30 information on fragmentation.

<h1>31 3         Requirements</h1>

32         There are two requirements for this assignment:

<h2>33 3.1           Requirement 1 (R1)</h2>

34 You are required to write a python program to analyze the trace of IP datagrams created by 35 <em>traceroute</em>. To make terminologies consistent, in this assignment we call the <em>source node </em>as the 36 computer that executes <em>traceroute</em>. The <em>ultimate destination node </em>refers to the host that is the 37 ultimate destination defined when running <em>traceroute</em>. For example, the ultimate destination node 38 is “mit.edu” when you run

<h3>39 %traceroute mit.edu 2000</h3>

40 In addition, an <em>intermediate destination node </em>refers to the router that is not the ultimate destination 41 node but sends back a ICMP message to the source node.

42 As another example, you can set “don’t fragment”’ bit and set the number of probes per “ttl” 43 to 5 queries using the following command:

<h3>44 %traceroute -F -q 5 mit.edu 200</h3>

<ul>

 <li>Your program needs to output the following information:</li>

 <li>List the IP address of the source node, the IP address of ultimate destination node, the IP 47 address(es) of the intermediate destination node(s). If multiple intermediate destination nodes 48 exist, they should be ordered by their hop count to the source node in the increasing order.</li>

</ul>

49 • Check the IP header of all datagrams in the trace file, and list the set of values in the <em>protocol </em>50 field of the IP headers. Note that only different values should be listed in a set.

51 • How many fragments were created from the original datagram? Note that 0 means no frag52 mentation. Print out the offset (in terms of bytes) of the last fragment of the fragmented IP 53 datagram. Note that if the datagram is not fragmented, the offset is 0.

54 • Calculate the average and standard deviation of round trip time (RTT) between the source 55 node and the intermediate destination node (s) and the average round trip time between 56 the source node and the ultimate destination node. The average and standard deviation are 57 calculated over all fragments sent/received between the source nodes and the (intermediate/ 58 ultimate) destination node.

59                        The output format is as follows: (Note that the values do not correspond to any trace file).

<h3>60 The IP address of the source node: 192.168.1.12</h3>

61 The IP address of ultimate destination node: 12.216.216.2 62 The IP addresses of the intermediate destination nodes:

<h3>63                                            router 1: 24.218.01.102,</h3>

64                   router 2: 24.221.10.103, 65           router 3: 12.216.118.1.

66

67 The values in the protocol field of IP headers:

<h3>68                   1: ICMP 69                 17: UDP</h3>

70

71

<ul>

 <li>The number of fragments created from the original datagram is: 3</li>

 <li>The offset of the last fragment is: 3680</li>

</ul>

74

75 The avg RTT between 192.168.1.12 and 24.218.01.102 is: 50 ms, the s.d. is: 5 ms 76 The avg RTT between 192.168.1.12 and 24.221.10.103 is: 100 ms, the s.d. is: 6 ms 77 The avg RTT between 192.168.1.12 and 12.216.118.1 is: 150 ms, the s.d. is: 5 ms 78 The avg RTT between 192.168.1.12 and 12.216.216.2 is: 200 ms, the s.d. is: 15 ms

79

<h2>80 3.2           Requirement 2 (R2)</h2>

81 <strong>Note: You can finish this part either with a python program or by manually col</strong>82 <strong>lecting/analyzing data. In other words, coding is optional for the tasks listed in this</strong>

<ul>

 <li></li>

 <li>From a given set of five <em>traceroute </em>trace files, all with the same destination address,</li>

 <li>determine the number of probes per “ttl” used in each trace file,</li>

 <li>determine whether or not the sequence of intermediate routers is the same in different trace</li>

 <li>files,</li>

 <li>if the sequence of intermediate routers is different in the five trace files, list the difference and</li>

 <li>explain why,</li>

 <li>if the sequence of intermediate routers is the same in the five trace files, draw a table as shown 91 below (<strong>warning: </strong>the values in the table do not correspond to any trace files) to compare 92 the RTTs of different traceroute attempts. From the result, which hop is likely to incur the 93 maximum delay? Explain your conclusion.</li>

</ul>

<table width="593">

 <tbody>

  <tr>

   <td width="56">TTL</td>

   <td width="109">Average RTT</td>

   <td width="109">Average RTT</td>

   <td width="109">Average RTT</td>

   <td width="109">Average RTT</td>

   <td width="101">Average RTT</td>

  </tr>

  <tr>

   <td width="56"></td>

   <td width="109">in trace 1</td>

   <td width="109">in trace 2</td>

   <td width="109">in trace 3</td>

   <td width="109">in trace 4</td>

   <td width="101">in trace 5</td>

  </tr>

  <tr>

   <td width="56">1</td>

   <td width="109">0.5</td>

   <td width="109">0.7</td>

   <td width="109">0.8</td>

   <td width="109">0.7</td>

   <td width="101">0.9</td>

  </tr>

  <tr>

   <td width="56">2</td>

   <td width="109">0.9</td>

   <td width="109">1</td>

   <td width="109">1.2</td>

   <td width="109">1.2</td>

   <td width="101">1.3</td>

  </tr>

  <tr>

   <td width="56">3</td>

   <td width="109">1.5</td>

   <td width="109">1.5</td>

   <td width="109">1.5</td>

   <td width="109">1.5</td>

   <td width="101">2.5</td>

  </tr>

  <tr>

   <td width="56">4</td>

   <td width="109">2.5</td>

   <td width="109">2</td>

   <td width="109">2</td>

   <td width="109">2.5</td>

   <td width="101">3</td>

  </tr>

  <tr>

   <td width="56">5</td>

   <td width="109">3</td>

   <td width="109">2.5</td>

   <td width="109">3</td>

   <td width="109">3.5</td>

   <td width="101">3.5</td>

  </tr>

  <tr>

   <td width="56">6</td>

   <td width="109">5</td>

   <td width="109">4</td>

   <td width="109">5</td>

   <td width="109">4.5</td>

   <td width="101">4</td>

  </tr>

 </tbody>

</table>

94

<h1>95 4         Miscellaneous</h1>

<ul>

 <li><strong>Important! Please read!</strong></li>

 <li>Same as in Assignment 2, you are not allowed in this assignment to use python packages that</li>

 <li>can automatically extract each packet from the pcap files. That means, you can re-use your 99 code in Assignment 2 to extract packets.</li>

</ul>

100 • Some intermediate router may only send back one “ICMP TTL exceeded” message for multiple 101 fragments of the same datagram. In this case, please use this ICMP message to calculate RTT 102 for all fragments. For example, Assume that the source sends Frag 1, Frag2, Frag 3 (of the 103 same datagram, ID: 3000). The timestamps for Frag1, Frag2, Frag3 are <em>t</em><sub>1</sub><em>,t</em><sub>2</sub><em>,t</em><sub>3</sub>, respectively. 104             Later, the source receives one “ICMP TTL exceeded” message (ID: 3000). The timestamp is 105            <em>T</em>. Then the RTTs are calculated as: <em>T </em>− <em>t</em><sub>1</sub>, <em>T </em>− <em>t</em><sub>2</sub>, <em>T </em>− <em>t</em><sub>3</sub>.

<ul>

 <li>More explanation about the output format</li>

 <li>The number of fragments created from the original datagram is:</li>

</ul>

108

<ul>

 <li>The offset of the last fragment is:</li>

 <li>If there are multiple fragmented datagrams, you need to output the above information for</li>

 <li>each datagram. For example, assume that the source sends two datagrams: <em>D</em><sub>1</sub>, <em>D</em><sub>2</sub>, where 112 <em>D</em><sub>1 </sub>and <em>D</em><sub>2 </sub>are the identification of the two datagrams. Assume that <em>D</em><sub>1 </sub>has three fragments 113 and <em>D</em><sub>2 </sub>has two fragments. Then output should be:</li>

</ul>

<h2>114                                                    The number of fragments created from the original datagram D1 is: 3</h2>

115

116                                                The offset of the last fragment is: xxx.

117

118

<h2>119                                                    The number of fragments created from the original datagram D2 is: 2</h2>

120

121                                                The offset of the last fragment is: yyy.

122

<ul>

 <li>where <em>xxx </em>and <em>yyy </em>denote the actual number calculated by your program.</li>

 <li>If the tracefile is captured in Linux, the source port number included in the original UDP 125 can be used to match against the ICMP error message. This is due to the special traceroute 126 implementation in linux, which uses UDP and ICMP. If the tracefile is captured in Windows, 127 we should use the sequence number in the returned ICMP error message to match the sequence 128 number in the ICMP echo (ping) message from the source node. Note that this ICMP error 129 message (type 11) includes the content of the ICMP echo message (type 8) from the source. 130 This is due to the special traceroute implementation in Windows, which uses ICMP only 131 (mainly message type 8 and message type 11). It is also possible that traceroute may be 132 implemented in another different way. For instance, we have found that some traceroute 133 implementation allows users to select protocol among ICMP, TCP, UDP and GRE. To avoid 134 the unnecessary complexity of your program, <strong>you only need to handle the two scenarios </strong>135 <strong>in finding a match between the original datagram and the returned ICMP error </strong>136 <strong>message: either (1) use the source port number in the original UDP, or (2) use the </strong>137 <strong>sequence number in the original ICMP echo message. </strong>You code should <strong>automatically </strong>138 find out the right case for matching datagrams in the trace file. We will not test your code 139 with a trace file not falling in the above cases.</li>

</ul>