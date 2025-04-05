# OpenBook - Andrei Stan 331CC

## Diagrama

- 

## Descriere Functionalitate Hardware
- Tableta este controlata prin cele 3 butoane
- ESP-ul comunica cu memoria flash si SD card-ul
- Trimite date la display pentru afisarea continutului din flash/sd card
- De la USB se folosesc linia de date si cea de putere pentru alimentare
- Linia de alimentare incarca bateria tabletei
- Se folosesc protocoalele i2c si spi pentru comunicatie
- UART se poate folosi prin testpad-uri pentru debugging
## ESP32 Pini
|Pin|Semnal|Descriere|
|---|------|---------|
|EN|RESET|exact ce spune semanalul
|IO0|INT_RTC| conectat la modulul RTC care poate emite intreruperi la anumite alarme/timere
|IO1|32KHz| transmite un semanl de 32Khz care este folosit pentru ceasul tabletei
|IO2|MISO| pentru primirea datelor de la periferic (ex. SD card reader, Flash memorie)
|IO3|EPD_BUSY| pentru a trimite date numai atunci cand display-ul este gata de randat, epaper este incet, deci avem nevoie de acest semnal
|IO4|SS_SD| folosit pentru detectia sd cardului, daca este prezent
|IO5|EPD_DC| comunicatie seriala cu e-paper display-ul
|IO6|SCK| ceas pentru comunicatia SPI cu celelalte componente SPI
|IO7|MOSI| pentru transmisia informatiilor pentru card SD, memorie flash si display
|IO8|GPIO8| neutilizat
|IO9|IO/BOOT| a fost apasat butonul de pornire
|IO10|EPD_CS| Chip select pentru comunicatia seriala
|IO11|FLASH_CS| Chip select pentru memoria flash
|IO12|USB_D-| transfer de date USB diferential -
|IO13|USB_D+| transfer de date USB diferential +
|IO15|IO/Change| butonul de schimbat pagina este apasat
|TXD0| TX| Tx pe UART, este folosit numai la testpad-uri pentru debugging
|RXD0| RX| Rx pe UART, este folosit numai la testpad-uri  pentru debugging
|IO18| RTC_RST| resetare a ceasului de 32Khz
|IO19| I2C_PW| alimentare si chip-select pentru senzor
|IO20| EPD_3v3_c| controleaza transzistorul prin care este alimentat display-ul (nu putem alimenta direct din el sau cel putin e bad practice)
|IO21| SDA| linie de date pentru comunicarea i2c 
|IO22| SCL| semnalul de ceas pentru comunicatrea i2c
|IO23| EPD_RST| resetare a display-ului


## Design Log \ Decizii

* Mufa USB a fost modificata pentru a evita erorile DRC
* Traseele de putere au fost facute prima data, dupa care am folosit autorouter-ul pentru a completa
* Am mutat toate gaurile de pe carcasa si dimensiunile acesteia pentru a intra PCB ul

## BOM
|Qty|Device|Parts|DATASHEET|DESCRIPTION|MOUSER_PRICE-STOCK|
|---|------|-----|---------|-----------|------------------|
|1|ADAFRUIT_LEDCHIP-LED0603|CHG_LED|https://www.vishay.com/doc?82437||https://ro.mouser.com/ProductDetail/Vishay-Semiconductors/VLMY1301-GS08?qs=sGAEpiMZZMusoohG2hS%252B168PbK3WnfgfiGSE4pxVBaDPiKIho6Ieew%3D%3D|
|1|ESP32_WROVER_EAGLE-LTSPICE_RR0402|R15|https://www.vishay.com/doc?20035||https://ro.mouser.com/ProductDetail/Vishay-Dale/CRCW040240K2FKED?qs=rzhQWu8UUS3g49JmcwYN7w%3D%3D&utm_id=20109199409&utm_source=google&utm_medium=cpc&utm_marketing_tactic=emeacorp&gad_source=1&gclid=EAIaIQobChMI4vv9kZaojAMV7YKDBx2W9Ae5EAAYAiAAEgK9cfD_BwE|
|1|ESP32_WROVER_EAGLE-LTSPICE_RR0402|R21|https://www.vishay.com/doc?20035|||
|7|EAGLE-LTSPICE_CC0402|"C3, C4, C5, C9, C18, C19, C_DELAY"|https://ro.mouser.com/datasheet/2/447/KEM_C1006_X5R_SMD-3316465.pdf||https://ro.mouser.com/ProductDetail/KEMET/C0402C475K8PACTU?qs=sGAEpiMZZMsh%252B1woXyUXj%252BeMYF%2FJh1ZHWLnD7xub%252BoY%3D|
|2|ESP32_WROVER_EAGLE-LTSPICE_CC0402|"C24, C25"|https://ro.mouser.com/datasheet/2/447/KEM_C1006_X5R_SMD-3316465.pdf||https://ro.mouser.com/ProductDetail/KEMET/C0402C475K8PACTU?qs=sGAEpiMZZMsh%252B1woXyUXj%252BeMYF%2FJh1ZHWLnD7xub%252BoY%3D|
|1|RCL_CPOL-EUCT3528|C28|https://ro.mouser.com/datasheet/2/447/KEM_T2073_T59X-3316825.pdf||https://ro.mouser.com/ProductDetail/KEMET/T598B335M035ATE150?qs=sGAEpiMZZMsh%252B1woXyUXj9kQnrMN1UR3%252B%2FX%2FiUkAw%2Fg%3D|
|1|ESP32_WROVER_EAGLE-LTSPICE_RR0402|R14|https://www.vishay.com/doc?20035||https://ro.mouser.com/ProductDetail/Vishay-Dale/CRCW040240K2FKED?qs=rzhQWu8UUS3g49JmcwYN7w%3D%3D&utm_id=20109199409&utm_source=google&utm_medium=cpc&utm_marketing_tactic=emeacorp&gad_source=1&gclid=EAIaIQobChMI4vv9kZaojAMV7YKDBx2W9Ae5EAAYAiAAEgK9cfD_BwE|
|12|ESP32_WROVER_EAGLE-LTSPICE_RR0402|"R1, R1_PINH1, R2, R2_PINH1, R3, R5, R6, R7, R8, R10, R11, R17"|https://www.vishay.com/doc?20035|||
|3|ESP32_WROVER_EAGLE-LTSPICE_RR0402|"R_BOOT, R_CHANGE, R_RESET"|https://www.vishay.com/doc?20035|||
|1|ESP32_WROVER_EAGLE-LTSPICE_CC0402|C21|https://ro.mouser.com/datasheet/2/447/KEM_C1006_X5R_SMD-3316465.pdf||https://ro.mouser.com/ProductDetail/KEMET/C0402C475K8PACTU?qs=sGAEpiMZZMsh%252B1woXyUXj%252BeMYF%2FJh1ZHWLnD7xub%252BoY%3D|
|1|112A-TAAR-R03_ATTEND|J1|https://www.attend.com.tw/data/download/file/112A-TAAR-R03_Spec.pdf|"Micro SD Card Socket, Push-Push Type, Top Mount, SMT, H=1.83mm, 10u"|https://www.digikey.com/en/products/detail/attend-technology/112A-TAAR-R03/17633923|
|1|ESP32_WROVER_EAGLE-LTSPICE_RR0402|R_CAPACITOR|https://www.vishay.com/doc?20035|||
|1|EAGLE-LTSPICE_CC0402|C2|https://ro.mouser.com/datasheet/2/447/KEM_C1006_X5R_SMD-3316465.pdf||https://ro.mouser.com/ProductDetail/KEMET/C0402C475K8PACTU?qs=sGAEpiMZZMsh%252B1woXyUXj%252BeMYF%2FJh1ZHWLnD7xub%252BoY%3D|
|10|EAGLE-LTSPICE_CC0402|"C7, C8, C10, C11, C12, C13, C14, C15, C16, C17"|https://ro.mouser.com/datasheet/2/447/KEM_C1006_X5R_SMD-3316465.pdf||https://ro.mouser.com/ProductDetail/KEMET/C0402C475K8PACTU?qs=sGAEpiMZZMsh%252B1woXyUXj%252BeMYF%2FJh1ZHWLnD7xub%252BoY%3D|
|1|ESP32_WROVER_EAGLE-LTSPICE_RR0402|R12|https://www.vishay.com/doc?20035|||
|1|ESP32_WROVER_EAGLE-LTSPICE_RR0402|R1_BAT|https://www.vishay.com/doc?20035|||
|1|ESP32_WROVER_SPARKFUN-DISCRETESEMI_MOSFET_PCH-DMG2305UX-7|Q1|https://www.diodes.com/assets/Datasheets/DMG2305UX.pdf||https://www.digikey.ro/en/products/detail/diodes-incorporated/DMG2305UX-7/4340667|
|1|ESP32_WROVER_SPARKFUN-DISCRETESEMI_MOSFET_PCH-DMG2305UX-7|Q3|https://www.diodes.com/assets/Datasheets/DMG2305UX.pdf||https://www.digikey.ro/en/products/detail/diodes-incorporated/DMG2305UX-7/4340667|
|1|ESP32_WROVER_EAGLE-LTSPICE_RR0402|R16|https://www.vishay.com/doc?20035|||
|2|EAGLE-LTSPICE_CC0402|"C22, C23"|https://ro.mouser.com/datasheet/2/447/KEM_C1006_X5R_SMD-3316465.pdf||https://ro.mouser.com/ProductDetail/KEMET/C0402C475K8PACTU?qs=sGAEpiMZZMsh%252B1woXyUXj%252BeMYF%2FJh1ZHWLnD7xub%252BoY%3D|
|2|ESP32_WROVER_EAGLE-LTSPICE_CC0402|"C26, C27"|https://ro.mouser.com/datasheet/2/447/KEM_C1006_X5R_SMD-3316465.pdf||https://ro.mouser.com/ProductDetail/KEMET/C0402C475K8PACTU?qs=sGAEpiMZZMsh%252B1woXyUXj%252BeMYF%2FJh1ZHWLnD7xub%252BoY%3D|
|1|ESP32_WROVER_EAGLE-LTSPICE_CC0402|C20|https://ro.mouser.com/datasheet/2/447/KEM_C1006_X5R_SMD-3316465.pdf||https://ro.mouser.com/ProductDetail/KEMET/C0402C475K8PACTU?qs=sGAEpiMZZMsh%252B1woXyUXj%252BeMYF%2FJh1ZHWLnD7xub%252BoY%3D|
|2|ESP32_WROVER_EAGLE-LTSPICE_RR0402|"R19, R20"|https://www.vishay.com/doc?20035|||
|1|744043680IND_4828-WE-TPC_WRE|L3|https://www.we-online.com/components/products/datasheet/744043680.pdf||https://ro.mouser.com/ProductDetail/Wurth-Elektronik/744043680?qs=PGXP4M47uW6VkZq%252BkzjrHA%3D%3D&srsltid=AfmBOoq3PLABygfB0-85eEKpA9SffUYwty425nbkhbFJ01kDNoAxFF7J|
|1|BD5229G-TR|IC1|https://fscdn.rohm.com/en/products/databook/datasheet/ic/power/voltage_detector/bd52xxg-e.pdf|"Voltage Detector with Adjustable Delay Time: CMOS processes are utilized to develop high precision  low current consumption CMOS reset ICs that allow arbitrary setting of the delay time. The extensive lineup includes both Nch Open Drain and CMOS output types in a wide range of detection voltages (from 2.3V to 6.0V, in 0.1V steps) enabling selection of the ideal solution based on customer requirements. In addition the entire series is of course both lead-free and RoHS-compliant."|https://www.mouser.co.uk/ProductDetail/ROHM-Semiconductor/BD5229G-TR?qs=4kLU8WoGk0vvnhrrYwdszw%3D%3D|
|1|ESP32_WROVER_BME680_BME680|SENSOR2|https://ro.mouser.com/datasheet/2/783/BST_BME680_DS001-1509608.pdf| Integrated Environmental Unit |https://ro.mouser.com/ProductDetail/Bosch-Sensortec/BME680?qs=v271MhAjFHjo0yA%2FC4OnDQ%3D%3D|
|3|BUTTON_CUSYOMV1|"BOOT_BUTTON, CHANGE_BUTTON, RESET_BUTTON"|https://4donline.ihs.com/images/VipMasterIC/IC/PANA/PANAS45028/PANAS45028-1.pdf?hkey=CECEF36DEECDED6468708AAF2E19C0C6||https://ro.mouser.com/ProductDetail/Panasonic/EVQ-9P701P?qs=NPkb10g2yLBKCwpELvsGNg%3D%3D|
|1|CPH3225A|C6|https://mm.digikey.com/Volume0/opasdata/d220001/medias/docus/6537/rev05-CPHCPM.pdf| 11 mF (EDLC) Supercapacitor 3.3 V 1210 (3225 Metric) - - ||
|1|DS3231SN#|U4|https://ro.mouser.com/datasheet/2/609/DS3231-3421123.pdf| Extremely Accurate I C-Integrated RTC/TCXO/Crystal ||
|1|ESP32-C6-WROOM-1-N8|U1|https://www.espressif.com/sites/default/files/documentation/esp32-c6-wroom-1_wroom-1u_datasheet_en.pdf|" Multiprotocol Modules ESP32-C6 module, Wi-Fi 6 in 2.4 GHz band, Bluetooth 5, Zigbee 3.0 and Thread. ESP34-WROOM Compatible - ENGINEERING SAMPLE "||
|1|ESP32C6_VARISTORCN1812|R18|https://mm.digikey.com/Volume0/opasdata/d220001/medias/docus/2123/CTVS_Standard_Rev2015.pdf||https://www.digikey.be/en/products/detail/epcos-tdk-electronics/CN1812K11G/635074?srsltid=AfmBOora8jXqSIsuJ5wbLbjXOKEBe4X6EtjlDXrR_O7ItUtFQ009LUoi|
|2|ESP32_WROVER_AVX---SD0805S020S1R0_AVX_SD0805S020S1R0_0_0AVX_SD0805S020S1R0_0_0|"D1, D13"|http://datasheets.avx.com/schottky.pdf|||
|1|ESP32_WROVER_SPARKFUN-IC-POWER_MCP73831|MCP73831|https://ro.mouser.com/datasheet/2/268/MCP73831_Family_Data_Sheet_DS20001984H-3441711.pdf||https://www.mouser.dk/ProductDetail/Microchip-Technology/MCP73831T-3ACI-OT?qs=yUQqVecv4quInAWkk8YFWg%3D%3D|
|1|FH34SRJ-24S-0.5SH_99_|J3|https://ro.mouser.com/datasheet/2/185/FH34SRJ_24S_0_5SH_99__CL0580_1255_6_99_2DDrawing_0-1615044.pdf|"24 Position FFC, FPC Connector Contacts, Top and Bottom 0.020"" (0.50mm) Surface Mount, Right Angle"|https://www.mouser.co.uk/ProductDetail/Hirose-Connector/FH34SRJ-24S-0.5SH99?qs=vcbW%252B4%252BSTIpKBl5ap9J8Fw%3D%3D|
|1|MAX17048G+T10|U2|https://ro.mouser.com/datasheet/2/609/MAX17048_MAX17049-3469099.pdf| 3 A 1-Cell/2-Cell Fuel Gauge with ModelGauge ||
|3|MBR0530|"D3, D5, D7"|https://www.onsemi.cn/pdf/datasheet/mbr0530-d.pdf| Diode Schottky 30 V 500mA Surface Mount SOD-123 ||
|6|PGB1010603MR|"D2, D4, D6, D8, D10, D11"|https://www.littelfuse.com/assetdocs/pulseguard-esd-suppressors-pgb1-datasheet?assetguid=8a337998-d54d-466b-be4e-dc5bcd1f9321| 150V (Typ) Clamp - Ipp Tvs Diode Surface Mount 0603 (1608 Metric) ||
|1|QWIIC_CONNECTORJS-1MM|J2|https://ro.mouser.com/datasheet/2/813/Qwiic_Connector_Datasheet-1223982.pdf||https://ro.mouser.com/ProductDetail/SparkFun/PRT-14417?qs=wd5RIQLrsJhgdz%2FpmZ%2F3GQ%3D%3D&srsltid=AfmBOoqQ1oOwS9wen4cUg5-iBLh8Bm57R1iVLhkDmOc94Djde0aRxIcK|
|1|SAMACSYS_PARTS_USB4110-GF-A|J4|https://ro.mouser.com/datasheet/2/837/GCT_USB4110_Product_Drawing___20k_cycles-3455479.pdf|CONN USB 2.0 TYPE-C R/A SMT|https://www.mouser.co.uk/ProductDetail/GCT/USB4110-GF-A?qs=KUoIvG%2F9IlYiZvIXQjyJeA%3D%3D|
|1|SI1308EDL-T1-GE3|Q2|https://www.vishay.com/docs/63399/si1308edl.pdf|" Si1308EDL-T1-GE3 N-channel MOSFET Transistor, 1.5 A, 30 V, 3-Pin SC-70 Siliconix / Vishay SI1308EDL-T1-GE3 "||
|1|USBLC6-2SC6Y|D9|https://ro.mouser.com/datasheet/2/389/usblc6_2sc6y-1852505.pdf| 17V Clamp 5A (8/20 s) Ipp Tvs Diode Surface Mount SOT-23-6 |https://ro.mouser.com/ProductDetail/STMicroelectronics/USBLC6-2SC6Y?utm_campaign=mouser&qs=gNDSiZmRJS%2FOgDexvXkdow==&utm_medium=online&utm_source=snapedaonline&utm_content=model|
|1|W25Q512JVEIQ|U3|https://www.winbond.com/resource-files/W25Q512JV%20SPI%20RevB%2006252019%20KMS.pdf| FLASH - NOR Memory IC 512Mb (64M x 8) SPI - Quad I/O 133 MHz 8-WSON (8x6) ||
|1|XC6220A331MR-G|IC2|https://ro.mouser.com/datasheet/2/760/xc6220-3371556.pdf|LDO Voltage Regulators|https://www.mouser.co.uk/ProductDetail/Torex-Semiconductor/XC6220A331MR-G?qs=AsjdqWjXhJ8ZSWznL1J0gg%3D%3D|



