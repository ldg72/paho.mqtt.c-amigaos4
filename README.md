# Paho MQTT C Client for AmigaOS 4

This is a port of the Eclipse Paho MQTT C Client library to AmigaOS 4.

## Prerequisites

-   AmigaOS 4.1 or later
-   SDK with `ppc-amigaos-gcc`
-   `newlib` (standard C library)
-   `pthreads` (usually available in the SDK/newlib)

## Building

To build the library and the sample application, run:

```bash
make -f Makefile.amigaos4
```

This will create:
-   `build/amigaos4/libpaho-mqtt3c.a`: The static library.
-   `build/amigaos4/MQTTClient_publish`: A sample application.

## Changes

The following files have been modified or added for the AmigaOS 4 port:

### New Files
-   `Makefile.amigaos4`: Build script for AmigaOS 4.
-   `README.md`: This documentation file.

### Modified Files
-   `src/Socket.c`: Added AmigaOS specific headers and network definitions.
-   `src/Thread.c`: Implemented semaphores using pthreads for AmigaOS 4.
-   `src/Thread.h`: Added `sem_struct` definition for AmigaOS 4.
-   `src/WebSocket.c`: Added Big Endian handling for AmigaOS 4 (PPC).
-   `src/SHA1.c`: Added Big Endian handling for AmigaOS 4 (PPC).
-   `src/MQTTPacket.h`: Defined `REVERSED` for Big Endian bitfields on AmigaOS 4.

## Installation

To install the library and headers into your SDK (assuming `SDK:` is your SDK assignment):

1.  Copy the library:
    ```bash
    copy build/amigaos4/libpaho-mqtt3c.a SDK:local/newlib/lib/
    ```
2.  Copy the headers:
    ```bash
    makedir SDK:local/newlib/include/MQTTClient
    copy src/MQTTClient.h SDK:local/newlib/include/MQTTClient/
    copy src/MQTTAsync.h SDK:local/newlib/include/MQTTClient/
    copy src/MQTTClientPersistence.h SDK:local/newlib/include/MQTTClient/
    copy src/MQTTProperties.h SDK:local/newlib/include/MQTTClient/
    copy src/MQTTReasonCodes.h SDK:local/newlib/include/MQTTClient/
    copy src/MQTTSubscribeOpts.h SDK:local/newlib/include/MQTTClient/
    ```

## License

This project is licensed under the Eclipse Public License 2.0 and Eclipse Distribution License 1.0. See the [LICENSE](LICENSE) file for details.

## Usage

Link your application with `-Lbuild/amigaos4 -lpaho-mqtt3c -lpthread`.

