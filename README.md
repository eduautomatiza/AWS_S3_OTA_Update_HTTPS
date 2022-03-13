## AWS S3 OTA Update HTTPS para ESP32
Inspirado em:
[AWS_S3_OTA_Update](https://github.com/espressif/arduino-esp32/blob/master/libraries/Update/examples/AWS_S3_OTA_Update/AWS_S3_OTA_Update.ino) e em
[httpUpdateSecure](https://github.com/espressif/arduino-esp32/blob/master/libraries/HTTPUpdate/examples/httpUpdateSecure/httpUpdateSecure.ino)

### Propósito
Executar uma atualização OTA no ESP32 de um arquivo localizado no Amazon S3 usando HTTPS

### Preparando o arquivo na Amazon S3
1. Faça o upload do arquivo binário para sua conta do Amazon S3, em um bucket de sua escolha
2. Uma vez carregado, dentro do S3, selecione o arquivo bin >> Mais (botão no topo da lista de arquivos) >> Tornar público
3. Sua URI do S3 deve ser algo assim: http://bucket-name.s3.ap-south-1.amazonaws.com/sketch-name.ino.bin
4. Copie a URI dispare-a no seu navegador ou faça o curl `curl -I -v http://bucket-name.ap-south-1.amazonaws.com/sketch-name.ino.bin` para validar o mesmo

### Build e Upload
1. Carrege o [arquivo](https://github.com/eduautomatiza/AWS_S3_OTA_Update_HTTPS/blob/main/AWS_S3_OTA_Update_HPPTS.ino) para seu sketch do arduino
2. Configure com seu WIFI_SSID, WIFI_PASSWORD e a URI do arquivo .ino localizado na Amazon S3
3. Compile(build)
4. Carrege(upload) o sketch para o módulo
5. Use o monitor serial para ver a saída

### Saída esperada
```
Aguardando WiFi...
Atualizando firmware. Pode demorar de 2 a 5 minutos.
Atualização terminada. Reboot para rodar novo firmware.
```
### Saída esperada usando Platformio com Framework Arduino
Saída do terminal definindo nível de debug para verbose no arquivo platformio.ini
```
build_flags = 
   -D CORE_DEBUG_LEVEL=ARDUHAL_LOG_LEVEL_VERBOSE
```
Saída completa
```
Processing esp32doit-devkit-v1 (platform: espressif32; board: esp32doit-devkit-v1; framework: arduino)
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Verbose mode can be enabled via `-v, --verbose` option
CONFIGURATION: https://docs.platformio.org/page/boards/espressif32/esp32doit-devkit-v1.html
PLATFORM: Espressif 32 (3.5.0) > DOIT ESP32 DEVKIT V1
HARDWARE: ESP32 240MHz, 320KB RAM, 4MB Flash
DEBUG: Current (esp-prog) External (esp-prog, iot-bus-jtag, jlink, minimodule, olimex-arm-usb-ocd, olimex-arm-usb-ocd-h, olimex-arm-usb-tiny-h, olimex-jtag-tiny, tumpa)
PACKAGES: 
 - framework-arduinoespressif32 3.10006.210326 (1.0.6) 
 - tool-esptoolpy 1.30100.210531 (3.1.0) 
 - tool-mkspiffs 2.230.0 (2.30) 
 - toolchain-xtensa32 2.50200.97 (5.2.0)
LDF: Library Dependency Finder -> https://bit.ly/configure-pio-ldf
LDF Modes: Finder ~ chain, Compatibility ~ soft
Found 28 compatible libraries
Scanning dependencies...
Dependency Graph
|-- <HTTPUpdate> 1.3
|   |-- <HTTPClient> 1.2
|   |   |-- <WiFi> 1.0
|   |   |-- <WiFiClientSecure> 1.0
|   |   |   |-- <WiFi> 1.0
|   |-- <Update> 1.0
|   |-- <WiFi> 1.0
|-- <WiFi> 1.0
|-- <WiFiClientSecure> 1.0
|   |-- <WiFi> 1.0
Building in release mode
Retrieving maximum program size .pio/build/esp32doit-devkit-v1/firmware.elf
Checking size .pio/build/esp32doit-devkit-v1/firmware.elf
Advanced Memory Usage is available via "PlatformIO Home > Project Inspect"
RAM:   [=         ]  12.0% (used 39336 bytes from 327680 bytes)
Flash: [=======   ]  69.6% (used 911634 bytes from 1310720 bytes)
Configuring upload protocol...
AVAILABLE: esp-prog, espota, esptool, iot-bus-jtag, jlink, minimodule, olimex-arm-usb-ocd, olimex-arm-usb-ocd-h, olimex-arm-usb-tiny-h, olimex-jtag-tiny, tumpa
CURRENT: upload_protocol = esptool
Looking for upload port...
Use manually specified: /dev/ttyUSB0
Uploading .pio/build/esp32doit-devkit-v1/firmware.bin
esptool.py v3.1
Serial port /dev/ttyUSB0
Connecting........_____....._
Chip is ESP32-D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme None
Crystal is 40MHz
MAC: 24:62:ab:[REMOVIDO]
Uploading stub...
Running stub...
Stub running...
Changing baud rate to 921600
Changed.
Configuring flash size...
Auto-detected Flash size: 4MB
Flash will be erased from 0x00001000 to 0x00005fff...
Flash will be erased from 0x00008000 to 0x00008fff...
Flash will be erased from 0x0000e000 to 0x0000ffff...
Flash will be erased from 0x00010000 to 0x000eefff...
Compressed 17104 bytes to 11191...
Writing at 0x00001000... (100 %)
Wrote 17104 bytes (11191 compressed) at 0x00001000 in 0.4 seconds (effective 348.6 kbit/s)...
Hash of data verified.
Compressed 3072 bytes to 128...
Writing at 0x00008000... (100 %)
Wrote 3072 bytes (128 compressed) at 0x00008000 in 0.1 seconds (effective 436.8 kbit/s)...
Hash of data verified.
Compressed 8192 bytes to 47...
Writing at 0x0000e000... (100 %)
Wrote 8192 bytes (47 compressed) at 0x0000e000 in 0.1 seconds (effective 594.4 kbit/s)...
Hash of data verified.
Compressed 911744 bytes to 526623...
Writing at 0x00010000... (3 %)
Writing at 0x0001ae82... (6 %)
Writing at 0x00025c34... (9 %)
Writing at 0x00031a65... (12 %)
Writing at 0x00049620... (15 %)
Writing at 0x0004f069... (18 %)
Writing at 0x00054979... (21 %)
Writing at 0x00059d93... (24 %)
Writing at 0x0005ef3b... (27 %)
Writing at 0x000643b4... (30 %)
Writing at 0x0006998c... (33 %)
Writing at 0x0006ed27... (36 %)
Writing at 0x0007614b... (39 %)
Writing at 0x0007e6c0... (42 %)
Writing at 0x00083da7... (45 %)
Writing at 0x00089622... (48 %)
Writing at 0x0008ec85... (51 %)
Writing at 0x0009436f... (54 %)
Writing at 0x00099d12... (57 %)
Writing at 0x0009f9cf... (60 %)
Writing at 0x000a57e4... (63 %)
Writing at 0x000ac512... (66 %)
Writing at 0x000b26dd... (69 %)
Writing at 0x000b8508... (72 %)
Writing at 0x000bdfa4... (75 %)
Writing at 0x000c3b3e... (78 %)
Writing at 0x000c9741... (81 %)
Writing at 0x000cf3ea... (84 %)
Writing at 0x000d5728... (87 %)
Writing at 0x000db5af... (90 %)
Writing at 0x000e1651... (93 %)
Writing at 0x000e7b8c... (96 %)
Writing at 0x000ed8b8... (100 %)
Wrote 911744 bytes (526623 compressed) at 0x00010000 in 7.9 seconds (effective 924.9 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
======================================================================= [SUCCESS] Took 18.00 seconds =======================================================================
--- Available filters and text transformations: colorize, debug, default, direct, esp32_exception_decoder, hexlify, log2file, nocontrol, printable, send_on_enter, time
--- More details at https://bit.ly/pio-monitor-filters

Please build project in debug configuration to get more details about an exception.
See https://docs.platformio.org/page/projectconf/build_configurations.html


--- Miniterm on /dev/ttyUSB0  115200,8,N,1 ---
--- Quit: Ctrl+C | Menu: Ctrl+T | Help: Ctrl+T followed by Ctrl+H ---
04:53:07.633 > [D][WiFiGeneric.cpp:374] _eventCallback(): Event: 0 - WIFI_READY
04:53:07.633 > [D][WiFiGeneric.cpp:374] _eventCallback(): Event: 2 - STA_START
04:53:07.633 > Aguardando WiFi..[D][WiFiGeneric.cpp:374] _eventCallback(): Event: 4 - STA_CONNECTED
04:53:09.757 > [D][WiFiGeneric.cpp:374] _eventCallback(): Event: 7 - STA_GOT_IP
04:53:09.762 > [D][WiFiGeneric.cpp:419] _eventCallback(): STA IP: 10.11.12.49, MASK: 255.255.255.0, GW: 10.11.12.1
04:53:10.502 > .
04:53:10.503 > Atualizando firmware. Pode demorar de 2 a 5 minutos.
04:53:10.508 > [V][HTTPClient.cpp:245] beginInternal(): url: https://[REMOVIDO].s3.us-east-2.amazonaws.com:443/firmwares/[REMOVIDO].esp32.bin
04:53:10.523 > [D][HTTPClient.cpp:293] beginInternal(): protocol: https, host: [REMOVIDO].s3.us-east-2.amazonaws.com port: 443 url: /firmwares/[REMOVIDO].esp32.bin
04:53:12.349 > [D][HTTPClient.cpp:579] sendRequest(): request type: 'GET' redirCount: 0
04:53:12.355 > 
04:53:12.356 > [V][ssl_client.cpp:59] start_ssl_client(): Free internal heap before TLS 278200
04:53:12.363 > [V][ssl_client.cpp:65] start_ssl_client(): Starting socket
04:53:13.035 > [V][ssl_client.cpp:104] start_ssl_client(): Seeding the random number generator
04:53:13.042 > [V][ssl_client.cpp:113] start_ssl_client(): Setting up the SSL/TLS structure...
04:53:13.048 > [V][ssl_client.cpp:129] start_ssl_client(): Loading CA cert
04:53:13.053 > [V][ssl_client.cpp:197] start_ssl_client(): Setting hostname for TLS session...
04:53:13.060 > [V][ssl_client.cpp:212] start_ssl_client(): Performing the SSL/TLS handshake...
04:53:14.769 > [V][ssl_client.cpp:233] start_ssl_client(): Verifying peer X.509 certificate...
04:53:14.776 > [V][ssl_client.cpp:242] start_ssl_client(): Certificate verified.
04:53:14.782 > [V][ssl_client.cpp:257] start_ssl_client(): Free internal heap after TLS 230952
04:53:14.789 > [D][HTTPClient.cpp:1125] connect():  connected to [REMOVIDO].s3.us-east-2.amazonaws.com:443
04:53:14.798 > [V][ssl_client.cpp:295] send_ssl_data(): Writing HTTP request with 578 bytes...
04:53:15.074 > [V][HTTPClient.cpp:1216] handleHeaderResponse(): RX: 'HTTP/1.1 200 OK'
04:53:15.081 > [V][HTTPClient.cpp:1216] handleHeaderResponse(): RX: 'x-amz-id-2: [REMOVIDO]'
04:53:15.093 > [V][HTTPClient.cpp:1216] handleHeaderResponse(): RX: 'x-amz-request-id: [REMOVIDO]'
04:53:15.101 > [V][HTTPClient.cpp:1216] handleHeaderResponse(): RX: 'Date: Sun, 13 Mar 2022 07:53:16 GMT'
04:53:15.109 > [V][HTTPClient.cpp:1216] handleHeaderResponse(): RX: 'Last-Modified: Tue, 11 Jan 2022 17:45:05 GMT'
04:53:15.118 > [V][HTTPClient.cpp:1216] handleHeaderResponse(): RX: 'ETag: "[REMOVIDO]"'
04:53:15.126 > [V][HTTPClient.cpp:1216] handleHeaderResponse(): RX: 'Accept-Ranges: bytes'
04:53:15.133 > [V][HTTPClient.cpp:1216] handleHeaderResponse(): RX: 'Content-Type: application/macbinary'
04:53:15.141 > [V][HTTPClient.cpp:1216] handleHeaderResponse(): RX: 'Server: AmazonS3'
04:53:15.147 > [V][HTTPClient.cpp:1216] handleHeaderResponse(): RX: 'Content-Length: 204592'
04:53:15.154 > [V][HTTPClient.cpp:1216] handleHeaderResponse(): RX: 'Connection: close'
04:53:15.161 > [V][HTTPClient.cpp:1216] handleHeaderResponse(): RX: ''
04:53:15.166 > [D][HTTPClient.cpp:1257] handleHeaderResponse(): code: 200
04:53:15.171 > [D][HTTPClient.cpp:1260] handleHeaderResponse(): size: 204592
04:53:15.176 > [D][HTTPClient.cpp:603] sendRequest(): sendRequest code=200
04:53:15.181 > 
04:53:15.182 > [D][HTTPUpdate.cpp:238] handleUpdate(): Header read fin.
04:53:15.187 > 
04:53:15.187 > [D][HTTPUpdate.cpp:239] handleUpdate(): Server header:
04:53:15.192 > 
04:53:15.192 > [D][HTTPUpdate.cpp:240] handleUpdate():  - code: 200
04:53:15.196 > 
04:53:15.196 > [D][HTTPUpdate.cpp:241] handleUpdate():  - len: 204592
04:53:15.202 > 
04:53:15.202 > [D][HTTPUpdate.cpp:247] handleUpdate(): ESP32 info:
04:53:15.205 > 
04:53:15.206 > [D][HTTPUpdate.cpp:248] handleUpdate():  - free Space: 1310720
04:53:15.211 > 
04:53:15.730 > [D][HTTPUpdate.cpp:249] handleUpdate():  - current Sketch Size: 911744
04:53:15.737 > 
04:53:15.839 > [D][HTTPUpdate.cpp:302] handleUpdate(): runUpdate flash...
04:53:15.844 > 
04:53:16.004 > [D][Updater.cpp:132] begin(): OTA Partition: app1
04:53:26.566 > [D][HTTPUpdate.cpp:339] handleUpdate(): Update ok
04:53:26.571 > 
04:53:26.573 > [V][ssl_client.cpp:265] stop_ssl_socket(): Cleaning SSL connection.
04:53:26.580 > [D][HTTPClient.cpp:400] disconnect(): tcp is closed
04:53:26.583 > 
04:53:26.584 > [D][HTTPClient.cpp:400] disconnect(): tcp is closed
04:53:26.588 > 
04:53:26.588 > [V][ssl_client.cpp:265] stop_ssl_socket(): Cleaning SSL connection.
04:53:26.594 > Atualização terminada. Reboot para rodar novo firmware.
04:53:26.600 > ................
```
