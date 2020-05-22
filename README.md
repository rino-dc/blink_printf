Assalamualaikum.

kali ini kita coba blink dan printf di serial STM32L432KC..
menggunakan STM32CubeIDE ,

Berikut tampilan STM32Cube IDE..

Code sudah saya tulis, jadi sy terangin saja ...

kita coba generate project baru..

1. File > New Project > STM32 Project

2. Pilih microcontroller, disini saya menggunakan NUCLEO-32 STM32L432KC. jadi langsung saya pilih di boardnya. Klik next.

3. Beri nama project, "blink_printf"

4. Klik Next

5. Pilih target and firmware package, jika belum ada anda akan mendownload terlebih dahulu sesuai microcontroller yang di pilih. Klik FINISH

6. karena saya menggunakan Board Nucleo-32, saya langsung aktifkan saja default peripheralnya.. Klik YES

7. Tunggu prosesnya.. sabar...

8. Oke , default LED yang ada di board Nucleo-32 ini ada di LD3 (PB3), Sebagai GPIO_Output..

9. Sedangkan serial ke PC (USB-Serial), dihubungkan ke USART2
PA2 - TX
PA15 - RX

10. Selanjutnya kita klik di SAVE ALL pada menu, lalu code akan di generate..

11. Selanjutnya kita buka project "blink_printf"..

12. buka project "blink_prinf" > "Core" > "Src" > "main.c".

13. pada main.c kita akan menuliskan code.

14. untuk membuat GPIO menjadi HIGH >>  HAL_GPIO_WritePin(LD3_GPIO_Port, LD3_Pin, GPIO_PIN_SET);

15. untuk membuat GPIO menjadi LOW >> HAL_GPIO_WritePin(LD3_GPIO_Port, LD3_Pin, GPIO_PIN_RESET);

16. untuk membuat Delay >> HAL_Delay(1000); "1000" dalam milliseconds.

17. untuk melakukan serial print. atau printf di STM32 maka copy kan code berikut,..


int __io_putchar(int ch)
{
    HAL_UART_Transmit(&huart2, (uint8_t *)&ch, 1, 0xFFFF);
    return ch;
}

int __io_getchar(void)
{
    int ch = 0;
    while(!__HAL_UART_GET_FLAG(&huart2, UART_FLAG_RXNE));
    HAL_UART_Receive(&huart2, (uint8_t *)&ch, 1, 0xFFFF);
    return ch;
}


ke bawah USER CODE BEGIN 4

lalu tambahkan #include "stdio.h"
di bawah USER CODE BEGIN Includes

* code yang ditambahkan diantara tulisan USER CODE BEGIN dan USER CODE END, tidak akan berubah saat kita generate ulang code di STM32CubeMX (saat kita pilih pin IC tadi).
* 
18. untuk printf. maka tuliskan saja printf("LED HIDUP\r\n");

atau printf("LED MATI\r\n");

19. "Save" lalu "Build All"..
"Build Finished. 0 errors, 0 warnings." 

20. Untuk upload ke board. bisa pakai "Debug" atau "Run"

21. kita coba "Debug".
lalu klik "Resume" agar program dijalankan.. 
* dalam mode "Debug" saat program bermasalah kita bisa melihat kesalahannya melalui prespective saat debugging. misal melihat isi variabel yang sering saya pakai..
* 
21. Buka serial monitor,. 

untuk defaultnya sesuai STM32CubeMX kita pakai 115200

untuk merubahnya. kita bisa ubah pada "blink_printf.ioc"

# maaf ternyata tadi yang jalan adalah program yg sebelumya saya buat.. HAHAHA..

22. kita coba ubah baudrate menjadi 9600. 

23. "Connectivity" > "USART2" > "Parameter Setting" > "Baudrate" > tulis "9600". lalu "Save All"

24. sekarang coba kita "Run"

25. klik "ok" pada "Edit Config"

26. pada serial monitor tidak terlihat karena kita sudah ganti baud menjadi 9600.

27. oke sekian tutorial singkat ini.. code dapat di unduh lewat GITHUB yaa..

wassalamualaikum wr wb.
