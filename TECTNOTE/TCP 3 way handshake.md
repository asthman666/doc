## TRANSMISSION CONTROL PROTOCOL

The procedures to establish connections utilize the synchronize (SYN) control flag and involves an exchange of three messages.  This exchange has been termed a three-way hand shake.

A three way handshake is necessary because sequence numbers are not tied to a global clock in the network, and TCPs may have different mechanisms for picking the ISN's.

The principle reason for the three-way handshake is to prevent old duplicate connection initiations from causing confusion. 

The simplest three-way handshake is shown below:

    TCP A                                                    TCP B

    1.  CLOSED                                               LISTEN

    2.  SYN-SENT    --> <SEQ=100><CTL=SYN>                --> SYN-RECEIVED

    3.  ESTABLISHED <-- <SEQ=300><ACK=101><CTL=SYN,ACK>   <-- SYN-RECEIVED

    4.  ESTABLISHED --> <SEQ=101><ACK=301><CTL=ACK>       --> ESTABLISHED

    5.  ESTABLISHED --> <SEQ=101><ACK=301><CTL=ACK><DATA> --> ESTABLISHED


> [rfc793](https://www.ietf.org/rfc/rfc793.txt)
