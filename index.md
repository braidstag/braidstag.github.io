## BraidsTag

An open source lasertag game featuring network connected guns enabling advanced gameplay fetures.

### Design considerations

While the networked nature of the guns is a significant feature, this is fundamentally unreliable in a field and so enough data for basic functioning must be transmitted in the IR "shot". A system for resolving any problems from guns being out of contact exists and we will test and monitor the state of the mesh to reduce the incidents of this.

### Hardware

The guns use an arduino for the realtime control of the IR led and reciever (and some auxiliary hardware like a torch). The main processing is done on a Raspberry Pi (probably a zero-w) connected by serial link.

We might include a screen on the gun controlled by the arduino but cost is a factor.

We might include a bluetooth headset for both audible gun feedback and comms (using mumble protocol or similar).

#### Mesh Network
We use a [batman-adv mesh](https://www.open-mesh.org/projects/batman-adv/wiki) to network the guns and if needed can deploy repeater nodes for the cost of just a pi zero-w and battery.

### Software
#### Arduino
Written in C using the arduino IDE, this is deployed directly to the arduino but will form part of the client release package and be deployed from the Pi to the arduino.

#### Pi
Written in Python, there is a client and server with some shared components. QT is used for the management UI on the server.

## Deployment
Deployment will be using multi-container support on resin.io. There will be a client application which includes the Pi client and the arduino firmware and a server application which contains the server app and some networking infrastructure (dhcp server and name resolution from DNS or Avahi)
