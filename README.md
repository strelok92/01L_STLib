# 01L_STLib
This project is realises stx etx protocol with  with following format of package:
========================================================================
|| ENQ | ACK(NAK) | STX | data | ETX | LRC | CR | LF | ACK(NAK) | EOT ||
========================================================================

Codes:
STX - 0x02
ETX - 0x03
EOT - 0x04
ENQ - 0x05
ACK - 0x06
LF - 0x0A
CR - 0x0D
NAK - 0x15
LRC - LRC checksum, 1 byte
data - data for send-receive. Some bytes(Limit 1024 bytes).

Following section describes the protocol of exchanges of data.
SUCCESS EXCHANGE:
Device 1          Device 2
--------------------------
  ENQ       -> 
            <-     ACK
--------------------------           
  STX       -> 
  data      -> 
  ETX       -> 
  LRC       -> 
  CR        -> 
  LF        -> 
            <-     ACK
--------------------------           
  EOT       -> 
--------------------------

ERROR HANDSHAKE:
Device 1          Device 2
--------------------------
  ENQ       -> 
            <-     NAK
--------------------------

ERROR DATA:
--------------------------
  ENQ       -> 
            <-     ACK
--------------------------           
  STX       -> 
  data      -> 
  ETX       -> 
  LRC       -> 
  CR        -> 
  LF        -> 
            <-     NAK
--------------------------  

TIMEOUT:
Device 1          Device 2
--------------------------
  ENQ       -> 
--------------------------
