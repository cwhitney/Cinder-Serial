
# Cinder-Serial
Cross-platform serial communication CinderBlock thinly wrapping the [serial](https://github.com/wjwwood/serial) library.

### USAGE
```C++
// dump all serial ports
for (auto port : SerialPort::getPorts()) {
    console() << port->getName() << endl;
    console() << "descr: " << port->getDescription() << endl;
    console() << "ident: " << port->getHardwareIdentifier() << endl;
}

// find a port
auto port = SerialPort::findPortByNameMatching(std::regex("\\/dev\\/cu\\.usbmodem.*"));

// create a device
auto device = SerialDevice::create(port, 115200);

// read
uint8_t inBuffer[16];
while (device->getNumBytesAvailable() > 0) {
    size_t size = device->readBytes(inBuffer, 16);
}

// write
uint8_t outBuffer[5] = {
    0, 255, 255, // cyan RGB
    '\r', '\n', // EOL
};
device->writeBytes(outBuffer, 5);
```

[SLIP](https://en.m.wikipedia.org/wiki/Serial_Line_Internet_Protocol) and [COBS](https://en.m.wikipedia.org/wiki/Consistent_Overhead_Byte_Stuffing) encode / decode is available separately via the [Cinder-Encoding](https://github.com/pizthewiz/Cinder-Encoding) CinderBlock.

### GREETZ
- [William Woodall](https://github.com/wjwwood) and [John Harrison](https://github.com/ashgti) for _the_ [serial](https://github.com/wjwwood/serial) library
- [Christopher Baker](https://github.com/bakercp) and his [ofxSerial](https://github.com/bakercp/ofxSerial) [openFrameworks](https://github.com/openframeworks/openframeworks) addon
