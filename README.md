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
