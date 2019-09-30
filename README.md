# elites


#include <stdio.h>
#include <stdint.h>
#include <ctype.h>

#include "common.h"


void HD44780_Init();
void HD44780_ClrScr();
void HD44780_GotoXY();
void HD44780_PutStr();


void Screen_initialise()
{
	HD44780_Init();//to initialise LCD
	PWM_Init();	     ///to initialize pwm
	PWM_Set3(3,100);//this is to enable the LCD backlight
	char stringBuffer[16] = { 0 };
	HD44780_ClrScr();
	HD44780_GotoXY(1, 0);
	snprintf(stringBuffer, 16, "Bi-Dir Counter");
	HD44780_PutStr(stringBuffer);
	HD44780_GotoXY(0, 1);
	HD44780_PutStr("In:-");
	HD44780_GotoXY(8, 1);
	HD44780_PutStr("Out:-");
	printf("Screen initialisation successful\n");
}

ParserReturnVal_t CmdScreeninit(int mode)
{
  
  if(mode != CMD_INTERACTIVE) return CmdReturnOk;
	Screen_initialise();
  return CmdReturnOk;
}

ADD_CMD("screeninit",CmdScreeninit,"            Bi-directional counter")
