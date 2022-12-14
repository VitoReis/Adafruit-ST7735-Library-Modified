# Why i made this library modification  
I was having troubles with my 0.96" 80x160(RGB) IPS display, so added a new display based on the original INITR_MINI160x80 code  
You can init this new display with initR(INITR_MINI160x80_MOD)  

This display had the following issues when i tried to use the original INITR_MINI160x80:  
* Inverted colors -> RGB to CMY 
* Inverted Red and Blue colors -> RGB to BGR -> BGR to YMC 
* Screen is rotated  
* The starting colum and row of the screen is moved (Some pixels aren't used)

# Modifications on Adafruit_ST7735.cpp file 
Same code of INITR_MINI160x80 but changing the starting row and column and inverting colors  

Modification on line 237 to fix the display colors and X, Y positions  
```c
else if (options == INITR_MINI160x80_MOD) {
    _height = ST7735_TFTWIDTH_80;
    _width = ST7735_TFTHEIGHT_160;
    displayInit(Rcmd2green160x80);
    _colstart = 26;
    _rowstart = 1;
    invertDisplay(1);
}
```  
Modification on line 260 to fix the display rotation  
```c
else if (options == INITR_MINI160x80_MOD) {
    setRotation(3);
}
```

# Modifications on Adafruit_ST7735.cpp file 
Modification on line 15  
```c
#define INITR_MINI160x80_MOD 0x04
```
# Examples using this library  
You can check out my ardagotchi project using this library [here](https://github.com/VitoReis/Ardagotchi) (It's a tamagotchi game made on arduino).