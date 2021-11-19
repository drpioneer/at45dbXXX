# at45dbXXX

 *  Драйвер для работы с м/сх FLASH-памяти at45dbXXX от Adesto!!! (есть небольшие отличия в работе с памятью от Atmel)
 *  Источники кода:     https://github.com/nimaltd/45dbxxx
 *                      https://github.com/iDiy/AT45DB161D-Drv
 *  Описание работы:    http: //we.easyelectronics.ru/Frankie/spi-programmnyy-pamyat-atmel-dataflash-at45db081d.html
 *                      https://eax.me/stm32-spi-flash/
 *  Настройки SPI1 в CubeMX для работы с микросхемой FLASH-памяти:
 *                      Frame format: Motorola      Data size: 8 bit            First bit: MSB;
 *                      CPOL: LOW                   CPHA:      1 Edge
 *                      CRC:  Disabled              NSS:       Software
 *  Особенности работы с м/сх:
 *  1.  По умолчанию вся память организована по 264/528/1056 байт на страницу. 
 *      Размер страницы можно однократно изменить на 256/512/1024 байт без возможности вернуться обратно.
 *  2.  Микросхема имеет специальные 4 байта для однократной записи идентификатора (например, серийного номера изделия).
 *  3.  Обмен данными производится по 4-х проводному интерфейсу SPI. Микросхема может работать в режимах SPI 0 и 3, 
 *      а также двух собственных режимах Atmel. В коде использован обычный SPI mode 0.
 *  4.  Организация памяти страничная -> доступ к отдельным ячейкам памяти не существует.
 *      Все операции чтения/записи происходят по принципу «чтение-модификация-запись».
 *  5.  После подачи питания и перед обращением к памяти необходимо сделать гарантированную задержку в 20 миллисекунд.
 *  Выявленное отличие м/сх Adesto от м/сх Atmel:   регистр состояния 16-битный, а не 8.
