## Distributed Simplex Downlink Protocol (DSDP)

`dsdp` ("dee ess dee pee") is a platform agnostic downlink protocol designed to allow satellites with simple radio hardware to effectively downlink data via other nearby satellites and their associated groundstations

## Design goals

1. Very low hardware requirements to participate. Simplex radios using UHF with embedded C&DH computers (low RAM, moderately small storage) should be able to use this protocol
2. Efficient; The throughput of the network of associated satellites and their groundstations should be higher than the sum of individual throughputs
3. Reliable; Users are assured that the data that was put into the network is the same data that comes out on the other side
4. Encrypted in flight; all datagrams containing science data will be encrypted using strong encryption so that only the teams flying the hardware will be able to extract the data,
5. Cooperative; users in the constellation will only be able to downlink as much as they downlink for others, when bandwidth is at a premium
6. Platform agnostic; this protocol should work as well on an AVR microcontroller as it would on a Linux SOM. Protocol will not require the C standard library
7. Compliant; Implementation of the protocol will conform to the necessary regulatory bodies so that it can be used in the real world

## Ideas

- Caching of handshakes regarding available storage and downlink capabilities so those only have to be updated every so often
    - maybe keep a CRC of the peer's settings, so that if they're different you can do an additional settings request
    - peer will advertise this CRC in their downlink request advertisement
- ChaCha20 encryption
- Same protocol works in duplex
    - downlink data is different than transmit message? protocl negotiation in simplex before switching to duplex for downlink?
    - table this till the simplex protocol works
- Abstract away frequency hopping? Allocate a band of frequencies just for this protocol?
- compare vs torrenting
- encryption is optional; transfer only cares about blocks of data not their contents
- dynamic block size? Advertise which sizes you support?
- forward error correction is Reed-Solomon

## Testing

- simulate satellites downlinkin only on their passes vs being in the network
- simulate random interactions between satellites and other nodes
- compare to torrent network
