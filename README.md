# FLASHING-OF-LEDS-WITH-LPC-1768

# AIM: 
   To interface and toggle the led with ARM LPC 1768 microprocessor           
           
# COMPONENTS REQUIRED:
##  HARDWARE:
ARM LPC1768
LED
## SOFTWARE:
KEIL MICRO VISION 4.0 IDE

# PROCEDURE:


⮚	Open the Keil software and select the New uvision project from Project Menu as shown below.
⮚	Browse to your project folder and provide the project name and click on save.
⮚	Once the project is saved a new pop up “Select Device for Target” opens, Select the controller (NXP: LPC1768) from NXP (founded by philips) and click on OK.
⮚	Select the controller (NXP: LPC1768) and click on OK.
⮚	As LPC1768 needs the startup code, click on Yes option to include the LPC17xx Startup file.
⮚	Create a new file by file → new to write the program.
⮚	Type the code.
⮚	After typing the code save the file as main.c eg. (abc.c).
⮚	Right click target and Add the suitable files to source group1 and header for the project.
⮚	Add the main.c along with system_LPC17xx.c.
⮚	Build the project and fix the compiler errors/warnings if any.
⮚	Code is compiled with no errors. The .bin file is still not generated.
⮚	Right Click on Target Options to select the option for generating .bin file.
⮚	Set IROM1 start address as 0x2000. Bootloader will be stored from 0x0000- 0x2000 so application should start from 0x2000
⮚	Write	the	command	to	generate	the .bin file	from
.axf file
Command: fromelf --bin projectname.axf --output filename.bin
⮚	in c/c++ → include paths → desktop (00-libfiles).
⮚	.Bin file is generated after a rebuild.
⮚	Check the project folder for the generated .Bin file.

# ADD FILES:
Target1:
Source group1:
Startuplpc17xx.s, main.c (t), delay.c (t), systemlpc17xx.c (t), gpio.c (t)
Header:
Delay.h, stdutils.h, gpioi.h

# PIN DIAGRAM :
~~~
 <img width="426" height="519" alt="image" src="https://github.com/user-attachments/assets/aed28cc3-caed-4895-a9d8-a985d01e6934" />
~~~
# CIRCUIT DIAGRAM:
~~~
<img width="1755" height="1365" alt="image" src="https://github.com/user-attachments/assets/3480f745-6626-4900-99a7-62f160a41faf" />
~~~

# PROGRAM:
~~~
#include <LPC17xx.h>

void delay_ms(unsigned int ms)
{
    unsigned int i, j;
    for(i = 0; i < ms; i++)
        for(j = 0; j < 5000; j++);
}

int main(void)
{
    /* Enable GPIO for PORT0 and PORT1 */
    LPC_GPIO0->FIODIR |= (1 << 22);  // Configure P0.22 as output (LED1)
    LPC_GPIO1->FIODIR |= (1 << 18);  // Configure P1.18 as output (LED2)
    LPC_GPIO1->FIODIR |= (1 << 20);  // Configure P1.20 as output (LED3)

    while(1)
    {
        /* Turn ON LEDs */
        LPC_GPIO0->FIOSET = (1 << 22);   // LED1 ON
        LPC_GPIO1->FIOSET = (1 << 18);   // LED2 ON
        LPC_GPIO1->FIOSET = (1 << 20);   // LED3 ON
        delay_ms(500);

        /* Turn OFF LEDs */
        LPC_GPIO0->FIOCLR = (1 << 22);   // LED1 OFF
        LPC_GPIO1->FIOCLR = (1 << 18);   // LED2 OFF
        LPC_GPIO1->FIOCLR = (1 << 20);   // LED3 OFF
        delay_ms(500);
    }
}
~~~
 
# Output:
 Thus the interface and toggle the led with ARM LPC 1768 microprocessor is done






